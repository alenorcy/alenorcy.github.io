---
title: "[Ansible] Premier playbook !"
date: 2022-11-11T15:18:26+01:00
slug: ""
description: ""
keywords: []
draft: false
tags: [ansible,python,shell]
math: false
toc: false
---

**Objectif:** Administrer la machine lab.lenorcy.fr depuis le __node manager__. Nous allons tout d'abord tenter de faire un ping via ansible.


## Connexion ssh avec clés depuis le __node manager__

Sur la machine lab.lenorcy.fr, nous créons l'utilisateur ansible :
```
adduser ansible
usermod -G sudo ansible
```

Sur le __node manager__ nous allons créer une paire de clés, puis nous copions la clé publique sur le noeud distant (lab.lenorcy.fr) :
```
ssh-keygen -f ~/.ssh/ansible-home
ssh-copy-id -i ~/.ssh/ansible-home.pub ansible@lab.lenorcy.fr
```

## Préparation de l'environnement

Nous allons créer l'arborescence de travail suivante sur le node manager :
```
├── ansible.cfg (f)
├── ping.yml (f)
└── inventories 
    ├── connexion-ansible.yml (f)
    ├── group_vars
    │   └── all
    │       └── ansible_account_vault.yml (f)
    └── hosts (f)
```  

Création des dossiers :
```
mkdir -p inventories/group_vars/all
```

Création du fichier de configuration de base ansible.cfg :
```
cati > ansible.cfg <<EOL 
[defaults]
inventory          = inventories
ask_vault_pass     = true
roles_path         = roles
interpreter_python = /usr/bin/python3

[ssh_connection]
pipelining         = True
EOL
```

Création du fichier inventaire hosts :
```
cat > inventories/hosts <<EOL
[lab]
lab.lenorcy.fr
EOL
```

Création du fichier contenant les variables permettant la connexion avec le compte ansible :
```
cat > inventories/connexion-ansible.yml <<EOL
# Mode de connexion par défaut avec compte Ansible
all:

  vars:
    ansible_user: ansible 
    ansible_become: yes
    ansible_become_method: sudo
    ansible_become_pass: "{{ ansible_account_password }}"
EOL
```

Création du fichier __vault__ qui contiendra le secret : 
```
ansible-vault edit ansible_account_vault.yml
```

Nous y mettons le mot de passe :
```
ansible_account_password: "censured"
```
Ainsi positionné dans l'arborescence, ce mot de passe pourra servir à administrer tous les noeuds.

Création de notre premier script ansible (qu'on appelle également **playbook**) qui réalisera un test de ping ! :
```
cat > ping.yml <<EOL 
---
- hosts: all
  vars:
  # puisque la commande ping ne necessite pas d'être root, on positionne ansible_become à no
    ansible_become: no
  tasks:
    - ping:
EOL    
```

## Exécution de notre premier playbook !

On utilise la commande ansible-playbook :
```
╭─~
╰─➤ ansible-playbook ping.yml -l lab
Vault password: 

PLAY [all] **********************************************************************************************

TASK [Gathering Facts] **********************************************************************************
ok: [lab.lenorcy.fr]

TASK [ping] *********************************************************************************************
ok: [lab.lenorcy.fr]

PLAY RECAP **********************************************************************************************
lab.lenorcy.fr             : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

Il existe un module **ping** évitant la création d'un playbook. Il suffit de le charger via la commande **ansible** :
```
$ ansible -m ping lab.lenorcy.fr -e ansible_become=no
Vault password: 
lab.lenorcy.fr | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
