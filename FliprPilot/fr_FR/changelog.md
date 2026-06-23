---
layout: default
title: Plugin FliprPilot - Changelog
lang: fr_FR
pluginId: fliprpilot
---

# Changelog

## v1.2.1 — 2026-06-23
- Ajout des champs de configuration **« Cible refroidissement jour »** et **« Cible refroidissement nuit »** dans l'onglet Automatisation (étaient absents de l'interface malgré leur présence dans le code)

## v1.2.0 — 2026-06-22
- Ajout du **mode refroidissement PAC** pour les journées de forte chaleur :
  - Nouvelle commande action **« PAC mode froid »** : bascule la logique de régulation en mode refroidissement (à utiliser après avoir changé manuellement le mode sur la PAC physique)
  - Nouvelle commande action **« PAC mode chauffe »** : retour au mode chauffage
  - Nouvelle commande info **« Mode PAC »** : affiche le mode actif (`chauffe` ou `froid`)
  - Logique hysterèse inversée en mode froid — PAC ON quand T°eau > cible + hysterèse, OFF quand T°eau ≤ cible − hysterèse
  - Cibles de température dédiées au refroidissement : `temp_cible_froid_jour` et `temp_cible_froid_nuit` (défaut 28°C), indépendantes des cibles de chauffage

## v1.1.5 — 2026-06-22
- Cache batterie/tension : quand `AnalysR/settings` est indisponible (timeout), la dernière valeur connue est restituée au lieu d'afficher 0%/0V
- Résilience token syncFlipr : si le refresh forcé du token échoue (timeout ou 429 épuisé), le token existant est réutilisé s'il est encore valide — empêche la cascade « syncFlipr timeout → syncAlert 429 » 30 min plus tard

## v1.1.4 — 2026-06-11
- Élimination des erreurs HTTP 429 sur `syncAlert` (toutes les 30 min) :
  - `syncFlipr` renouvelle systématiquement le token à chaque cycle horaire et étend sa durée de vie à 65 min
  - `syncAlert` réutilise désormais le token en cache (âgé de ~30 min) sans jamais rappeler `/oauth2/token` → 1 appel token/heure au lieu de 2
- Suppression du log « PAC → aucune action » en plage nocturne (était émis toutes les 5 min, soit ~108 lignes par nuit)

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
