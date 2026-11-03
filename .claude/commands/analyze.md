---
description: Ingérer une source (URL, fichier local, chemin raw/) dans le wiki BrainOS
argument-hint: [URL | chemin fichier | "batch"]
---

# /analyze — Ingest d'une source dans BrainOS

**Source à ingérer** : $ARGUMENTS

## Flux à exécuter

### 1. Session loading (si pas déjà fait dans cette session)

Lire dans cet ordre :
- `index.md`
- Les 10 dernières opérations : `grep "^## \[" log.md | head -10`

### 2. Résolution de la source

- Si `$ARGUMENTS` vaut `batch` → mode batch (voir étape 4), puis scanner `raw/` comme ci-dessous. Si `batch` est suivi d'une source, traiter cette source en mode batch.
- Sinon, si `$ARGUMENTS` est non vide → utiliser cette valeur comme source.
- Si `$ARGUMENTS` est vide → scanner **la racine** de `raw/` (hors `raw/resources/` et `.gitkeep`). Ce qui est à la racine attend d'être analysé ; ce qui est dans `raw/resources/` l'a déjà été.
  - Si plusieurs fichiers attendent, les lister à l'utilisateur et ingérer chacun en séquence.
  - Si rien n'attend, informer l'utilisateur qu'il n'y a rien à ingérer.

### 3. Extraction

Invoquer l'agent `source-extractor` avec la source.
Récupérer son rapport (métadonnées + contenu + points clés + entités).

### 4. Discussion (mode impliqué — par défaut)

**Par défaut, parler à l'utilisateur avant d'écrire quoi que ce soit** :
- Résumer la thèse en 2–3 phrases
- Proposer 3–5 points clés candidats
- Proposer un angle personnel ("ce qu'on en retient")
- Demander : accord ? ajouts ? angle différent ?

**Mode batch** : si l'utilisateur a passé `batch` en argument ou demande explicitement "pas de discussion", sauter cette étape et exécuter directement la suite avec un angle neutre.

### 5. Écriture de la page source

Utiliser la skill `write-source` pour créer `wiki/sources/[slug].md` à partir du rapport d'extraction + décisions de la discussion.

**Si la source est une réunion** (transcript, compte rendu, notes d'appel) : créer aussi `wiki/meetings/YYYY-MM-DD-sujet.md` avec participants, décisions, actions et un lien vers la page source. Mettre à jour la page du client ou du projet concerné (`wiki/entities/` ou `wiki/projects/`) avec les décisions prises.

### 6. Intégration wiki

Invoquer l'agent `wiki-integrator` avec le chemin de la page source.
Il crée/enrichit les pages `topics/` et `concepts/` pertinentes, pose les liens bidirectionnels.

### 7. Entités et projets

Pour chaque entité notable identifiée à l'étape 3, utiliser la skill `write-entity` (création ou mise à jour). Un client ou un projet suivi dans le temps va dans `wiki/projects/`.

### 7 bis. Actions

Si la source contient des actions qui reviennent à l'utilisateur (surtout une réunion), les ranger dans le bon fichier de `todo/`, une ligne chacune, avec la date du jour et un lien vers la réunion ou la source :
`- [ ] YYYY-MM-DD · action · [[wiki/meetings/YYYY-MM-DD-sujet]]`
Vérifier les doublons avant d'ajouter. Les montrer à l'utilisateur dans le récap.

### 8. Mise à jour des index

Utiliser la skill `update-index` pour :
- Ajouter la ligne dans les `--index-*.md` des dossiers touchés
- Mettre à jour les compteurs de `index.md`

### 9. Log

Utiliser la skill `append-log` avec `operation: ingest` (ou `meeting` pour une réunion) et un titre court évoquant la source.

### 10. Ranger l'original

Si la source provenait de la racine de `raw/`, déplacer le fichier dans `raw/resources/`, sans le renommer ni le modifier. Ne jamais le supprimer : c'est l'original, la preuve si une page dit quelque chose de faux. Mettre à jour le lien `source_url` de la page source si besoin.

## Règles

- **Une source peut toucher 5 à 15 pages wiki**, c'est normal et attendu.
- Ne jamais créer de page vide (min. 150 mots pour entités/concepts/topics, 300 pour sources).
- Toujours vérifier `index.md` avant création pour éviter les doublons.
- Respecter strictement les conventions de nommage et frontmatter définies dans `CLAUDE.md`.
- À la fin, retourner un récap court : pages créées, pages mises à jour, actions ajoutées à `todo/`, prochaines pistes d'ingest éventuelles.
