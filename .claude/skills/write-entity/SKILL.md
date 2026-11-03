---
name: write-entity
description: Créer ou mettre à jour une page wiki/entities/ (personne, entreprise, outil) ou wiki/projects/ (projet, client suivi dans le temps) mentionnée dans une source. Utilise cette skill pour chaque entité notable identifiée lors d'un ingest.
---

# write-entity

## Quand l'utiliser

Pour chaque entité **notable** mentionnée dans une source ingérée :
- **Personne** : auteur, expert cité, fondateur, figure du domaine
- **Entreprise** : acteur du marché, concurrent, partenaire
- **Outil** : logiciel, SaaS, framework, API
- **Projet** : projet ou client suivi dans le temps, initiative, produit. **Va dans `wiki/projects/`**, avec `type: project` dans le frontmatter.

**Règle de notabilité** : si l'entité est mentionnée en passant (« comme Google ») sans apport informatif, **ne pas créer de page**. Une page entité = une entité qui mérite d'être suivie dans le temps.

## Structure d'une page entity

```markdown
---
title: "Nom affichable"
type: entity
entity_type: person | company | tool
domain: [domaine principal]
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 1
---

# Nom affichable

> [!info] En une ligne
> Qui / quoi, en une phrase factuelle.

## Description

Paragraphe de 3–6 lignes qui plante le décor : rôle, activité, pertinence pour moi.

## Pertinence pour mes projets

Pourquoi cette entité m'intéresse — à connecter à mes objectifs, stack, domaines.

## Faits clés

- Fait 1 (avec date si pertinent)
- Fait 2
- Fait 3

## Mentions dans le wiki

- [[source-x]] — contexte de la mention
- [[topic-y]]

## Liens externes

- Site : https://...
- Twitter/X : @...
- Autre : ...

## Connexions

- [[entité-liée-1]]
- [[entité-liée-2]]
```

## Cas "mise à jour d'une entité existante"

Si la page existe déjà :
1. **Ne pas écraser** le contenu existant.
2. Ajouter un fait dans "Faits clés" si la source en apporte un nouveau.
3. Ajouter la source dans "Mentions dans le wiki".
4. Incrémenter `sources:` dans le frontmatter.
5. Mettre à jour `updated: YYYY-MM-DD`.
6. Si nouveau lien externe pertinent, l'ajouter.

## Règles de nommage

- **Personnes** : `prenom-nom.md` (ex: `paul-graham.md`)
- **Entreprises** : `slug-court.md` (ex: `webflow.md`, `anthropic.md`)
- **Outils** : `slug-outil.md` (ex: `make-com.md` si ambigu, sinon `make.md`)
- **Projets** : `slug-projet.md`

Pas de préfixe `person-`, `company-`, etc. — le type est dans le frontmatter.

## Règles

- Minimum 150 mots de contenu substantiel.
- Pas de page "placeholder" avec juste un nom et un lien.
- Si tu ne sais rien sur l'entité au-delà du nom, **ne crée pas la page** — attends une seconde source qui apportera du contenu.
- Langue : français pour le contenu, nom propre tel qu'il s'écrit officiellement.

## Ce que tu ne fais PAS

- Tu ne modifies pas `wiki/entities/--index-entities.md` (c'est `update-index`).
- Tu ne crées pas de lien bidirectionnel dans la source ici (c'est `wiki-integrator`).

Retourne la liste des pages créées ou mises à jour avec leur chemin.
