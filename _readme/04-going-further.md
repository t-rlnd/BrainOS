# 04 — Aller plus loin

Ton BrainOS tourne. Voici les astuces et outils qui vont démultiplier sa valeur.

---

## Astuces Obsidian qui changent tout

### La graph view

Raccourci : **Cmd/Ctrl + G**.

C'est la vue qui te montre toutes les pages de ton wiki comme une galaxie de points reliés. Au début, 3–4 points isolés. Après 20 sources, une vraie constellation. C'est visuellement satisfaisant, et très utile pour repérer les **pages orphelines** (points isolés sans connexion) et les **pages hubs** (gros points très connectés qui structurent ton savoir).

### L'extension Obsidian Web Clipper

Installer : [obsidian.md/clipper](https://obsidian.md/clipper).

C'est une extension pour ton navigateur (Chrome, Safari, Firefox). Tu tombes sur un bon article → tu cliques sur l'icône → l'article est converti en markdown propre et déposé dans ton vault.

**Configure-le pour déposer dans `raw/`** — comme ça tu dis juste à Claude *"ingère les nouvelles sources dans raw/"* quand tu veux traiter ton buffer.

### Le plugin Dataview

Dans Obsidian → Settings → Community plugins → Browse → rechercher **"Dataview"** → Install → Enable.

Ça permet à tes pages wiki d'afficher des tableaux dynamiques : *"Toutes mes sources sur le sujet X, triées par date"*, *"Toutes les entités de type 'personne' mentionnées plus de 3 fois"*, etc.

Dis à Claude *"ajoute un bloc Dataview sur cette page pour lister toutes les sources liées"* — il saura faire.

### Télécharger les images en local

Dans Obsidian → Settings → Files and links :
- **Attachment folder path** → mettre `raw/resources/`

Puis → Settings → Hotkeys → chercher *"Download"* → assigner un raccourci à **"Download attachments for current file"**.

Résultat : quand tu clippes un article, les images sont téléchargées en local (pas de lien cassé plus tard). Claude peut aussi les lire et les référencer.

---

## Les fichiers que tu n'as jamais à ouvrir

Ton BrainOS contient des fichiers-système que **Claude gère seul**. Tu n'as pas à y toucher :

- `index.md` — le sommaire du wiki. Mis à jour à chaque ingest.
- `log.md` — l'historique chronologique de tout ce qui s'est passé.
- Les fichiers `--index-*.md` dans chaque dossier — sous-sommaires détaillés.
- `memory.md` — les règles apprises en route. Tu peux le lire et demander à Claude d'y ajouter une règle : « Ajoute à memory.md la règle : … »
- Le dossier `.claude/` — contient les commandes, skills et agents personnalisés. N'y touche que si tu sais ce que tu fais.

Tu peux les lire pour ta curiosité. Ne les édite pas à la main.

---

## Faire évoluer ton BrainOS

### Ajouter un domaine

Ta vie change. Tu te mets à la photo, ou tu prends un nouveau rôle pro. Tu peux dire à Claude :

> *"Ajoute 'photographie argentique' à mes domaines dans CLAUDE.md. Je vais commencer à ingérer des sources là-dessus."*

Il mettra à jour `CLAUDE.md` proprement.

### Refaire l'interview

Si ton profil a beaucoup bougé (6 mois plus tard, nouveau projet, pivot pro), dis simplement :

> *"Refais l'interview de configuration depuis le début, j'ai évolué."*

Claude relance le prompt d'interview de l'étape 02 et réécrit ton `CLAUDE.md`.

### Faire évoluer l'arborescence

L'arborescence du template est une base de départ. Tu n'écris pas de contenu ? Supprime `todo/content/`. Tu gères plusieurs produits ? Ajoute `todo/products/`. Un type de page revient souvent dans le wiki ? Crée-lui un sous-dossier. Dis simplement à Claude ce que tu changes : il met à jour la section Architecture du `CLAUDE.md` et les index.

### Créer tes propres commandes

Les commandes `/analyze`, `/brain`, etc. sont définies dans le dossier `.claude/commands/`. Ce sont de simples fichiers markdown. Tu peux en ajouter :

> *"Crée-moi une commande /idea qui prend un sujet et génère 5 angles de contenu pour YouTube."*

Claude créera le fichier.

---

## Versionner ton cerveau avec Git

Ton BrainOS est un simple dossier de fichiers markdown. Si tu l'as cloné depuis GitHub, il est déjà versionné.

Demande à Claude « fais un commit de ma base et pousse-le », ou dans un terminal :
```bash
git add .
git commit -m "Ingests de la semaine"
git push
```

Tu as maintenant un historique complet de l'évolution de ta pensée. Et un backup.

> ⚠️ **Si ton BrainOS contient des infos privées**, garde ton repo en **private** sur GitHub.

---

## Ressources

### Claude Code

- **Doc officielle** : [docs.claude.com/en/docs/claude-code](https://docs.claude.com/en/docs/claude-code)
- **Commandes de base dans Claude** : tape `/help` pour voir toutes les commandes disponibles

### Changer de modèle

Selon ton abonnement, Claude Code peut utiliser plusieurs modèles. Pour les tâches complexes (ingests denses, synthèses croisées, analyse approfondie), choisis le plus puissant ; pour le quotidien, le modèle par défaut suffit.

Dans ta session, tape (ou utilise le sélecteur de modèle de Claude Desktop) :

```
/model
```

Une liste de modèles disponibles s'affiche. Sélectionne celui qui correspond à tes besoins. Pour revenir au modèle par défaut, relance `/model` et sélectionne Sonnet.

> 💡 Garde Sonnet pour les tâches courantes — Opus pour les moments où tu veux vraiment creuser.

**Petit tips : Tu peux taper "/model opusplan" dans Claude dans le Terminal pour débloquer le combo OpusPlan qui utilise Opus pour réfléchir et Sonnet pour exécuter.**

### Obsidian

- **Doc officielle** : [help.obsidian.md](https://help.obsidian.md)
- **Forum** : [forum.obsidian.md](https://forum.obsidian.md) — communauté très active

### L'idée originelle

- **LLM Wiki** d'Andrej Karpathy : [karpathy.bearblog.dev/llm-wiki](https://karpathy.bearblog.dev/llm-wiki/) — lecture fortement recommandée, 10 minutes, ça clarifie l'intention derrière tout le système.

---

## Ton prochain pas

→ **[99-cleanup.md](99-cleanup.md)** — comment nettoyer ce dossier d'onboarding une fois que tout tourne.
