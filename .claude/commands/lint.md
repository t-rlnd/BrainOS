---
description: Auditer le wiki BrainOS (pages orphelines, concepts fantômes, contradictions, périmé)
---

# /lint — Audit du wiki

## Flux à exécuter

### 1. Session loading (si pas déjà fait)

- Lire `index.md`
- `grep "^## \[" log.md | head -10`

### 2. Invoquer l'auditeur

Invoquer l'agent `wiki-auditor`. Il parcourt `wiki/` et produit un rapport structuré en priorités (🔴 / 🟡 / 🟢).

### 3. Présentation du rapport

Afficher le rapport tel que produit par l'agent, sans reformulation agressive.

### 4. Proposer des actions

À la fin, proposer à l'utilisateur de traiter **1 à 3 points de priorité haute** tout de suite :
- Créer la page d'un concept fantôme
- Ajouter un wikilink manquant évident
- Actualiser une source périmée (déclenche un nouveau `/analyze`)

**Ne rien corriger automatiquement** — l'utilisateur décide quoi attaquer.

### 5. Log

Utiliser la skill `append-log` avec `operation: lint` et un titre résumant le volume du rapport (ex: `lint · 3 orphelines, 2 concepts fantômes`).

## Règles

- Rapport > 50 items = probablement trop bruyant, resserrer les critères.
- Ne pas lancer `/lint` plus d'une fois par semaine dans une même phase de travail (pas de valeur ajoutée).
- L'agent ne modifie rien — c'est un audit read-only.
