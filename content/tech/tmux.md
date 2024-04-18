---
title: "Tmux - Commandes de base"
date: 2024-04-16T16:34:28+01:00
slug: ""
description: ""
keywords: []
draft: false 
tags: [tmux, shell]
math: false
toc: false
---

Voici les commandes de base de **Tmux** (multiplexeur de terminaux) 

## Sessions :

Lister les sessions:
  * `$ tmux ls`

Démarrer une session (verbeux) :
  * `$ tmux -v`

Démarrer une session en la nommant directement :
  * `$ tmux new -s un-nom`

Renommer une session :
  * [ctrl]+[B] puis [$]

Attacher une session :
  * `$ tmux a -t <name>`

Tuer une session :
  * `$ tmux kill-session -t <name>`

Détacher une session :
  * [ctrl]+[B] puis [d]


## Fenêtres :

Création d'une fenêtre :
  * [ctrl]+[B] puis [c]
  * `$ tmux new-window`

Renommer la fenêtre :
  * [ctrl]+[B] puis [,]
  * `$ tmux rename-window nouveau_nom_sans_espace`

Fenêtre suivante :
  * [ctrl]+[B] puis [n] 
  * `$ tmux select-window -n`

Fenêtre précédante :
  * [ctrl]+[B] puis [p]
  * `$ tmux select-window -p`

Fenêtre précise (par numéro) :
  * [ctrl]+[B] puis [0…9]
  * `$ tmux select-window -t :0-9`


## Panneaux :

Diviser verticalement :
  * [ctrl]+[B] puis [%]
  * `$ tmux split-window -h`

Diviser horizontalement :
  * [ctrl]+[B] puis [“]
  * `$ tmux split-window`

Panneau suivante :
  * [ctrl]+[B] puis flèche droite

Panneau précédant :
  * [ctrl]+[B] puis flèche gauche 

Précédemment utilisé :
  * [ctrl]+[B] puis [;]

Echanger les panneaux :
  * [ctrl]+[B] puis [o]

Fermer un panneau (ou une fenêtre) :
  * [ctrl]+[B] puis \[x\]
  * `$ exit`

