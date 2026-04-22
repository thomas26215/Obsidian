# 📊 Analyse Comparative

#liftconnect #ia #feature

status: 🟡 À faire
priorité: moyenne
lié à: [[Analyse IA d'un programme]]

## Concept
Comparer le programme de l'utilisateur à un template de référence
("Push Day optimal", "Full Body débutant", etc.) et afficher l'écart.

## Fonctionnement
1. L'IA identifie le type de programme (Push / Pull / Legs / Full Body / Upper-Lower…)
2. On charge le template de référence correspondant depuis Firestore
3. On compare les scores (global, équilibre, volume) entre le programme réel et le template
4. On affiche l'écart : +/- par catégorie

## Affichage suggéré
"Ton Push Day atteint 78% du Push Day optimal.
Points à combler : haut des pectoraux (-2 sets), deltoïdes postérieurs (-1 set)"

## Templates de référence
Stockés dans Firestore : `templates/{type}/reference`
Créés manuellement au départ (5-6 templates suffisent)

## Questions ouvertes
- [ ] Qui valide les templates de référence ? (sources scientifiques ?)
- [ ] Adapter le template selon niveau (débutant / intermédiaire / avancé) ?

## Lié à
- [[Analyse IA d'un programme]]
- [[🎯 Radar Chart Musculaire]]
- [[Architecture Firebase]]
