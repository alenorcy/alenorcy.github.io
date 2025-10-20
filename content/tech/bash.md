---
title: "commandes bash"
date: 2022-01-08T14:01:13+01:00
slug: ""
description: ""
keywords: []
draft: false
tags: [bash,shell]
math: false
toc: false
---
## 💻 prompt
```
$ PS1="╭─\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\n╰─➤ "
╭─lenorcy@mydebian:~
╰─➤ 

```

![prompt](/images/prompt.png)


## 🌐 alternatives à telnet pour tester l'ouverture d'un port

avec cat :
```
$ cat < /dev/tcp/www.lenorcy.fr/22
SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
^C
$ cat < /dev/tcp/127.0.0.1/23
bash: connect: Connexion refusée
bash: /dev/tcp/127.0.0.1/23: Connexion refusée
```
avec netcat :
```
$ nc -vz www.lenorcy.info 22
Connection to www.lenorcy.info (217.160.28.69) 22 port [tcp/ssh] succeeded!

```

## 📝 écrire dans un fichier
```
$ cat > fichier.txt <<EOL
Ce fichier contiendra uniquement cette ligne.
EOL
$ cat >> fichier.txt <<EOL
Ajoute cette ligne au fichier s'il existe.
EOL
``
