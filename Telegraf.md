# Telegraf

Nous utilisons les sondes telegraf pour remonter les données dans notre BDD.  
La configuration de ces sondes se fait par le rôle [manala.telegraf](https://github.com/manala/ansible-role-telegraf). Cette configuration est consultable dans les _group\_vars_ `playbook/group_vars/all/main.yml`
Vous trouverez ci-dessous un exemple non complet de fichier de conf (_/etc/telegraf/telegraf.conf_) après lancement du playbook ansible. Les commentaires ont été rajoutés à la main pour le wiki. \

```conf
# Configuration générale de la sonde 
[agent]
    interval = "100s"
    hostname = "MaMachine"
    round_interval = true
    flush_interval = "10s"
    logfile = "/var/log/telegraf/telegraf.log"

###############################################################################
#                                  OUTPUTS                                    #
###############################################################################

[[outputs.influxdb]]
    # On renseigne ici les informations pour que la sonde telegraf puisse 
    # inscrire ses données dans la base
    urls = ["http://influxdb:8086"]
    database = "database"
    username = "user"
    password = "password"

###############################################################################
#                                  INPUTS                                     #
###############################################################################

# On séléctionne ici les métriques qui nous interessent
[[inputs.system]]
[[inputs.cpu]]
[[inputs.mem]]
[[inputs.disk]]
[[inputs.netstat]]
```
\
Une fois le fichier édité, bien penser à redémarrer le service `systemctl restart telegraf` pour prendre en compte les changements. \
Vous pouvez vérifier que tout fonctionne correctement en regardant le status du service `systemctl status telegraf`
```
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/lib/systemd/system/telegraf.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 1969-07-20 13:37:00 UTC; 12h 0min ago
     Docs: https://github.com/influxdata/telegraf
```


Pour un hôte Windows, on va utiliser un script qui devra être lancé après la création d'une vm.

```
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12

if ($args[0] -eq $null)
{
	throw "Vous devez renseigner le nom du projet."
}

if ($args[1] -ne $null)
{
		throw "Vous ne pouvez mettre qu'un seul nom de projet. Utilisez des guillemets si besoin."
}

# téléchargement de telegraf via web request
#Invoke-WebRequest https://dl.influxdata.com/telegraf/releases/telegraf-1.13.3_windows_amd64.zip -OutFile C:\telegraf.zip -UseBasicParsing

# unzip et suppr l'archive
Expand-Archive C:\telegraf.zip -DestinationPath C:\
rm C:\telegraf.zip

# création des dossiers de conf et logs
mkdir C:\telegraf\telegraf.d
mkdir C:\telegraf\logs

# suppression fichier de conf
del C:\telegraf\telegraf.conf


ADD-content -path "C:\telegraf\telegraf.conf" -value '[global_tags]
projet = "projet_var_to_replace"
[agent]
  interval = "10s"
  round_interval = true
  metric_batch_size = 1000
  metric_buffer_limit = 10000
  collection_jitter = "0s"
  flush_interval = "10s"
  flush_jitter = "0s"
  precision = ""
  hostname = ""
  omit_hostname = false


###############################################################################
#                            OUTPUT PLUGINS                                   #
###############################################################################


# Configuration for sending metrics to InfluxDB
[[outputs.influxdb]]
  urls = ["http://192.168.3.132:8086"]
  database = "telegraf"
   username = "CHANGEME"
   password = "CHANGEME"


###############################################################################
#                            INPUT PLUGINS                                    #
###############################################################################

  [[inputs.cpu]]
  percpu = true
  totalcpu = true
  collect_cpu_time = false
  
  [[inputs.mem]]

  [[inputs.disk]]
  
  [[inputs.diskio]]
  
  [[inputs.io]]

  [[inputs.processes]]
 
  [[inputs.swap]]

  [[inputs.system]]
  
  [[inputs.net]]'


ADD-content -path "C:\telegraf\telegraf.d\win_perf_counters.conf" -value '[[inputs.win_perf_counters]]
  [[inputs.win_perf_counters.object]]
    ObjectName = "Processor"
    Instances = ["*"]
    Counters = [
      "% Idle Time",
      "% Interrupt Time",
      "% Privileged Time",
      "% User Time",
      "% Processor Time",
      "% DPC Time",
    ]
    Measurement = "cpu"
    IncludeTotal=true

  [[inputs.win_perf_counters.object]]
    ObjectName = "LogicalDisk"
    Instances = ["*"]
    Counters = [
      "% Idle Time",
      "% Disk Time",
      "% Disk Read Time",
      "% Disk Write Time",
      "Current Disk Queue Length",
      "% Free Space",
      "Free Megabytes",
    ]
    Measurement = "disk"

  [[inputs.win_perf_counters.object]]
    ObjectName = "PhysicalDisk"
    Instances = ["*"]
    Counters = [
      "Disk Read Bytes/sec",
      "Disk Write Bytes/sec",
      "Current Disk Queue Length",
      "Disk Reads/sec",
      "Disk Writes/sec",
      "% Disk Time",
      "% Disk Read Time",
      "% Disk Write Time",
    ]
    Measurement = "diskio"

  [[inputs.win_perf_counters.object]]
    ObjectName = "Network Interface"
    Instances = ["*"]
    Counters = [
      "Bytes Received/sec",
      "Bytes Sent/sec",
      "Packets Received/sec",
      "Packets Sent/sec",
      "Packets Received Discarded",
      "Packets Outbound Discarded",
      "Packets Received Errors",
      "Packets Outbound Errors",
    ]
    Measurement = "net"

  [[inputs.win_perf_counters.object]]
    ObjectName = "System"
    Counters = [
      "Context Switches/sec",
      "System Calls/sec",
      "Processor Queue Length",
      "System Up Time",
    ]
    Instances = ["------"]
    Measurement = "system"

  [[inputs.win_perf_counters.object]]
    ObjectName = "Memory"
    Counters = [
      "Available Bytes",
      "Cache Faults/sec",
      "Demand Zero Faults/sec",
      "Page Faults/sec",
      "Pages/sec",
      "Transition Faults/sec",
      "Pool Nonpaged Bytes",
      "Pool Paged Bytes",
      "Standby Cache Reserve Bytes",
      "Standby Cache Normal Priority Bytes",
      "Standby Cache Core Bytes",

    ]
    Instances = ["------"]
    Measurement = "mem"
    IncludeTotal=true

  [[inputs.win_perf_counters.object]]
    ObjectName = "Paging File"
    Counters = [
      "% Usage",
    ]
    Instances = ["_Total"]
    Measurement = "swap"'

# récupération du tag group
# $projet = Get-Content -Path C:\temp\project.txt
# (Get-Content -path "C:\telegraf\telegraf.conf" -Raw) -replace 'projet_var_to_replace',$projet | Set-Content "C:\telegraf\telegraf.conf"

# récupération du tag group en mode argument
$projet_arg=$args[0]
(Get-Content -path "C:\telegraf\telegraf.conf" -Raw) -replace 'projet_var_to_replace',$projet_arg | Set-Content "C:\telegraf\telegraf.conf"

# test
# C:\telegraf\telegraf.exe --config=C:\telegraf\telegraf.conf --config-directory=C:\telegraf\telegraf.d --test

# installation
C:\telegraf\telegraf.exe --service install --config C:\telegraf\telegraf.conf --config-directory C:\telegraf\telegraf.d

# service start
net start telegraf
```
Pour lancer le script il faut lancer un powershell et taper : ./script install telegraf - measurement.ps1 nom_projet
Il prend un paramètre et un paramètre seulement : le nom du projet pour lequel sera déployée la vm.
Dans son fonctionnement, il télécharge le dernier package de Telegraf, l'installe dans c:\telegraf\ et y ajoute deux fichiers de configuration.
Le premier, telegraf.conf, contient l'adresse IP et les identifiants pour se connecter à influxDB.
Le deuxième, win_perf_counters.conf, contient toutes les métriques et leur nom qui seront utilisées par Graphana.
Enfin, il lance le service telegraf sur la machine hôte.
