# Retention Policy

> Documentation officielle : https://docs.influxdata.com/influxdb/v1.8/query_language/manage-database/#create-retention-policies-with-create-retention-policy

Nous avons créer plusieurs politiques de rétention afin de gérer la durée de vie des données stocker dans InfluxDB

**RP1month** : Politique de rétention par défaut de 1 heure

`CREATE RETENTION POLICY RP1month ON monitoring DURATION 4w REPLICATION 1 DEFAULT`

**RP3month** : Politique de rétention de 2 heures

`CREATE RETENTION POLICY RP3month ON monitoring DURATION 12w REPLICATION 1`

**RP6month** : Politique de rétention de 3 heures

`CREATE RETENTION POLICY RP6month ON monitoring DURATION 24w REPLICATION 1`

# Continuous Queries

> Documentation officielle : https://docs.influxdata.com/influxdb/v1.8/query_language/continuous_queries/

Les continuous queries nous permettent de grouper différentes données en une seule afin de d'alléger la base de données 
Une nouvelle donnée est récupérée par telegraf et envoyé à InfluxDB toutes les 10 secondes.

**RP1toRP3** : Continuous query qui récupère toute les données de measurement sur 10s et fait une moyenne sur 1 minute et les envoie sur RP6hour (voir au dessus) 

```sql
CREATE CONTINUOUS QUERY RP1toRP2 on monitoring
RESAMPLE EVERY 1h FOR 1h 
BEGIN 
   SELECT mean(*) INTO RP3month.:MEASUREMENT 
   FROM /.*/ 
   GROUP BY time(1m), * 
END
```

**RP3toRP6** : Continuous query qui récupère toute les données de RP6Hour sur 1 minute et fait une moyenne sur 10 minute et les envoie sur RP10hour (voir au dessus) 

```sql
CREATE CONTINUOUS QUERY RP2toRP3 on monitoring 
RESAMPLE EVERY 2h FOR 2h 
BEGIN 
   SELECT mean(*) INTO RP6month.:MEASUREMENT 
   FROM RP3month./.*/ 
   GROUP BY time(10m), * 
END"
```
