---
description: Ajouter une action datée dans le bon fichier de todo/
argument-hint: [action en langage naturel]
---

# /todo — Ajouter une action

**Action** : $ARGUMENTS

## Flux à exécuter

### 1. Lire la todo

- Lire `todo/--index-todo.md` pour connaître les fichiers disponibles.
- Si `$ARGUMENTS` est vide : lister les actions non cochées de tous les fichiers, les plus anciennes en premier, et signaler celles qui ont plus de deux semaines. Ne rien modifier. Fin.

### 2. Router l'action

Choisir le fichier de `todo/` qui correspond au sujet :
- `todo/business/actions.md` : relances, devis, administratif, prospection ;
- `todo/clients/suivi.md` : ce que l'utilisateur doit à un client ou attend de lui ;
- `todo/content/idees.md` : idées de posts, d'articles, de vidéos.

Si l'utilisateur a renommé ou ajouté des fichiers, suivre `--index-todo.md`. En cas de doute, demander.

### 3. Vérifier les doublons

Chercher une action proche dans tous les fichiers de `todo/` (`Grep` sur les mots-clés). Si elle existe et n'est pas cochée, le dire et ne rien ajouter.

### 4. Écrire la ligne

Ajouter une ligne dans la section pertinente (sinon « Ajouts rapides ») :

```
- [ ] YYYY-MM-DD · action reformulée en une phrase, verbe à l'infinitif · [[page-liée]]
```

- Date = date du jour (date d'ajout). Pas d'échéance, sauf si l'utilisateur en donne une : l'ajouter alors en fin de ligne (`· avant le YYYY-MM-DD`).
- Lien = la page du client, du projet ou de la réunion concernée, si elle existe dans le wiki.

### 5. Index et log

- Mettre à jour la date du fichier dans `todo/--index-todo.md`.
- Skill `append-log` avec `operation: todo` et un titre court.

## Règles

- Une action par ligne. Plusieurs actions dans la demande → plusieurs lignes.
- Ne jamais cocher ni supprimer une action ici.
- Confirmer en une ligne : fichier choisi et ligne ajoutée.
