# Les playbook utilisés

Dans cette section, nous allons parler des playbooks que nous utilisons dans notre projet.  
## Main-infra.yml

Pour commencer, le playbook *main-infra.yml* va s'occuper de monter les principaux composants de l'infrastructure. Les tâches réalisées sont les suivantes : 
1. Mise à jour des dépots de nos machines linux puis ajout du dépot InfluxDB
2. Installation de Ansible sur la machine *Ansible* via le rôle de [Geerlingguy](https://galaxy.ansible.com/geerlingguy/ansible)
3. Installation et configuration d'influxDB via le rôle [Manala](https://galaxy.ansible.com/manala/influxdb) puis configuration des politique de rétentions via un rôle développé par nous même (influxDB-retention-policy)
4. Lancement du playbook [Telegraf.yml](#telegraf.yml)
5. Ajout des sources Grafana dans le dépot des machines du groupe grafana
6. Installation et configuration des services grafana via le rôle galaxy [Manala Grafana](https://galaxy.ansible.com/manala/grafana)

## telegraf.yml
Comme son nom l'indique, ce playbook installe et configure les sondes telegraf.
1. Ajout des sources telegraf dans les dépots de toutes les machines 
2. Installation et configuration des sondes via le rôle galaxy [dj-wasabi](https://galaxy.ansible.com/dj-wasabi/telegraf)