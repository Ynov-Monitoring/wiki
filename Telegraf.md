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