---
description: Interroger le wiki BrainOS et proposer d'archiver la réponse dans synthesis/
argument-hint: [question en langage naturel]
---

# /brain — Query du wiki

**Question** : $ARGUMENTS

## Flux à exécuter

### 1. Session loading (si pas déjà fait)

- Lire `index.md` pour orienter
- `grep "^## \[" log.md | head -10`

### 2. Ciblage des pages

À partir de `index.md` et des `--index-*.md` pertinents, identifier les pages du wiki susceptibles de contenir une réponse.

Utiliser :
- `Grep` sur les mots-clés de la question dans tout `wiki/`
- `Glob` pour repérer les pages par dossier
- Les `--index-*.md` pour repérer par description

### 3. Lecture ciblée

Lire **seulement** les pages identifiées comme pertinentes (3 à 10 max). Pas de lecture exhaustive du wiki.

### 4. Synthèse

Construire la réponse avec :
- **Réponse directe** en tête (2–5 phrases)
- **Développement** structuré, chaque affirmation reliée à une page via `[[wikilink]]`
- **Sources primaires** citées avec `[[wiki/sources/...]]`
- **Points d'incertitude ou de contradiction** si le wiki en contient

### 5. Proposer d'archiver (étape cruciale)

À la fin de la réponse, proposer à l'utilisateur :

> Cette réponse mérite-t-elle d'être archivée dans `wiki/synthesis/` ?

**Critères pour proposer oui** (sinon ne pas spammer la proposition) :
- La réponse combine ≥ 3 pages wiki et produit un angle nouveau
- La question risque de revenir
- L'utilisateur a formulé une question stratégique (pas "c'est quoi X ?")

**Si l'utilisateur accepte** :
1. Créer `wiki/synthesis/[slug-question].md` avec frontmatter `type: synthesis`
2. Contenu = la réponse + section "Question d'origine" et "Pages sources"
3. Mettre à jour `wiki/synthesis/--index-synthesis.md` via skill `update-index`
4. Appender au log (operation: `query`) via skill `append-log`

### 6. Si le wiki est insuffisant

Si la question n'a pas de réponse satisfaisante dans le wiki :
- Le dire explicitement ("le wiki ne contient rien sur ce sujet")
- Proposer 1–3 sources externes à ingérer (`/analyze ...`)
- Ne **pas** inventer — ne pas répondre avec du savoir général hors wiki sauf si l'utilisateur le demande explicitement

## Règles

- Langue : français
- Toujours citer les pages sources avec `[[wikilink]]`
- Préserver les nuances — si deux sources disent des choses différentes, le dire
- Ne jamais modifier de pages wiki dans ce flux sauf pour l'archivage en `synthesis/` (avec accord explicite)
