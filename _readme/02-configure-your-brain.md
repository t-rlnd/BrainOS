# 02 — Configure ton cerveau

> L'étape la plus importante. Ton BrainOS doit **te connaître**. Un système générique est inutile — un système qui sait **qui tu es, ce que tu cherches, comment tu penses** devient un vrai multiplicateur.

Plutôt que de te faire remplir des formulaires, on va laisser Claude **t'interviewer pendant une quinzaine de minutes**. Il te posera ses questions une par une, tu répondras naturellement. À la fin, il réécrit ton `CLAUDE.md` et pose les premiers brouillons de `company/` : `now.md`, `offers.md` et `writing-rules.md`.

Le `CLAUDE.md`, c'est le mode d'emploi que Claude lit au début de chaque session pour savoir qui tu es et comment ta base est rangée.

---

## Comment faire, pas à pas

### 1. Dépose quelques documents dans `raw/` (facultatif)

Une proposition type, un brief client, un texte qui te ressemble. Claude y jettera un œil pour poser des questions plus précises. Il ne les analysera pas encore.

### 2. Ouvre une session dans ton BrainOS

Dans la surface choisie à l'étape 01 : onglet Code de Claude Desktop, terminal ou éditeur.

### 3. Colle le prompt d'interview

Copie tout le bloc de la section suivante, colle-le, envoie.

### 4. Laisse-toi interviewer

**Réponds comme à l'oral**, sans chercher à bien formuler. Si tu as une application de dictée, c'est le moment. **Sois concret** : « des PME industrielles de 20 à 100 salariés » vaut mieux que « des PME ». **Dis « je ne sais pas »** quand c'est le cas : Claude le notera comme une question ouverte au lieu d'inventer.

Pour la supervision (question 10), je te conseille le mode impliqué au début : Claude te résume chaque source et te demande l'angle avant d'écrire.

### 5. Valide le récapitulatif, puis relis

Avant d'écrire, Claude te montre ce qu'il a compris. Corrige ce qui est faux, puis dis « c'est bon, écris ». Ensuite, ouvre le `CLAUDE.md` et relis-le ligne par ligne : il sera lu avant chacune de tes sessions. Pour corriger, demande à Claude plutôt que de modifier le fichier toi-même.

---

## Le prompt d'interview

```text
Tu es l'architecte de mon BrainOS. Avant de configurer quoi que ce
soit, tu vas m'interviewer pour comprendre qui je suis et comment je
travaille, puis personnaliser ma base.

CONTEXTE
BrainOS est un second cerveau maintenu par toi. J'apporte les sources
et les questions, tu fais l'extraction, la structuration, les liens et
les synthèses. Le CLAUDE.md actuel est un modèle avec des champs à
remplir. Ton travail : le remplacer par une version qui me ressemble.

AVANT DE COMMENCER
Liste les fichiers de raw/ en une ligne chacun, sans les analyser.
Ils t'aideront à poser des questions précises.

PENDANT L'INTERVIEW
- Une question à la fois. Attends ma réponse avant la suivante.
- Reformule après chaque réponse (« si je résume… »). Je corrige.
- Creuse quand une réponse est vague.
- N'écris rien dans les fichiers avant la fin, sauf si je te le demande.
- Une quinzaine de questions au maximum.

CE QUE TU DOIS APPRENDRE, DANS CET ORDRE
1. Identité : prénom, métier, statut (freelance, salarié, fondateur),
   activité en une phrase.
2. Mon offre : ce que je vends, à qui, à quel prix.
3. Pourquoi BrainOS : ce que je veux accumuler, ce qui m'a manqué
   jusqu'ici, la question que j'aimerais poser à ma base dans six mois.
4. Mes domaines : 2 à 4 territoires précis, avec ce qui m'intéresse
   et ce qui ne m'intéresse pas.
5. Mes outils du quotidien.
6. Mes objectifs à 6-12 mois : 2 ou 3 choses concrètes.
7. Ma façon de travailler avec toi : synthèses courtes ou analyses
   creusées, ton direct ou nuancé, être challengé ou non.
8. Ma façon d'écrire : tutoiement ou vouvoiement, longueur, formules
   que je déteste.
9. Mes interdits : sujets, formulations ou conseils à éviter.
10. Le niveau de supervision : quand tu analyses une source, tu
    discutes d'abord avec moi, ou tu avances sans pause ?

APRÈS L'INTERVIEW
1. Récapitule en 10 à 15 lignes ce que tu as compris. Attends ma
   validation.
2. Réécris CLAUDE.md : remplis « Qui tu es » en 3 à 5 lignes et
   « Comment travailler avec moi », garde intact le reste
   (architecture, opérations, conventions, interdits). Propose-moi une
   ou deux règles spécifiques à mon cas. Moins de 150 lignes.
3. Écris les brouillons de company/now.md, company/offers.md et
   company/writing-rules.md à partir de mes réponses. N'invente rien :
   ce que tu ne sais pas, écris-le comme une question ouverte.
4. Mets à jour company/--index-company.md et ajoute une entrée
   « init » dans log.md.
5. Montre-moi la liste des fichiers écrits.

Commence par te présenter en une phrase, puis pose ta première question.
```

---

## Pourquoi une interview plutôt qu'un formulaire

Si on te donnait un modèle avec des champs à remplir (*"ton domaine principal : ___"*), tu écrirais 3 mots et Claude n'aurait aucun contexte réel.

Une vraie conversation fait ressortir :
- Les nuances de tes domaines (ce qui t'intéresse **précisément**, ce qui ne t'intéresse pas)
- Ton vocabulaire à toi
- Les choses à éviter dans son style de réponse
- Des spécificités que tu n'aurais jamais pensé à écrire si on t'avait demandé

C'est la différence entre un questionnaire RH et une vraie discussion avec quelqu'un qui veut comprendre.

---

## Après l'interview

Ouvre ton `CLAUDE.md` et les fichiers de `company/`. Jette un œil à ce que Claude a écrit. Si une phrase te dérange, modifie-la directement (c'est un simple fichier texte) ou demande à Claude de la réécrire.

**Tu peux refaire l'interview plus tard.** Si ta vie change dans 6 mois (nouveau projet, nouveau métier, nouveaux centres d'intérêt), dis simplement à Claude :

> *"Refais l'interview de configuration, j'ai évolué."*

Il relancera le même processus et mettra à jour ton `CLAUDE.md` et `company/`.

---

## Ton prochain pas

→ **[03-first-ingest.md](03-first-ingest.md)** — ingérer ta première source et poser ta première question.
