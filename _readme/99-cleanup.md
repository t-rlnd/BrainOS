# 99 — Nettoyage

Ton BrainOS est configuré, tes premières sources sont ingérées, tu as pris tes marques.

**Ce dossier `_readme/` ne te sert plus.** Il encombre ton vault Obsidian et il est devenu redondant avec ton vrai `CLAUDE.md` personnalisé.

---

## Quand supprimer ce dossier

Coche mentalement :

- [ ] J'ai fait l'interview de configuration et mon `CLAUDE.md` reflète vraiment qui je suis
- [ ] J'ai ingéré au moins 3 sources avec `/analyze` et je vois le wiki grandir
- [ ] J'ai posé au moins une question avec `/brain` et j'ai eu une réponse satisfaisante
- [ ] Je sais où retrouver les ressources externes (Karpathy, doc Claude Code, doc Obsidian) si j'en ai besoin

Si les 4 sont cochés → tu peux supprimer.

---

## Comment supprimer

### Option 1 — Dans Obsidian (le plus simple)

1. Dans la barre latérale gauche, clic droit sur le dossier `_readme`
2. Choisis **"Delete"**
3. Valide

### Option 2 — En demandant à Claude

Dans ta session :
> *« Supprime le dossier _readme/ et retire les mentions qui y renvoient dans CLAUDE.md et index.md, s'il y en a. Note l'opération dans log.md. »*

Claude te demandera la permission avant de supprimer.

### Option 3 — En ligne de commande

Depuis ton dossier BrainOS :
```bash
rm -rf _readme/
```

### Commit Git (optionnel)

Si tu versionnes avec Git :
```bash
git add -A
git commit -m "Cleanup: suppression du dossier d'onboarding"
```

---

## Tu veux garder une trace ?

Si tu préfères ne rien supprimer, tu peux simplement **renommer** le dossier `_readme/` en `_archive-onboarding/`. Le préfixe `_` le range en bas de l'arborescence d'Obsidian, hors de ton chemin quotidien.

---

## Et après ?

Tu n'as plus besoin de ce guide. Tu es entré dans le **mode normal** de BrainOS :

- Nouvelle source intéressante → `/analyze`
- Question en tête → `/brain`
- Chose à faire → `/todo`, puis `/do` le moment venu
- Réflexion à structurer → `/daily` (facultatif)
- Entretien mensuel → `/lint`

Bienvenue dans ton Second Brain. Plus tu l'utilises, plus il te rend de service.

---

*Si tu veux contribuer au template, signaler un bug, ou suggérer une amélioration : le repo GitHub est ton point de contact.*
