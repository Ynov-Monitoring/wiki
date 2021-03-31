Vagrant permet un déploiement de VM sur Virtualbox et Vmware _As Code_

## Installation
Suivre l'installation sur [la doc officielle](https://learn.hashicorp.com/collections/vagrant/getting-started) 

## Utilisation
Il faut être dans le dossier où se trouve le fichier `Vagrantfile` et taper la commande `vagrant up`  

## Quelques commandes communes
```bash
# Monte toutes les machines renseignées dans le Vagrantfile
# Il est possible de ne monter qu'une machine en précisant 
# son nom 
vagrant up

# Eteint les machines 
vagrant halt

# Supprime les machines 
vagrant destroy -f

# Reload les machines si le Vagrantfile a été modifié
vagrant reload
```

## Avantage
1- Avoir un environnement uniforme entre tous les membres de l'équipe  
2- Gain de temps considérable pour déployer un ensemble de VM  