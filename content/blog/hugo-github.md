---
title: "Faire un site statique avec Hugo et l'héberger sur Github"
date: 2021-11-28T21:36:49+01:00
slug: ""
description: ""
keywords: []
draft: false 
tags: [hugo,web]
math: false
toc: false
---
Voici la procédure pour créer une site statique avec [Hugo](https://gohugo.io/) et l'héberger sur [github](https://github.com) !

_Pré-requis : avoir déjà créé un compte Github_

  * [Création d'un repository Github](#1)
  * [Création du site en local (sur Ubuntu)](#2)
  * [Création du dépôt Git local](#3)
  * [Mise en place d'un thème pour Hugo](#4)
  * [Premier test](#5)
  * [Première synchronisation distante](#6)
  * [Configuration finale sur le repositoy Github](#7)

## Création du repository Github {#1}

Depuis votre profil, cliquez sur l'onglet sur _Repositories_ puis sur le bouton _New_ : 

![New repository Github](/images/Selection_516.png)

Saisissez un nom avec ce format **[login].github.io** (attention ce format précis est indispensable !) :

![Repository name](/images/Selection_518.png)

Github vous indique ensuite quelques conseils d'utilisation :

![Git advice](/images/Selection_471.png)


## Création du site en local (sur Ubuntu) {#2}

Installation de Hugo (sur Ubuntu 20.04) :
```
snap install hugo --channel=extended
```

Création du site avec [Hugo](https://gohugo.io/) :
```
hugo new site alenorcy.github.io
```

## Création du dépôt Git local {#3}

On crée le dépôt local et on récupère le thème [codex](https://github.com/jakewies/hugo-theme-codex) :
```
cd alenorcy.github.io
git init
```

## Mise en place d'un thème pour Hugo {#4}

On choisit le thème **codex**
```
git submodule add https://github.com/jakewies/hugo-theme-codex.git themes/hugo-theme-codex
cp themes/hugo-theme-codex/exampleSite/config.toml .
```

On modifie quelques lignes du fichier _config.toml_ :
  * On commente la ligne **themesDir = "../../"**,
  * On modifie **title**, **baseURL** dans les paramètres globales,
  * On modifie **twitter** et **github** dans les paramètres optionels [params],

## Premier test {#5}

Lancement du site en local :
```
hugo server -D
```

En lançant l'URL http://localhost:1313/ dans son navigateur, on peut vérifier si le site statique est OK :

![Hugo desktop screenshot](/images/screenshot-hugo.png)

## Première synchronisation distante {#6}

On envoie les fichiers locaux vers la branche distante (main) :
```
git add .
git commit -m "premier commit"
git branch -M main
git remote add origin https://*******-mon_token-***********@github.com/alenorcy/alenorcy.github.io.git
git push -u origin main
```

## Configuration finale sur le repositoy Github {#7}

Dans Settings > Pages > Source, on positionne construction du site statique dans la branche distante "gh-pages" :
![gh-pages](/images/Selection_517.png)


On créé le fichier _.github/workflows/gh-pages.yml_ suivant (depuis l'interface de Github dans la branche **main**) :
```
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

On le récupère en local :
```
git pull
```

Et c'est terminé :-)

On peut ensuite mettre à jour son site en local... et pousser les modifications sur Github :

```
git add .
git commit -m "mes modifications blabla"
git push -u origin main
```

Liens : 
  * https://gohugo.io/getting-started/quick-start/
  * https://gohugo.io/hosting-and-deployment/hosting-on-github/

Bonne journée.
