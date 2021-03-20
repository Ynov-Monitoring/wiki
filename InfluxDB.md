# InfluxDB 

Toutes nos données sont stocké dans une base de données InfluxDB. Nous avons sélectionné cette solution car elle est opensource, bien documentée et éprouvé dans le milieu professionnel. \
\
Nous utilisons le rôle galaxy [manala.influxdb](https://github.com/manala/ansible-role-influxdb) pour configurer notre influx. Cette configuration est consultable dans les _group\_vars_ `playbook/group_vars/main/main.yml` \
Les points importants sont les suivants : 
1. Création d'une base pour accueillir les données
2. Ajout d'utilisateurs :
   1.  Pour telegraf avec les droits de _Write_ sur la base précédement créée
   2.  Pour Grafana avec les droits de _Read_ sur la base précédement créée
3. Les répertoires pour stocker les données, métadonnées et WAL (Write Ahead Log). 
4. Les _Continuous\_queries_ 

\
Point important : Nous utilisons la **version 1.8** d'influxdb. La version 2.0 étant récente, nous ne l'avons pas encore intégrée au projet.  
\
Les données rentrent ensuite dans un cycle de vie. Ce cycle est géré par les _Retention Policies_. Un article sur ce sujet [consultable ici](https://github.com/Ynov-Monitoring/deployment/wiki/Retention-de-donn%C3%A9es) a été rédigé.  

## Exemple de connexion à la DB et de visualisation de données

```sql
influx -precision rfc3339

use <nom_de_la_db>

SELECT cpu, usage_idle, host, projet from cpu ORDER BY DESC LIMIT 20

SELECT cpu, mean_usage_idle, host, projet from <nom_de_la_retention_policy>.cpu ORDER BY DESC LIMIT 20
```