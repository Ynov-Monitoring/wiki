# Retention Policy

Nous avons créer plusieurs politiques de rétention afin de gérer la durée de vie des données stocker dans InfluxDB

**RP1hour** : Politique de rétention par défaut de 1 heure

`CREATE RETENTION POLICY RP1hour ON monitoring DURATION 1h REPLICATION 1 DEFAULT`

**RP6hour** : Politique de rétention de 2 heures

`CREATE RETENTION POLICY RP6hour ON monitoring DURATION 2h REPLICATION 1`

**RP10hour** : Politique de rétention de 3 heures

`CREATE RETENTION POLICY RP10hour ON monitoring DURATION 3h REPLICATION 1`

# Continuous Queries

Les continuous queries nous permettent de grouper différentes données en une seule afin de d'alléger la base de données 
Une nouvelle donnée est récupérée par telegraf et envoyé à InfluxDB toutes les 10 secondes.

**CQ1** : Continuous query qui récupère toute les données de measurement sur 10s et fait une moyenne sur 1 minute et les envoie sur RP6hour (voir au dessus) 

`CREATE CONTINUOUS QUERY CQ10sTo1min on monitoring RESAMPLE EVERY 1h FOR 1h BEGIN SELECT mean(*) INTO RP6hour.:MEASUREMENT FROM /.*/ GROUP BY time(1m), * END"`

**CQ2** : Continuous query qui récupère toute les données de RP6Hour sur 1 minute et fait une moyenne sur 10 minute et les envoie sur RP10hour (voir au dessus) 

`CREATE CONTINUOUS QUERY CQ1minTo10min on monitoring RESAMPLE EVERY 2h FOR 2h BEGIN SELECT mean(*) INTO RP10hour.:MEASUREMENT FROM RP6hour./.*/ GROUP BY time(10m), * END"`
