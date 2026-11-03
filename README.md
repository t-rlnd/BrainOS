# BrainOS

> **Un Second Brain vivant, maintenu par Claude.**
> Tu apportes les sources et les questions. Claude fait le reste.

BrainOS est un template clonable pour construire ta propre base de connaissances personnelle — un wiki qui grandit, se structure et se connecte tout seul au fil de ce que tu lis. Tu n'écris plus de notes. Tu ingères des sources, tu poses des questions, et Claude s'occupe du reste.

Inspiré du pattern *[LLM Wiki](https://karpathy.bearblog.dev/llm-wiki/)* d'Andrej Karpathy.

---

## Le problème

Prendre des notes, c'est fastidieux. Les ranger, c'est pire. Et après 6 mois, personne ne retrouve rien.

La plupart des systèmes de notes échouent pour la même raison : **le coût de maintenance dépasse la valeur perçue**. On arrête de relier, de mettre à jour, de classer. Le vault devient un cimetière de markdown.

Les outils comme ChatGPT avec upload de fichiers ou NotebookLM règlent une partie du problème (tu retrouves l'info), mais ils redécouvrent ta connaissance **à chaque question**. Rien ne s'accumule. Rien ne se structure.

## L'idée de BrainOS

Au lieu d'interroger des sources brutes à chaque fois, **Claude maintient un wiki persistant entre toi et tes sources**. Quand tu ajoutes une nouvelle source, Claude ne l'indexe pas — il la lit, en extrait les idées clés, et les **intègre dans le wiki existant** :

- Met à jour les pages entités concernées
- Révise les synthèses en cours
- Signale les contradictions avec ce que tu as déjà lu
- Renforce ou challenge les connexions

La connaissance est **compilée une fois** puis tenue à jour. Pas re-dérivée à chaque requête.

Après quelques semaines, ton wiki devient plus riche que ta propre mémoire sur les sujets que tu explores. Chaque nouvelle source enrichit 5 à 15 pages. Les connexions se font toutes seules. **Le wiki compound dans le temps.**

## Comment ça marche

BrainOS est un simple dossier de fichiers Markdown. Claude y travaille directement : il lit tes fichiers, en crée, les relie. Tu n'es enfermé dans aucune application. Le même dossier s'ouvre dans :

| Surface | Pour qui |
|---|---|
| **Claude Desktop, onglet Code** | Tout le monde. Aucun terminal. C'est le chemin conseillé pour démarrer. |
| **Le terminal** (`claude`) | Ceux qui aiment la ligne de commande, les tâches longues, l'automatisation |
| **Un éditeur** (VS Code, Cursor, JetBrains) avec l'extension Claude Code | Ceux qui codent déjà |
| **claude.ai/code**, dans le navigateur | Ceux qui ont mis leur base sur GitHub |

Toutes ces surfaces lisent le même `CLAUDE.md` et proposent les mêmes commandes. Tu peux commencer dans l'une et passer à une autre sans rien changer au dossier. [Obsidian](https://obsidian.md) est recommandé pour lire ton wiki et voir le graphe des liens, mais facultatif.

Les commandes :

| Commande | Ce qui se passe |
|---|---|
| `/analyze [source]` | Claude lit une URL, un PDF, un transcript ou ce qui attend dans `raw/`, discute de l'angle avec toi, puis écrit 5 à 15 pages dans le wiki |
| `/brain [question]` | Claude répond à partir de ton wiki, en citant tes propres pages |
| `/lint` | Claude audite le wiki : pages orphelines, contradictions, concepts sans page, pages périmées |
| `/todo [action]` | Claude range une action datée dans le bon fichier de `todo/` |
| `/do [sujet]` | Claude reprend une action avec tout son contexte, puis propose de la cocher |
| `/daily` | Facultatif : ta note du jour, et ce qui mérite d'aller ailleurs |

Tu peux créer tes propres commandes : ce sont de simples fichiers dans `.claude/commands/`.

## Démarrage

**[Commence par le dossier `_readme/`](_readme/00-start-here.md)** : 5 étapes dans l'ordre, environ 45 minutes pour tout installer, configurer ta base et faire ta première analyse.

| Étape | Fichier | Durée |
|---|---|---|
| 00 | [Commence ici](_readme/00-start-here.md) | 5 min |
| 01 | [Installation](_readme/01-installation.md) | 10–20 min |
| 02 | [Configure ton cerveau](_readme/02-configure-your-brain.md) | 15–20 min |
| 03 | [Première source, première question](_readme/03-first-ingest.md) | 10 min |
| 04 | [Aller plus loin](_readme/04-going-further.md) | lecture libre |
| 99 | [Nettoyage](_readme/99-cleanup.md) | 1 min |

> Tu veux être accompagné ? Le workshop **W01 · Ton second cerveau** de l'[Académie initWeb](https://initweb.fr) construit ce BrainOS pas à pas, avec vidéos, prompts et une base de démonstration.

## Prérequis

- **Un abonnement Claude Pro ou Max.** Claude Code, qui travaille dans ton dossier, n'est pas inclus dans le plan gratuit. Et analyser tes sources demande du volume.
- **Une surface Claude Code** : [Claude Desktop](https://claude.ai/download) suffit.
- **[Obsidian](https://obsidian.md)**, facultatif, gratuit, pour lire et naviguer dans le wiki.

Tout est détaillé dans [01-installation.md](_readme/01-installation.md).

## Structure du projet

```
BrainOS/
├── CLAUDE.md           → Le schéma : lu en premier à chaque session
├── memory.md           → Les règles apprises en route
├── index.md            → La carte (pointe vers un --index- par dossier)
├── log.md              → Le journal des opérations
│
├── company/            → Ton activité : now, offers, metrics, writing-rules
├── todo/               → Tes actions datées : business, clients, content
│
├── raw/                → Dépose ta matière brute ici (jamais modifiée)
│   └── resources/      → Originaux déjà analysés, images
├── wiki/               → Savoir compilé : Claude écrit, tu lis
│   ├── sources/        → Une page par source
│   ├── meetings/       → Une page par réunion
│   ├── entities/       → Personnes, entreprises, outils
│   ├── projects/       → Projets et clients suivis dans le temps
│   ├── topics/         → Connaissance par domaine
│   ├── concepts/       → Modèles mentaux, frameworks, idées
│   ├── decisions/      → Décisions importantes et leur contexte
│   └── synthesis/      → Analyses croisées, réponses archivées
│
├── daily/              → (optionnel) notes du jour
├── outputs/            → Livrables : drafts, analyses, exports
├── .claude/            → Commandes, skills et agents
└── _readme/            → Guide de démarrage (à supprimer après)
```

Les dossiers sont en anglais, sans accent : c'est ce qui évite les erreurs de chemin. Tes fichiers, eux, peuvent rester en français. Chaque dossier a son `--index-<dossier>.md`.

Cette arborescence est une base de départ, pas un cadre figé. Renomme, ajoute ou supprime des sous-dossiers selon ton quotidien. Demande simplement à Claude de mettre à jour le `CLAUDE.md` et les index.

## À qui c'est destiné

BrainOS est utile pour n'importe qui accumule de la connaissance sur un sujet dans le temps :

- **Un indépendant ou fondateur** qui veut structurer sa veille métier
- **Un chercheur ou étudiant** qui creuse un sujet sur plusieurs mois
- **Un créateur de contenu** qui capitalise sur ses lectures et interviews
- **Une équipe** qui veut un wiki interne maintenu par un LLM, alimenté par Slack, transcripts, docs
- **Tout curieux** qui en a marre d'oublier 80 % de ce qu'il lit

Pas besoin d'être développeur. Le template est conçu pour être utilisé dès l'installation, sans écrire une ligne de code.

## Philosophie

> Le travail fastidieux d'une base de connaissances, ce n'est pas la lecture ou la réflexion — c'est le **bookkeeping**. Mettre à jour les cross-références, maintenir les résumés, signaler les contradictions, garder la cohérence entre des dizaines de pages. Les humains abandonnent les wikis parce que la maintenance grandit plus vite que la valeur. Les LLM ne s'ennuient pas, n'oublient pas, et peuvent toucher 15 fichiers d'un coup.
>
> *— Andrej Karpathy, [LLM Wiki](https://karpathy.bearblog.dev/llm-wiki/)*

Ton rôle : sourcer, explorer, poser les bonnes questions, décider ce que ça veut dire.
Le rôle de Claude : tout le reste.

## Contribution

Fork libre, adapte à ton usage, partage tes améliorations. Les issues et pull requests sont les bienvenues.

## Licence

MIT. Utilise comme tu veux.

## Crédits

- Pattern originel : [Andrej Karpathy](https://karpathy.bearblog.dev/llm-wiki/)
- Template maintenu par [Théo Roland](https://initweb.fr) — [initWeb](https://initweb.fr) / STUDIO ROLAND

---

*Si BrainOS t'aide, laisse une star sur le repo. Ça m'aide à savoir si ça sert à autre chose que mon propre cerveau.*
