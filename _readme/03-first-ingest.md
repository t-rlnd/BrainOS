# 03 — Ta première source, ta première question

Ton cerveau est configuré. Il est vide — c'est normal. On va le nourrir.

---

## 1. Ingère ta première source

Une source, c'est n'importe quoi qui contient du savoir que tu veux garder :
- un article de blog
- une vidéo YouTube (Claude extraira la transcription)
- un PDF
- un transcript d'une réunion ou d'un podcast
- un simple paragraphe que tu colles

Dans Claude, tape simplement :

```
/analyze https://exemple.com/un-article-qui-te-plait
```

Ou, si tu as un fichier sur ton ordinateur :
```
/analyze /chemin/vers/mon-fichier.pdf
```

Ou encore, tu peux coller directement un gros bloc de texte après `/analyze`.

### Ingérer ton dossier `raw/` en un clic

Tu as déposé plusieurs sources dans `raw/` (articles clippés avec Web Clipper, PDF glissés à la main, transcripts de réunion…) ? Tape simplement :

```
/analyze
```

**Sans argument**, la commande traite tout ce qui attend à la racine de `raw/`. Une fois un fichier analysé, Claude range l'original dans `raw/resources/`. Il ne le supprime jamais : c'est ta preuve si une page dit quelque chose de faux. La racine de `raw/` ne contient donc que ce qui reste à analyser.

Quand tu feras confiance à Claude, `/analyze batch` traite tout sans discussion. Je te conseille d'attendre quelques semaines : la discussion est ce qui donne de la valeur à tes pages.

### Ce qui va se passer

1. Claude lit la source
2. Il te présente **la thèse, les 3-5 points clés, et te demande quel angle tu veux retenir**
3. Tu discutes avec lui — tu peux corriger, préciser, lui dire ce qui t'a le plus marqué
4. Il écrit :
   - Une page résumé dans `wiki/sources/` (et une page dans `wiki/meetings/` si c'est une réunion)
   - Met à jour ou crée des pages dans `wiki/topics/` (sujets) et `wiki/concepts/` (idées)
   - Met à jour ou crée les pages `wiki/entities/` (personnes, entreprises, outils) et `wiki/projects/` (clients, projets)
   - Range tes actions dans `todo/`, une ligne datée chacune
   - Met à jour `index.md` (le sommaire du wiki)
   - Ajoute une ligne dans `log.md` (l'historique)

**Une seule source peut toucher 5 à 15 pages.** C'est le but — la connaissance se connecte toute seule.

### Regarde le wiki grandir

Si tu utilises Obsidian, ouvre-le à côté. Tu verras les nouvelles pages apparaître en temps réel. Clique sur les wikilinks (`[[comme-ceci]]`) pour naviguer. Ouvre la **graph view** (icône en haut à gauche dans Obsidian) pour voir les connexions se tisser.

---

## 2. Pose ta première question

Attends d'avoir ingéré 3 ou 4 sources avant de poser des questions — c'est à ce moment-là que la synthèse devient intéressante.

Puis :

```
/brain comment [sujet 1] se connecte-t-il à [sujet 2] dans ce que j'ai lu ?
```

Exemples concrets selon tes domaines :
- *"Quelle est la position de mes sources sur [sujet X] ?"*
- *"Si je devais expliquer [concept] à un débutant, quels points retenir ?"*
- *"Y a-t-il des contradictions entre ce que disent [auteur A] et [auteur B] sur [thème] ?"*
- *"Résume ce que j'ai accumulé cette semaine."*

### Ce qui va se passer

Claude lit `index.md`, ouvre les pages pertinentes, synthétise une réponse **avec les citations des pages wiki** (`[[page]]`). Tu peux cliquer sur chaque citation pour vérifier.

Si la réponse est riche, Claude te proposera de **l'archiver dans `wiki/synthesis/`** — c'est important : tes bonnes réponses doivent devenir des pages, pas disparaître dans l'historique du chat.

---

## 3. Les autres commandes que tu peux essayer

| Commande | À quoi ça sert |
|---|---|
| `/daily` | Crée ta note du jour. Tu y dumps tes pensées en vrac, Claude extrait ce qui mérite d'aller dans le wiki. |
| `/todo` | Range une action datée dans le bon fichier de `todo/`. Sans argument : liste tes actions en attente, les plus anciennes en premier. |
| `/do` | Reprend une action : charge le client, la réunion, l'historique, travaille avec toi, puis propose de la cocher. |
| `/lint` | Audite ton wiki. Cherche les pages oubliées, les contradictions, les concepts mentionnés qui mériteraient leur propre page. Une fois par mois suffit. |

Un transcript de réunion ? Dépose-le dans `raw/` et lance `/analyze` : Claude en fait une page dans `wiki/meetings/`, met à jour la page du client et range tes actions dans `todo/`.

À la fin d'une session où il s'est passé quelque chose, demande : *« Qu'est-ce qui, dans cette session, mérite d'aller dans memory.md, company/, todo/ ou le wiki ? »*

---

## Le rythme qui fonctionne

- **Chaque jour ou presque** : 1 à 3 ingests de sources que tu trouves intéressantes
- **Chaque semaine** : un `/analyze` sur ce qui attend dans `raw/`, un `/todo` pour voir ce qui traîne, une session de `/brain` pour explorer
- **Chaque mois** : un `/lint` pour entretenir
- **Et de temps en temps** : relis les synthèses créées — c'est là que tu vois ta pensée évoluer

Après 3 mois, ton BrainOS contient souvent plus de 100 sources et quelques centaines de pages interconnectées. Les réponses de `/brain` deviennent **plus riches que ce que tu pourrais trouver sur Google** — parce qu'elles sont adossées à des sources que toi tu as choisies, et filtrées par tes questions à toi.

---

## Ton prochain pas

→ **[04-going-further.md](04-going-further.md)** — astuces, plugins Obsidian qui changent la vie, et comment faire évoluer ton BrainOS.
