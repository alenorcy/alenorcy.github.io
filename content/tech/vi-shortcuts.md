---
title: "commandes utiles sous vi / vim"
date: 2025-12-07T17:23:43+01:00
draft: false 
---
# 🧠 Fiche mémo

## 📄 Insérer du contenu d’un fichier
| Action | Commande |
|--------|----------|
| Insérer le contenu d'un fichier | `:r chemin-vers-le-fichier` |
| Insérer la sortie d’une commande (ex: secret OpenSSL) | `:r !openssl rand -base64 32` |

---

## 🪟 Gestion des splits (fenêtres)
### **Split horizontaux** (haut / bas)
| Action | Commande |
|--------|----------|
| Ouvrir un split horizontal | `:split` |
| Raccourci équivalent | `:sp` |

### **Split verticaux** (gauche / droite)
| Action | Commande |
|--------|----------|
| Ouvrir un split vertical | `:vsplit` |
| Raccourci équivalent | `:vs` |

---

## 📝 Mode insertion
| Action | Commande |
|--------|----------|
| Insérer avant le curseur | `i` |
| Insérer en début de ligne | `I` |
| Ajouter après le curseur | `a` |
| Ajouter en fin de ligne | `A` |
| Ouvrir une nouvelle ligne en dessous | `o` |
| Ouvrir une nouvelle ligne au-dessus | `O` |

---

## 🎯 Déplacements essentiels
| Action | Commande |
|--------|----------|
| Début de ligne | `0` |
| Première non‑espacement | `^` |
| Fin de ligne | `$` |
| Début du fichier | `gg` |
| Fin du fichier | `G` |
| Avancer d’un mot | `w` |
| Reculer d’un mot | `b` |
| Aller au mot suivant | `e` |
| Aller à la ligne n | `:n` |

---

## ✂️ Copie / collage / suppression
| Action | Commande |
|--------|----------|
| Copier (yank) une ligne | `yy` |
| Copier un mot | `yw` |
| Copier jusqu’à fin de ligne | `y$` |
| Coller après le curseur | `p` |
| Coller avant le curseur | `P` |
| Supprimer une ligne | `dd` |
| Supprimer un mot | `dw` |
| Supprimer jusqu’à fin de ligne | `d$` |

---

## 🔍 Recherche et remplacement
| Action | Commande |
|--------|----------|
| Rechercher une chaîne | `/mot` |
| Rechercher vers l’arrière | `?mot` |
| Suivant | `n` |
| Précédent | `N` |
| Remplacer *mot1* par *mot2* dans tout le fichier | `:%s/mot1/mot2/g` |
| Confirmer chaque remplacement | `:%s/mot1/mot2/gc` |

---

## 💾 Sauvegarde & sortie
| Action | Commande |
|--------|----------|
| Sauvegarder | `:w` |
| Quitter | `:q` |
| Sauvegarder et quitter | `:wq` |
| Quitter sans sauvegarder | `:q!` |

---
