# Ansible 

Ansible est un outil d'automatisation de configuration de systèmes d'informations. Notre projet s'articule autour de cette solution et nous permet de s'inscrire dans une démarche devops en développant une infrastructure "_As Code_". \
\
Pour l'installer, deux solutions s'offrent à vous :
1. Passer par le gestionnaire de paquet pip :
   - `# apt install python-pip3`
   - `# pip3 install ansible` 
2. Passer par votre gestionnaire de paquet favori
   - `# apt install ansible`

Vérification de l'installation : \
```bash
$ ansible --version
ansible 2.10.3
```

## Utilisation

Ansible utilise la notion de playbook. Un playbook fait le lien entre un inventaire et un ensemble de tâche. \
Dans notre cas, si on veut lancer notre playbook sur notre infrastructure locale, il faut lancer la commande suivante :\
`$ ansible-playbook -i inventories/local playbook/main-infra.yml`\
\
Les inventaires contiennent des informations sensibles telle que les IP et les méthodes de connexion aux machines. Il devient donc nécessaire de chiffrer ces informations. Ansible permet cela :\
```bash
# Demande de mot de passe interactive
$ ansible-playbook -i inventories/local --ask-vault-pass playbook/main-infra.yml

# Mot de passe stocker dans le fichier vault.pass
$ ansible-playbook -i inventories/local --vault-password-file=pass.vault playbook/main-infra.yml 
```