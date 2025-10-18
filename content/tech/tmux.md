---
title: "Tmux - Commandes de base"
date: 2024-04-16T16:34:28+01:00
tags: [tmux, shell]
draft: false
toc: false
---

🧭 Mémo des principales commandes du multiplexeur de terminaux **Tmux**.

---

## 🗂️ Sessions

| Action | Raccourci clavier | Commande |
|:--|:--|:--|
| **Lister les sessions** | — | `tmux ls` |
| **Créer une session** | — | `tmux` |
| **Créer une session nommée** | — | `tmux new -s <nom>` |
| **Renommer la session** | `Ctrl+b`, `$` | `tmux rename-session -t <ancien> <nouveau>` |
| **Attacher une session** | — | `tmux attach -t <nom>` |
| **Détacher la session** | `Ctrl+b`, `d` | `tmux detach` |
| **Tuer une session** | — | `tmux kill-session -t <nom>` |
| **Basculer entre sessions** | `Ctrl+b`, `s` | — |
| **Rejoindre la dernière session** | `Ctrl+b`, `L` | — |

---

## 🪟 Fenêtres

| Action | Raccourci clavier | Commande |
|:--|:--|:--|
| **Nouvelle fenêtre** | `Ctrl+b`, `c` | `tmux new-window` |
| **Renommer la fenêtre** | `Ctrl+b`, `,` | `tmux rename-window <nom>` |
| **Fenêtre suivante** | `Ctrl+b`, `n` | `tmux next-window` |
| **Fenêtre précédente** | `Ctrl+b`, `p` | `tmux previous-window` |
| **Aller à une fenêtre (0–9)** | `Ctrl+b`, `0–9` | `tmux select-window -t :0-9` |
| **Lister les fenêtres** | `Ctrl+b`, `w` | — |
| **Fermer la fenêtre** | `Ctrl+b`, `&` | `tmux kill-window` |

---

## 🧩 Panneaux

| Action | Raccourci clavier | Commande |
|:--|:--|:--|
| **Diviser verticalement** | `Ctrl+b`, `%` | `tmux split-window -h` |
| **Diviser horizontalement** | `Ctrl+b`, `"` | `tmux split-window` |
| **Aller au panneau voisin** | `Ctrl+b`, flèches | `tmux select-pane -[UDLR]` |
| **Basculer entre panneaux (cyclique)** | `Ctrl+b`, `o` | — |
| **Dernier panneau actif** | `Ctrl+b`, `;` | — |
| **Échanger deux panneaux** | `Ctrl+b`, `Ctrl+o` | — |
| **Agrandir/réduire un panneau** | `Ctrl+b`, `z` | — |
| **Fermer le panneau** | `Ctrl+b`, `x` | `exit` |

---

## 📋 Gestion du texte

| Action | Raccourci clavier | Commande |
|:--|:--|:--|
| **Entrer en mode copie** | `Ctrl+b`, `[` | — |
| **Quitter le mode copie** | `q` ou `Enter` | — |
| **Copier la sélection** | `Space` (début) → `Enter` (copie) | — |
| **Coller** | `Ctrl+b`, `]` | — |

> 💡 Astuce : On peut configurer tmux pour utiliser le presse-papiers système (`set -g mouse on`, `set-option -g set-clipboard on`).

---

## ⚙️ Divers & astuces

| Action | Raccourci clavier | Commande |
|:--|:--|:--|
| **Afficher l’horloge** | `Ctrl+b`, `t` | — |
| **Afficher la liste des raccourcis** | `Ctrl+b`, `?` | — |
| **Recharger la configuration** | — | `tmux source-file ~/.tmux.conf` |
| **Quitter Tmux** | — | `exit` ou `Ctrl+d` |
| **Mode plein écran (zoom)** | `Ctrl+b`, `z` | — |
| **Activer la souris** | — | `set -g mouse on` dans `~/.tmux.conf` |

---

💡 **Conseils**
- Chaque **session** peut contenir plusieurs **fenêtres**, elles-mêmes divisées en **panneaux**.  
- `Ctrl+b d` (détacher) et `tmux a` (reprendre).  
- Faire des alias :  
  ```bash
  alias ta="tmux attach -t"
  alias tn="tmux new -s"
  alias tls="tmux ls"
