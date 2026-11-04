# BrainOS — Schéma

BrainOS est un second cerveau maintenu par Claude. J'apporte les sources et les questions. Tu fais l'extraction, la structuration, les liens et les synthèses.

> Ce fichier est un modèle. La section « Qui tu es » et la section « Comment travailler avec moi » se remplissent pendant l'interview de configuration (`_readme/02-configure-your-brain.md`). Le reste est le socle : garde-le tel quel.

## Qui tu es

[TON PRÉNOM ET NOM], [TON MÉTIER ET TON STATUT].
[TON ACTIVITÉ EN UNE PHRASE : CE QUE TU FAIS, POUR QUI, COMMENT.]
Domaines principaux : [DOMAINE 1], [DOMAINE 2], [DOMAINE 3].
Détail : `company/now.md` et `company/offers.md`.

---

## Architecture

```
BrainOS/
├── CLAUDE.md           → Ce fichier, lu en premier
├── memory.md           → Règles et corrections apprises en route
├── index.md            → Hub de navigation (pointe vers les --index-*)
├── log.md              → Journal des opérations (append only)
│
├── company/            → Mon activité : now, offers, metrics, writing-rules
├── todo/               → Mes actions, une ligne datée chacune
│   ├── business/       → Relances, devis, administratif
│   ├── clients/        → Ce que je dois aux clients, ce que j'attends d'eux
│   └── content/        → Idées de posts, d'articles, de vidéos
│
├── raw/                → Drop zone : la matière brute, jamais modifiée
│   └── resources/      → Originaux déjà analysés, images
├── wiki/               → Savoir compilé : tu écris, je lis
│   ├── sources/        → Une page par source analysée
│   ├── meetings/       → Une page par réunion (transcript, compte rendu)
│   ├── entities/       → Personnes, entreprises, outils
│   ├── projects/       → Projets et clients suivis dans le temps
│   ├── topics/         → Connaissance par domaine
│   ├── concepts/       → Modèles mentaux, frameworks, idées
│   ├── decisions/      → Décisions importantes et leur contexte
│   └── synthesis/      → Analyses croisées, réponses archivées
│
├── daily/              → (optionnel) notes du jour, via /daily
├── outputs/            → Livrables : drafts/, analyses/, exports/
└── .claude/            → commands/, skills/, agents/
```

Chaque dossier a son `--index-<dossier>.md`. Cette arborescence est une base de départ : si je la change, mets à jour cette section et les index.

---

## Au démarrage de chaque session

1. Lis `index.md`.
2. Lis les 10 dernières entrées de `log.md` : `grep "^## \[" log.md | head -10`.
3. Lis `memory.md` et `company/now.md`.
4. Si ma demande est une tâche précise, lis le fichier de `todo/` concerné. Si elle concerne un client ou un sujet, ouvre sa page dans `wiki/` avant de répondre.
5. Si la racine de `raw/` contient des fichiers pas encore analysés, signale-le-moi en une ligne.

---

## Comment travailler avec moi

