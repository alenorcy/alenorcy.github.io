---
title: "Bash"
date: 2022-01-08T14:01:13+01:00
slug: ""
description: ""
keywords: []
draft: true
tags: []
math: false
toc: false
---
# Prompt
```
╭─lenorcy@mydebian:~
╰─➤ grep "export PS1" ~/.bashrc
export PS1="╭─\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$(__git_check_ps1)\n╰─➤ "

```

![prompt](/images/prompt.png)
