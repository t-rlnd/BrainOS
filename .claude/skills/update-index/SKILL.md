---
name: update-index
description: Mettre à jour index.md (hub global) et les fichiers --index-*.md des dossiers touchés après création ou modification de pages wiki. À utiliser à la fin de chaque ingest.
---

# update-index

## Quand l'utiliser

À la fin de chaque opération qui crée ou modifie des pages wiki :
- Ingest (`/analyze`)
- Création manuelle de synthèse ou décision
- Mise à jour substantielle d'une page

## Double structure d'index

BrainOS utilise **deux niveaux d'index** :

1. **`index.md`** (racine) = **hub de navigation**. Pointe vers les `--index-*.md` par dossier. Compteurs globaux.
2. **`[dossier]/--index-[dossier].md`** = **catalogue détaillé** du dossier avec une ligne par page. Dossiers concernés : `company/`, `todo/`, chaque sous-dossier de `wiki/` (sources, meetings, entities, projects, topics, concepts, decisions, synthesis), `outputs/*`, `daily/`.

## Mise à jour d'un `--index-*.md`

Format d'une ligne :
```
| [[slug-page]] | description une ligne | YYYY-MM-DD |
```

Règles :
- Ajouter la nouvelle page dans l'ordre approprié (alphabétique ou chronologique — respecter ce qui existe).
- Description = une phrase courte qui résume l'apport de la page, pas un titre.
- Si la page existe déjà dans l'index, **mettre à jour la date et éventuellement la description**.
- Ne jamais dupliquer une ligne.

Structure attendue d'un `--index-*.md` :
```markdown
# [Dossier] — Index détaillé

> Catalogue des pages de `wiki/[dossier]/`. Maintenu à chaque ingest.

| Page | Description | Mis à jour |
|---|---|---|
| [[slug-1]] | ... | YYYY-MM-DD |
| [[slug-2]] | ... | YYYY-MM-DD |
```

## Mise à jour de `index.md`

À la fin d'un ingest, vérifier et mettre à jour dans `index.md` :

1. **Compteur de sources** : ligne `## Sources — N ingérées`
2. **Compteurs par domaine** dans le tableau sources
3. **Compteur topics / concepts / entities** : `## Topics — N pages`
4. **Ligne de synthèse en bas** : `*Pages wiki : N · Sources : N · Dernière mise à jour : YYYY-MM-DD*`
5. Si pertinent, ajouter une entrée dans le tableau "Navigation rapide" pour les sujets fréquemment consultés.

## Algorithme

1. Lire `index.md` et les `--index-*.md` concernés.
2. Compter les fichiers réels dans chaque dossier via `Glob` (`wiki/sources/*.md` en excluant `--index-*.md`).
3. Pour chaque page créée ou modifiée :
   - Ajouter/actualiser la ligne dans le `--index-*.md` du dossier.
4. Mettre à jour les compteurs dans `index.md`.
5. Mettre à jour la ligne de synthèse finale avec date du jour.

## Règles

- **Ne jamais inventer** une page dans un index — vérifier qu'elle existe sur disque.
- **Ne jamais retirer** une ligne d'index sans demande explicite (la page a pu être renommée, pas supprimée).
- Conserver l'ordre existant dans les `--index-*.md` (alphabétique par défaut).
- Ne pas modifier la structure de `index.md` sans raison — juste les compteurs et les lignes de nav.

## Ce que tu ne fais PAS

- Tu ne modifies pas les pages wiki elles-mêmes.
- Tu ne touches pas à `log.md`.
- Tu ne crées pas de nouveau `--index-*.md` sans que le dossier existe.