- [À REMPLIR PENDANT L'INTERVIEW : tutoiement, ton, longueur des réponses, être challengé ou non…]
- Si une information manque dans la base, dis-le au lieu de l'inventer.
- Cite la page d'où vient une information : `[[page]]`.
- Mon style d'écriture est dans `company/writing-rules.md`.

---

## Opérations

| Commande | Ce qu'elle fait |
|---|---|
| `/analyze [source]` | Analyse une source (URL, fichier, `raw/`) et l'intègre au wiki. Sans argument : tout ce qui attend à la racine de `raw/` |
| `/brain [question]` | Répond à partir du wiki, avec citations, et propose d'archiver dans `synthesis/` |
| `/lint` | Audite le wiki : orphelines, concepts fantômes, contradictions, pages périmées |
| `/daily [texte]` | Crée ou complète la note du jour et propose ce qui mérite d'aller ailleurs |
| `/todo [action]` | Range une action datée dans le bon fichier de `todo/` |
| `/do [sujet]` | Reprend une action de `todo/` avec son contexte, puis propose de la cocher |

### Ingest (`/analyze`)

1. Extraire le contenu (agent `source-extractor`).
2. Mode impliqué par défaut : discuter avec moi (thèse, points clés, angle) avant d'écrire. Mode batch (`/analyze batch`) : sans pause.
3. Écrire la page `wiki/sources/` (skill `write-source`). Si c'est une réunion : une page `wiki/meetings/` en plus.
4. Toucher les pages `topics/` et `concepts/` (agent `wiki-integrator`), puis `entities/` et `projects/` (skill `write-entity`).
5. Ranger mes actions dans `todo/` (une ligne datée, lien vers la source ou la réunion).
6. Mettre à jour les index (skill `update-index`) et `log.md` (skill `append-log`).
7. Ranger l'original dans `raw/resources/`. Ne jamais le supprimer.

Une source touche souvent 5 à 15 pages. C'est normal.

---

## Conventions

### Langue et format
- Français, sauf termes techniques.
- Markdown Obsidian : wikilinks `[[page]]`, callouts `> [!note]`, frontmatter YAML.

### Nommage
- Dossiers en anglais, sans accent ni apostrophe. Fichiers en français.
- kebab-case, minuscules, 2 à 4 mots, sans préfixe redondant avec le dossier.
- Réunions : `wiki/meetings/YYYY-MM-DD-sujet.md`.

### Frontmatter des pages wiki

```yaml
---
title: "Titre lisible"
type: source | meeting | entity | project | topic | concept | decision | synthesis
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 1
---
```

Pour `entity`, ajouter `entity_type: person | company | tool`. Pour `source`, ajouter `source_url: ""` et `source_author: ""`.

### Todo
Une action par ligne, avec sa date d'ajout et sa case. Pas d'échéance obligatoire.

```
- [ ] 2026-11-04 · Relancer Maison Verdier sur la proposition · [[maison-verdier]]
- [x] 2026-11-02 · Envoyer le devis à Atelier Nord · [[atelier-nord]]
```

Ne jamais cocher une action sans mon accord. Ne jamais supprimer une ligne : une action abandonnée est barrée (`~~…~~`).

### Liens
- Si A cite B, B cite A.
- Au plus 5 wikilinks dans le texte, les autres dans une section « Connexions » en bas.

### Index
`index.md` pointe vers les `--index-*.md`, pas vers les pages. Chaque `--index-*.md` a une ligne par page :
```
| [[slug-page]] | description en une ligne | YYYY-MM-DD |
```

### Log
En-tête d'une entrée de `log.md`, la plus récente en haut :
```
## [YYYY-MM-DD] <operation> | <titre>
```
Opérations : `init` · `ingest` · `meeting` · `query` · `lint` · `daily` · `todo` · `export` · `config`

---

## Sauvegarde

Ne s'applique que si ma base est dans un dépôt Git relié à mon dépôt GitHub privé.

- Lire ma base ne demande rien : pas de question, pas de sauvegarde.
- Dès que tu as créé ou modifié des fichiers de ma base, termine ta réponse par la question : « Je sauvegarde dans BrainOS ? »
- Si je réponds oui : vérifie qu'aucun fichier modifié ne contient de donnée sensible (voir Interdits), puis fais un commit avec un message court qui résume les changements, et un push vers mon dépôt GitHub privé.
- Si je réponds non, ne repose la question qu'à la prochaine modification.
- Ne pousse jamais vers le dépôt public du template t-rlnd/BrainOS.

---

## Permissions

| Zone | Lire | Écrire | Notes |
|---|---|---|---|
| `company/` | ✅ | ✅ avec mon accord | Je valide chaque modification |
| `todo/` | ✅ | ✅ | Ajouter, cocher avec mon accord, jamais supprimer |
| `raw/` | ✅ | déplacer vers `raw/resources/` | Ne jamais modifier ni supprimer |
| `wiki/` | ✅ | ✅ | Enrichissement continu |
| `daily/` | ✅ | ✅ via /daily | Ne jamais modifier une note passée |
| `outputs/` | ✅ | ✅ | Livrables sur demande |
| `index.md`, `--index-*` | ✅ | ✅ | À chaque création de page |
| `log.md` | ✅ | append only | Ne jamais modifier une entrée |
| `.obsidian/` | ❌ | ❌ | Jamais |

---

## Interdits

- Ne jamais modifier ni supprimer un fichier de `raw/`.
- Ne jamais modifier une entrée existante de `log.md`.
- Ne jamais créer de doublon : vérifier l'index avant toute création.
- Ne jamais créer une page vide.
- Ne jamais écrire de mot de passe, de donnée bancaire, de numéro d'identité, d'adresse personnelle ni d'information de santé.
- Ne jamais modifier `.obsidian/`.
- Ne rien supprimer sans me demander.

---

## Self-improvement

Après toute correction de comportement :
1. Identifier la règle générale derrière la correction.
2. L'ajouter à `memory.md` (titre, date, règle, pourquoi).
3. Si elle devient permanente et générale, la remonter dans ce fichier.
