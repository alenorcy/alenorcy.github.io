---
title: "premier playbook Ansible !"
date: 2022-11-11T15:18:26+01:00
slug: ""
description: "Créer un premier playbook Ansible pour tester la connexion ping depuis le node manager."
keywords: [ansible, python, shell]
draft: false
tags: [ansible, python, sysadmin, shell]
math: false
toc: false
---
🧭 L'objectif est d'écrire un petit **playbook** qui permettra de faire un **ping** de _lab.lenorcy.fr_ depuis le **node manager** (noeud d'administration) sur lequel nous avons [installé Ansible](/tech/ansible-installation/).

---

## 🔑 Connexion SSH avec clés depuis le node manager

Sur la machine `lab.lenorcy.fr`, créer l’utilisateur `ansible` :
```
sudo adduser ansible
```
Rajouter l'utilisateur au groupe `sudo` (pas nécessaire pour notre premier playbook)
```
sudo usermod -aG sudo ansible
```

Sur le **node manager**, générer une paire de clés et copier la clé publique sur le noeud distant :
```
ssh-keygen -f ~/.ssh/ansible-home
ssh-copy-id -i ~/.ssh/ansible-home.pub ansible@lab.lenorcy.fr
```

---

## 🧰 Préparation de l'environnement

### 📁 Arborescence de travail sur le node manager :
```
├── ansible.cfg (f)
├── ping.yml (f)
├── connexion-ansible.yml (f)
├── group_vars (d)
│   └── all (d)
│   └── ansible_account_vault.yml (f)
└── inventories (d)
    └── hosts (f)
```

### 📝 Fichiers à créer

| Fichier | Emplacement | Rôle |
|:--|:--|:--|
| `ansible.cfg` | Racine du projet Ansible | Fichier de configuration principale d’Ansible : inventaire par défaut, options SSH, chemins des rôles, etc. |
| `ping.yml` | Racine du projet Ansible | Playbook exécutant un test de connectivité (`ping`) sur les hôtes cibles. |
| `inventories/hosts` | Dossier `inventories` | Liste des machines gérées (groupes et hôtes). |
| `inventories/connexion-ansible.yml` | Dossier `inventories` | Variables globales définissant la méthode de connexion (`ansible_user`, `ansible_become`, etc.). |
| `inventories/group_vars/all/ansible_account_vault.yml` | Dossier `inventories/group_vars/all` | Contient les secrets chiffrés via Ansible Vault (mot de passe sudo, tokens, etc.). |

### 📁 Création des dossiers :
```
mkdir -p inventories/group_vars/all
```

---

## 📦 Fichier de configuration `ansible.cfg`
```
cat > ansible.cfg <<EOL
[defaults]
inventory = inventories
ask_vault_pass = true
roles_path = roles
interpreter_python = /usr/bin/python3

[ssh_connection]
pipelining = True
EOL
```

---

## 📂 Fichier d'inventaire `hosts`
```
cat > inventories/hosts <<EOL
[lab]
lab.lenorcy.fr
EOL
```

---

## 🔧 Variables de connexion dans le fichier `connexion-ansible.yml`
```
cat > inventories/connexion-ansible.yml <<EOL
all:
vars:
ansible_user: ansible
ansible_become: yes
ansible_become_method: sudo
ansible_become_pass: "{{ ansible_account_password }}"
EOL
```

> Seul `ansible_user` n'est véritablement nécessaire pour ce simple premier playbook 

---

## 🔐 Vault pour le mot de passe

Créer le fichier `Vault` :
```
ansible-vault edit inventories/group_vars/all/ansible_account_vault.yml
```

Ajouter le mot de passe :
```
ansible_account_password: "censured"
```

> Le `vault` n'est pas nécessaire pour ce premier playbook. Nous aurons rapidement besoin de privilèges pour exécuter certaines opérations.

---

## 📝 Création du premier playbook `ping.yml`
```
cat > ping.yml <<EOL

    hosts: all
    vars:
    ansible_become: no # ping n'a pas besoin d'être root
    tasks:

        ping:
EOL
```

---

## 🚀 Exécution du playbook
```
ansible-playbook ping.yml -l lab


Entrer le mot de passe du Vault si demandé.  
Exemple de sortie :

PLAY [all] **********************************************************************************************

TASK [Gathering Facts] **********************************************************************************
ok: [lab.lenorcy.fr]

TASK [ping] *********************************************************************************************
ok: [lab.lenorcy.fr]

PLAY RECAP **********************************************************************************************
lab.lenorcy.fr : ok=2 changed=0 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0
```

---

## 💡 Alternative : module ping directement

Il existe un module **ping** évitant la création d’un playbook :
```
ansible -m ping lab.lenorcy.fr -e ansible_become=no
```

Exemple de sortie :
```
lab.lenorcy.fr | SUCCESS => {
"changed": false,
"ping": "pong"
}
```

> Très pratique pour tester rapidement la connectivité Ansible.

---
