# 😴 Fatigue Estimée

#liftconnect #ia #feature #recovery

status: ⏸️ En attente
priorité: moyenne
lié à: [[Analyse Cross-Semaine]]

## Concept
Estimer la fatigue générée par une séance et signaler si le planning
hebdomadaire laisse suffisamment de temps de récupération par groupe musculaire.

## Calcul de la fatigue
Fatigue = sets × reps × coefficient d'intensité (basé sur % 1RM estimé ou RIR)

Exemple :
- Bench Press 4×8 @ intensité haute → fatigue pectoraux : 8.0
- Seuil de récupération pectoraux : 72h minimum

## Ce qu'on affiche
- Indicateur par muscle : "Récupéré / En cours / Surchargé"
- Alerte si deux séances trop proches : "Tes triceps n'ont eu que 24h de repos"
- Recommandation de jour de repos ou de substitution d'exercice

## Limites à communiquer à l'utilisateur
- Estimation basée sur le volume, pas sur la charge réelle
- Ne remplace pas l'écoute du corps
- Ajouter un disclaimer dans l'UI

## Questions ouvertes
- [ ] L'utilisateur peut-il ajuster les seuils de récupération (débutant vs avancé) ?
- [ ] Intégrer un journal de fatigue subjective (RPE post-séance) ?

## Lié à
- [[Analyse Cross-Semaine]]
- [[📈 Historique des Analyses]]
- [[Analyse IA d'un programme]]
