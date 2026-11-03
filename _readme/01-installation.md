# 01 — Installation

Temps estimé : **10 à 20 minutes**.

BrainOS n'appartient à aucune application. C'est un dossier de fichiers que Claude lit et modifie. Tu choisis la surface dans laquelle tu travailles avec lui, et tu peux en changer quand tu veux.

---

## Ce qu'il te faut

- **Un abonnement Claude Pro ou Max** ([claude.ai/pricing](https://claude.ai/pricing)). Claude Code, qui travaille dans ton dossier, n'est pas inclus dans le plan gratuit. C'est la seule dépense.
- **Une surface Claude Code**, au choix (étape 3).
- **Obsidian**, facultatif, pour lire ton wiki (étape 4).

---

## Étape 1 — Récupérer le template

### Option A (la plus simple) — Télécharger un ZIP

1. Sur la page GitHub du template, clique sur le bouton vert **Code**.
2. Clique sur **Download ZIP**.
3. Dézippe le fichier dans ton dossier **Documents**, et renomme le dossier en `BrainOS` (sans accent ni espace).

### Option B — GitHub Desktop

Dans [GitHub Desktop](https://desktop.github.com) : **File → Clone repository → URL**, colle `https://github.com/t-rlnd/BrainOS`, choisis ton dossier Documents.

### Option C — Git

```bash
git clone https://github.com/t-rlnd/BrainOS.git ~/Documents/BrainOS
```

> 💡 Choisis un endroit stable : les surfaces se souviennent de ta base par son chemin. Un dossier synchronisé (iCloud Drive, Dropbox, OneDrive) fonctionne, et permet de lire ta base dans Obsidian sur ton téléphone. Mais si tu utilises Git sur plusieurs ordinateurs, la synchronisation et Git peuvent se gêner.

Vérifie que tu vois `company/`, `todo/`, `raw/`, `wiki/` et `CLAUDE.md`. Le dossier `.claude/` est caché : sur Mac, **Cmd + Maj + .** dans le Finder pour l'afficher.

---

## Étape 2 — Lire avant d'accepter

Les commandes de `.claude/commands/` sont des instructions qui agissent sur tes fichiers. Elles sont courtes et en français. Ouvre au moins `analyze.md` et lis-le. Règle à garder pour toujours : n'ajoute jamais à ta base une commande ou un skill que tu n'as pas lu.

---

## Étape 3 — Ouvrir ta base dans ta surface

| Surface | Pour qui | Ce qu'il faut installer |
|---|---|---|
| **Claude Desktop, onglet Code** | Tout le monde. Aucun terminal. | [Claude Desktop](https://claude.ai/download) |
| **Le terminal** | Les habitués de la ligne de commande | Claude Code en ligne de commande |
| **Un éditeur** (VS Code, Cursor, JetBrains) | Ceux qui codent déjà | L'extension Claude Code de l'éditeur |
| **claude.ai/code** | Ceux qui ont mis leur base sur GitHub | Rien |

Toutes lisent le même `CLAUDE.md` et proposent les mêmes commandes. Si tu hésites, prends Claude Desktop.

### Claude Desktop (recommandé)

1. Installe [Claude Desktop](https://claude.ai/download) et connecte-toi.
2. Ouvre l'onglet **Code**.
3. Choisis de travailler dans un dossier, puis sélectionne ton dossier `BrainOS`.
4. Si ton système te demande d'autoriser l'accès aux fichiers, accepte.

### Le terminal

Installe Claude Code avec la commande indiquée sur la [page officielle](https://docs.claude.com/en/docs/claude-code), puis :

```bash
cd ~/Documents/BrainOS
claude
```

La première fois, une page web s'ouvre pour te connecter à ton compte Claude.

### Un éditeur de code

Installe l'extension **Claude Code** depuis la boutique d'extensions de ton éditeur. Ouvre le dossier `BrainOS` (Fichier → Ouvrir le dossier), puis le panneau de l'extension, et démarre une session.

### claude.ai/code

Mets ta base dans un dépôt GitHub **privé**, connecte GitHub à claude.ai, puis choisis ton dépôt sur [claude.ai/code](https://claude.ai/code). Claude travaille dans une copie de ta base et y enregistre ses modifications : récupère-les sur ton ordinateur avant d'y travailler.

---

## Étape 4 — Obsidian (facultatif)

Obsidian rend ton wiki agréable à lire : liens cliquables, propriétés, vue graphe.

1. Télécharge-le sur [obsidian.md/download](https://obsidian.md/download).
2. Lance-le, clique **Ouvrir un dossier comme coffre**, sélectionne `BrainOS`.

Le template contient déjà les réglages de base dans `.obsidian/`. Ton `CLAUDE.md` interdit à Claude d'y toucher.

---

## Étape 5 — Vérifier

Dans ta surface, colle :

```text
Lis le CLAUDE.md de ce dossier, puis dis-moi :
1. comment cette base est organisée, en une ligne par dossier ;
2. quelles commandes sont disponibles dans .claude/commands/ ;
3. ce qu'il manque dans le CLAUDE.md pour qu'il soit complet.
Ne modifie rien.
```

Claude doit décrire `company/`, `todo/`, `raw/` et `wiki/`, citer les six commandes (`/analyze`, `/brain`, `/lint`, `/daily`, `/todo`, `/do`) et te signaler que « Qui tu es » est encore un modèle. C'est normal : on le remplit à l'étape suivante.

Tape ensuite `/` : tes commandes apparaissent. Si elles n'y sont pas, vérifie que tu as ouvert le dossier `BrainOS` lui-même, et pas le dossier qui le contient.

---

## Ton prochain pas

→ **[02-configure-your-brain.md](02-configure-your-brain.md)** — on configure ton BrainOS via une conversation avec Claude.
