---
layout: default
title: Plugin FliprPilot - Changelog
lang: fr_FR
pluginId: fliprpilot
---

# Changelog

## v1.1.3 — 2026-06-10
- Amélioration de la résilience de l'API Flipr :
  - Backoff exponentiel sur les erreurs HTTP 429 (3 tentatives : 0s, 10s, 20s)
  - Suppression du double appel token à chaque heure (cause principale des 429 répétitifs)
  - Cache de la dernière valeur connue de `FiltrationTime` : plus de cible de filtration oscillante en cas d'indisponibilité API
- Réduction du bruit dans les logs : suppression des lignes rédundantes « PAC → aucune action » et « Filtration → maintien »

## v1.1.2 — 2026-06-08
- Suppression de la possibilité de cliquer sur les métriques info (desktop et mobile) : les métriques ne sont plus interactives, seuls les boutons d'action restent cliquables

## v1.1.1 — 2026-06-08
- Correction de l'affichage de la **tuile mobile** : la barre de statut s'affiche désormais en **2 colonnes** sur tous les appareils mobiles (Filtration/PAC à gauche, Batterie/Plage à droite)

## v1.1.0 — 2026-06-06
- Ajout d'une **tuile dashboard** personnalisée (desktop) : affichage complet des mesures, état filtration/PAC, barre de progression journalière et boutons d'action directement depuis **Accueil > Dashboard**
- Ajout d'une **tuile mobile** optimisée : version compacte et tactile, grille 2×2 des métriques, boutons large format adaptés aux smartphones
- Masquage automatique des commandes individuelles sur la tuile au profit du widget personnalisé
- Commande `Tuile dashboard` créée automatiquement à la sauvegarde de l'équipement

## v1.0.0 — 2026-06-04
- Version initiale
