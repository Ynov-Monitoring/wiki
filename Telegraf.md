# Telegraf

Nous utilisons les sondes telegraf pour remonter les données dans notre BDD.  
La configuration de ces sondes se fait par le rôle [manala.telegraf](https://github.com/manala/ansible-role-telegraf).  
Vous trouverez ci-dessous un exemple non complet de fichier de conf après lancement du playbook ansible. Les commentaires ont été rajoutés à la main pour le wiki. 

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
    # On renseigne ici les informations pour que la sonde telegraf puisse inscrire ses données dans la base
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