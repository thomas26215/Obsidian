# 🎯 Radar Chart Musculaire

#liftconnect #ia #feature #ui

status: 🟡 À faire
priorité: haute
lié à: [[Analyse IA d'un programme]]

## Concept
Graphique radar affiché dans l'analyse IA pour visualiser la couverture musculaire
d'un programme en un coup d'œil.

## Axes du radar (groupes musculaires)
- Pectoraux (haut / bas)
- Épaules (avant / latéral / arrière)
- Dos (grand dorsal / trapèzes / rhomboïdes)
- Biceps / Triceps
- Abdominaux / Lombaires
- Quadriceps / Ischio-jambiers / Fessiers
- Mollets

## Affichage
- Radar actuel du programme (couleur principale LiftConnect)
- Radar "idéal de référence" en superposition (couleur secondaire transparente)
- L'écart visuel = zones à améliorer immédiatement visibles

## Données
- Score par muscle calculé via : nombre de sets × coefficient d'activation musculaire
- Ex : Bench Press → pectoraux 1.0, triceps 0.6, épaules 0.3

## Technique Flutter
- Package : `fl_chart` (RadarChart) — déjà potentiellement présent dans le projet
- Données passées depuis le résultat de l'analyse IA

## Lié à
- [[Analyse IA d'un programme]]
- [[Analyse Comparative]]
