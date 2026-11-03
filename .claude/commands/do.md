---
description: Reprendre une action de todo/ avec son contexte, la traiter, puis proposer de la cocher
argument-hint: [sujet ou extrait de l'action]
---

# /do — Reprendre une action

**Sujet** : $ARGUMENTS

## Flux à exécuter

### 1. Retrouver l'action

- Chercher dans `todo/` les actions non cochées qui correspondent à `$ARGUMENTS` (`Grep`).
- Plusieurs résultats → les lister et demander laquelle. Aucun → le dire et proposer `/todo`.
- `$ARGUMENTS` vide → lister les 5 actions non cochées les plus anciennes et demander laquelle reprendre.

### 2. Charger le contexte

- Ouvrir les pages liées sur la ligne (`[[...]]`) : client, projet, réunion, source.
- Lire `company/writing-rules.md` si l'action consiste à écrire (e-mail, relance, post).
- Résumer en 3 à 5 lignes où en est le sujet : date d'ajout de l'action, dernier échange, décisions liées.

### 3. Travailler

Faire l'action avec l'utilisateur. Les livrables vont dans `outputs/drafts/`. Ne rien envoyer.

### 4. Clore

- Proposer de cocher l'action. **Ne jamais cocher sans accord explicite.**
- Si accord : passer `- [ ]` à `- [x]` et ajouter `· fait le YYYY-MM-DD` en fin de ligne.
- Si l'action est abandonnée : la barrer (`~~…~~`), ne jamais la supprimer.
- Mettre à jour la page wiki liée si l'action a fait avancer le sujet.
- Skill `append-log` avec `operation: todo`.
