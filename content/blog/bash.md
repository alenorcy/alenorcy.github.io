---
title: "Bash"
date: 2022-01-08T14:01:13+01:00
slug: ""
description: ""
keywords: []
draft: false
tags: [bash,shell]
math: false
toc: false
---
# prompt
```
╭─lenorcy@mydebian:~
╰─➤ grep "export PS1" ~/.bashrc
export PS1="╭─\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$(__git_check_ps1)\n╰─➤ "

```

![prompt](/images/prompt.png)


# alternative à telnet pour tester l'ouverture d'un port
```
╭─lenorcy@mydebian:~
╰─➤ cat < /dev/tcp/www.lenorcy.fr/22
SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
^C
╭─lenorcy@mydebian:~
╰─➤ cat < /dev/tcp/127.0.0.1/23
bash: connect: Connexion refusée
bash: /dev/tcp/127.0.0.1/23: Connexion refusée
```

# écrire dans un fichier
```
╭─lenorcy@mydebian:~
╰─➤ cat > fichier.txt <<EOL
Ce fichier contiendra uniquement cette ligne.
EOL
╭─lenorcy@mydebian:~
╰─➤ cat >> fichier.txt <<EOL
Ajoute cette ligne au fichier s'il existe.
EOL
```