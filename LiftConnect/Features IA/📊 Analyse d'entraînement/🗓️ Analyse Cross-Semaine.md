# 🗓️ Analyse Cross-Semaine (Split global)

#liftconnect #ia #feature

status: ⏸️ En attente
priorité: haute (valeur élevée, complexité élevée)
lié à: [[Analyse IA d'un programme]]

## Concept
Analyser l'ensemble des séances d'une semaine pour détecter des déséquilibres
globaux dans le split (ex: trop de Push, pas assez de Pull).

## Problème adressé
Une séance analysée seule peut sembler bonne, mais un Push Day 3x/semaine
sans Pull crée un déséquilibre réel. Seule l'analyse globale le détecte.

## Fonctionnement
1. L'utilisateur sélectionne un programme hebdomadaire (ou la semaine en cours)
2. L'IA reçoit toutes les séances avec leur fréquence
3. Analyse du ratio Push/Pull, quadriceps/ischio, volume total par groupe musculaire
4. Score de récupération : délai entre deux séances qui travaillent le même muscle

## Ratios surveillés
| Ratio | Idéal |
|-------|-------|
| Push / Pull | 1:1 |
| Quad / Ischio | 3:2 |
| Volume ant. épaule / post. épaule | 1:2 |

## Affichage
- Vue semaine avec heatmap musculaire par jour
- Alertes : "Tes pectoraux sont sollicités lundi ET mercredi sans jour de repos"

## Questions ouvertes
- [ ] L'utilisateur doit-il définir son split manuellement ou on le détecte ?
- [ ] Lier à la feature fatigue estimée ? → [[Fatigue Estimée]]

## Lié à
- [[Analyse IA d'un programme]]
- [[Fatigue Estimée]]
- [[🎯 Radar Chart Musculaire]]
