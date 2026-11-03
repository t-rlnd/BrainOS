---
description: Créer ou compléter la note quotidienne et en extraire les éléments wiki
argument-hint: [optionnel : contenu libre à ajouter à la note]
---

# /daily — Note quotidienne

**Input éventuel** : $ARGUMENTS

## Flux à exécuter

### 1. Session loading (si pas déjà fait)

- Lire `index.md`
- `grep "^## \[" log.md | head -10`

### 2. Localiser ou créer la note du jour

Chemin : `daily/YYYY-MM-DD.md` (format ISO, date du jour).

- Si le fichier n'existe **pas** : le créer à partir du template ci-dessous.
- Si le fichier existe : l'ouvrir pour complétion.

Template d'une note quotidienne :

```markdown
---
title: "YYYY-MM-DD"
type: daily
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# YYYY-MM-DD

## Focus du jour

(à remplir)

## Ce que j'ai fait

-

## Ce que j'ai appris

-

## À ingérer dans le wiki

-

## Questions ouvertes

-
```

### 3. Si input fourni

Si l'utilisateur a passé un texte en argument, l'intégrer dans la section pertinente :
- Mentions d'apprentissage → "Ce que j'ai appris"
- Mentions de sources/liens → "À ingérer dans le wiki"
- Sinon → "Ce que j'ai fait"

### 4. Extraction pour le wiki

Relire la note complète et identifier :
- **Sources à ingérer** (URLs, livres, podcasts mentionnés) → proposer un `/analyze` pour chacune
- **Entités nouvelles** (personne/outil/entreprise non encore dans le wiki) → proposer une page `wiki/entities/`
- **Concepts évoqués** qui mériteraient une page dédiée
- **Actions** à faire (relancer, envoyer, préparer…) → proposer de les ranger dans `todo/` avec `/todo`

**Ne pas ingérer automatiquement** — proposer à l'utilisateur les extractions à lancer, une par une.

### 5. Ne jamais modifier une note passée

Règle stricte de `CLAUDE.md` : les notes de jours antérieurs sont immuables. Si l'utilisateur veut compléter hier, lui dire que ce n'est pas permis et suggérer de l'écrire dans la note du jour en référençant `[[daily/YYYY-MM-DD]]`.

### 6. Log

Utiliser la skill `append-log` avec `operation: daily` et un titre court (ex: `daily · focus cadrage client X`).

## Règles

- Respect total du fichier quotidien de l'utilisateur : Claude n'écrit que ce que l'utilisateur a validé.
- Une seule note par jour.
- Pas de création multiple de daily à la chaîne.
