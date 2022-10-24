---
title: "Ansible"
date: 2022-01-16T16:34:28+01:00
slug: ""
description: ""
keywords: []
draft: false 
tags: [ansible, shell]
math: false
toc: false
---

**Objectif** : Pouvoir administrer la machine `lab.lenorcy.fr` depuis le __node manager__ `admin.lenorcy.fr`


## Installation d'Ansible sur le __node manager__ 

doc officielle : https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible

Vérification de la présence de pip :
```
╭─lenorcy@mydebian:~
╰─➤  python3 -m pip -V
```

Installation d'ansible :
```
╭─lenorcy@mydebian:~
╰─➤  python3 -m pip install --user ansible
```

Mise à niveau d'ansible :
```
╭─lenorcy@mydebian:~
╰─➤  python3 -m pip upgrade --user ansible
```

Création de la paire de clés et copie de la clé publique sur lab.lenorcy.fr :
```
ssh-keygen -f ~/.ssh/ansible-home
ssh-copy-id -i ~/.ssh/ansible-home.pub ansible@lab.lenorcy.fr
```

## 


