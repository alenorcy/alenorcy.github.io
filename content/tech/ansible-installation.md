---
title: "[Ansible] Installation"
date: 2022-01-16T16:34:28+01:00
slug: ""
description: ""
keywords: []
draft: false 
tags: [ansible, shell, python]
math: false
toc: false
---

**Objectif** : Installer ansible sur la machine d'administration appelée également le __node manager__.


## Installation d'Ansible sur le __node manager__ 

[Documention officielle](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible)

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


