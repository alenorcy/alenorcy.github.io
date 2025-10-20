---
title: "différence entre apt, aptitude et dpkg"
date: 2025-10-19T22:56:03+02:00
tags: [sysadmin, shell]
draft: false 
---
🧭 Sous Debian, Ubuntu et leurs dérivés, plusieurs outils permettent de gérer les paquets. Ils se complètent mais n'opèrent pas au même niveau du système.

---

## 📦 Les rôles de base

| Outil | Niveau | Gère les dépendances | Télécharge depuis dépôts | Usage typique |
|-------|--------|--------------------|------------------------|---------------|
| dpkg | Bas niveau | Non | Non | Installation/suppression directe de `.deb` |
| apt / apt-get | Moyen | Oui | Oui | Gestion quotidienne des paquets et mises à jour |
| aptitude | Haut niveau | Oui (résolution avancée) | Oui | Résolution interactive et choix de solutions |

---

## ⚙️  Les commandes principales

### apt upgrade

Met à jour les paquets installés sans ajouter ni supprimer de dépendances.

```
sudo apt update && sudo apt upgrade
```

- Met à jour les dépendances déjà installées  
- N’installe aucun nouveau paquet  
- Ne supprime rien  

Utilisation : mise à jour « sûre » du système, sans changement de structure.

---

### apt full-upgrade (ou apt-get dist-upgrade)

Met à jour tout le système, en ajoutant ou supprimant des paquets si nécessaire.

```
sudo apt full-upgrade
```

- Installe les nouvelles dépendances requises  
- Supprime les paquets obsolètes si nécessaire  
- Peut modifier la structure du système  

Utilisation : mise à jour complète, par exemple avant une montée de version.

---

### aptitude safe-upgrade

Met à jour les paquets installés sans installer ni supprimer d’autres paquets.  
Equivalent moderne de l’ancienne commande `aptitude upgrade`.

```
sudo aptitude safe-upgrade
```

- Met à jour uniquement les paquets existants  
- N’installe ni ne supprime de paquets  
- Utilise le moteur de résolution d’`aptitude` (plus intelligent que celui d’`apt`)  
- Peut proposer des solutions alternatives en cas de conflit  

Utilisation : mise à jour « sûre » du système, comme `apt upgrade`, mais avec résolution avancée.

---

### aptitude full-upgrade

Met à jour tout le système, en ajoutant ou supprimant des paquets si nécessaire.  
Équivalent d’un `apt full-upgrade`, mais avec une résolution de dépendances plus flexible.

```
sudo aptitude full-upgrade  
```

- Installe les nouvelles dépendances requises
- Supprime les paquets obsolètes ou incompatibles  
- Propose plusieurs solutions possibles en cas de conflit  
- Peut rétrograder ou conserver certains paquets selon les choix de l’utilisateur  

Utilisation : mise à jour complète du système, utile quand `apt full-upgrade` échoue à cause de dépendances complexes.

---

### Synthèse apt / aptitude : upgrade, safe-upgrade et full-upgrade

| Commande | Comportement | Ajoute/Supprime des paquets ? | Résolution automatique ? |
|-----------|--------------|-------------------------------|---------------------------|
| **apt upgrade** | Met à jour les paquets installés sans toucher aux dépendances | Non | Non |
| **apt full-upgrade** | Met à jour tout le système, ajoute ou supprime des paquets si nécessaire | Oui | Non |
| **aptitude safe-upgrade** | Met à jour sans modifier les dépendances (remplace `aptitude upgrade`) | Non | Oui (propose des solutions) |
| **aptitude full-upgrade** | Met à jour tout le système avec dépendances, en proposant des solutions aux conflits | Oui | Oui (applique la meilleure solution) |

**Différence principale :**  
- `apt` applique les changements de manière directe, sans proposer d’alternatives.  
- `aptitude` est plus "intelligent" : il propose des solutions interactives lorsque des conflits ou dépendances complexes apparaissent.
---

## 🧱 Identifier et gérer les paquets « conservés »

Quand apt upgrade ne peut pas mettre à jour un paquet, il est indiqué comme conservé (held back).

### Vérifier les paquets upgradables et conservés

```
apt list --upgradable
apt list --upgradable | grep "\[held back\]"
```

### Simuler la mise à jour d’un paquet pour voir pourquoi il est bloqué

```
sudo apt -s install <nom_du_paquet>
```

(-s = simulate)

### Débloquer ou mettre à jour un paquet manuellement

```
sudo apt install <nom_du_paquet>
sudo apt full-upgrade
```

### Si le paquet est en « hold » manuel

```
apt-mark showhold
sudo apt-mark unhold <nom_du_paquet>
```

---

## 🧰 dpkg : l’outil bas niveau

dpkg installe, configure ou supprime des fichiers `.deb`.  
Il ne résout pas les dépendances ni n'interagit avec les dépôts.

| Objectif | Commande |
|----------|----------|
| Installer un paquet local | sudo dpkg -i fichier.deb |
| Supprimer un paquet | sudo dpkg -r paquet |
| Supprimer avec fichiers de configuration | sudo dpkg -P paquet |
| Lister les paquets installés | dpkg -l |
| Obtenir le statut d’un paquet | dpkg -s paquet |
| Lister les fichiers installés par un paquet | dpkg -L paquet |
| Reconfigurer les paquets partiellement installés | sudo dpkg --configure -a |

Si `dpkg -i` provoque des erreurs de dépendances :

```
sudo apt -f install
```

apt corrigera alors les dépendances manquantes.

---

### 💡 apt vs apt-get

- **`apt upgrade` = `apt-get upgrade`** → même comportement, seul l’affichage diffère.  
  - `apt` : interface moderne et lisible (pour l’humain)  
  - `apt-get` : sortie brute et stable (pour les scripts)

- **`apt full-upgrade` = `apt-get dist-upgrade`** → même fonction, seule la syntaxe change.  
  - `apt full-upgrade` : nom plus explicite et convivial  
  - `apt-get dist-upgrade` : commande historique, toujours valable pour les scripts

## 📘 Bonnes pratiques

**Mise à jour de routine :**

```
sudo apt update && sudo apt upgrade
```

**Mise à jour complète (nouvelles dépendances / suppressions) :**

```
sudo apt full-upgrade
```

**Nettoyage :**

```
sudo apt autoremove
sudo apt autoclean
```

**Diagnostic / réparation :**

```
sudo dpkg --configure -a
sudo apt -f install
```

---

## 🚀 Résumé rapide

| Commande | Niveau de risque | Gère les dépendances ? | Supprime des paquets ? | Usage conseillé |
|----------|-----------------|------------------------|------------------------|----------------|
| apt upgrade | Faible | Partiellement | Non | Mise à jour sûre |
| apt full-upgrade | Moyen | Oui | Oui | Mise à jour complète |
| aptitude full-upgrade | Moyen | Oui (intelligent) | Oui | Mise à jour avec résolution avancée |
| dpkg -i | Élevé | Non | Non | Installation manuelle d’un `.deb` |

---

**En résumé :**

- dpkg pose les briques (`.deb`)  
- apt / apt-get gèrent le chantier (dépôts, dépendances)  
- aptitude ajoute une couche de raisonnement pour résoudre les conflits

---

🕓 Dernière mise à jour : 2025-10-19
