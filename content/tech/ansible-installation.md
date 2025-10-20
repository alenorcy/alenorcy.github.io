---
title: "installation d'Ansible"
date: 2022-01-16T16:34:28+01:00
slug: ""
description: "Guide rapide pour installer et mettre à jour Ansible sur la machine d'administration (node manager)."
keywords: [ansible, shell, python, automation]
draft: false
tags: [ansible, shell, python]
math: false
toc: false
---

🧭 Voici comment installer **Ansible** sur la machine d'administration, également appelée **node manager**.

---

## 🧰 Vérification de l’environnement Python

Avant toute installation, vérifier que `pip` est disponible :

```
python3 -m pip -V
```

Si la commande retourne une version de `pip`, tout est prêt.

---

## 📦 Installation d’Ansible

Installer Ansible pour l’utilisateur courant :

```
python3 -m pip install --user ansible
```

- Installe Ansible dans le répertoire utilisateur (`~/.local/bin`)
- Ne nécessite pas de privilèges administrateur
- Ajoute les exécutables dans `$PATH` (si le dossier `~/.local/bin` est inclus)

---

## 🔄 Mise à niveau d’Ansible

Pour mettre à jour vers la dernière version disponible :

```
python3 -m pip install --upgrade --user ansible
```

- Met à jour tous les modules Ansible installés par `pip`
- Conserve la configuration existante

---

## 💡 Bonnes pratiques

- 🧩 Vérifier la version installée :  
  ```
  ansible --version
  ```

- 🧰 Mettre à jour `pip` avant une nouvelle installation :  
  ```
  python3 -m pip install --upgrade pip
  ```

- 📦 Installer Ansible dans un environnement virtuel si plusieurs versions de Python cohabitent :  
  ```
  python3 -m venv ansible-env
  source ansible-env/bin/activate
  python -m pip install ansible
  ```

---

## 📘 Documentation officielle

👉 [Guide officiel d’installation d’Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible)

---
🕓 Dernière mise à jour : 2025-10-19
