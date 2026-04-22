# 📈 Historique des Analyses

#liftconnect #ia #feature #progression

status: 🟡 À faire
priorité: moyenne
lié à: [[Analyse IA d'un programme]]

## Concept
Sauvegarder chaque analyse IA pour permettre à l'utilisateur de suivre
l'évolution de la qualité de ses programmes dans le temps.

## Données sauvegardées par analyse
```json
{
  "program_id": "push_day_v2",
  "analyzed_at": "2026-04-21",
  "scores": {
    "global": 74,
    "balance": 62,
    "volume": 81
  },
  "summary": "Bonne couverture pectoraux, manque de travail épaules arrière"
}
```

## Firestore
Collection : `users/{uid}/programs/{programId}/analyses`
→ Chaque document = une analyse horodatée

## Affichage
- Graphique linéaire : évolution des 3 scores dans le temps
- Message de progression : "Ton score d'équilibre est passé de 62 → 78 ✓"
- Comparaison avec la dernière analyse en highlight

## Déclenchement d'une nouvelle analyse
- Automatique si le programme a été modifié depuis la dernière analyse
- Manuel via le bouton "Ré-analyser"

## Lié à
- [[Analyse IA d'un programme]]
- [[Architecture Firebase]]
