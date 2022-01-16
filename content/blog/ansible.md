---
title: "Ansible"
date: 2022-01-16T16:34:28+01:00
slug: ""
description: ""
keywords: []
draft: true
tags: [ansible, shell]
math: false
toc: false
---

Exécuter une commande shell via ansible en ligne de commande
```
╭─lenorcy@mydebian:~
╰─➤ ansible -m shell -a 'cat /etc/redhat-release' redhat-group
Vault password:
```