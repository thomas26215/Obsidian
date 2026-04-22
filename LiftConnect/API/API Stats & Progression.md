# 📊 API Stats & Progression

## Description
Permet à des applications tierces de consulter les statistiques et la progression d'un utilisateur.
Données personnelles — authentification requise.

## Endpoints
| Méthode | Route | Description |
|--------|-------|-------------|
| GET | `/users/{userId}/stats` | Stats globales (PR, volume, etc.) |
| GET | `/users/{userId}/stats/exercises/{exerciseId}` | Progression sur un exercice |
| GET | `/users/{userId}/stats/timeline` | Historique mensuel des progrès |
| GET | `/users/{userId}/workouts` | Historique des séances |

## Paramètres de filtre
- `from` — date début (ISO 8601)
- `to` — date fin (ISO 8601)
- `muscle_group` — ex: `chest`, `back`
- `limit` — nombre de résultats (défaut: 50)

## Exemple de réponse — Stats globales
```json
{
  "userId": "user_123",
  "totalWorkouts": 47,
  "totalVolume": 12500,
  "personalRecords": {
    "bench_press": 140,
    "squat": 180,
    "deadlift": 220
  },
  "averageWorkoutDuration": 62,
  "consistencyScore": 0.87,
  "lastWorkout": "2026-04-20T18:30:00Z"
}
```

## Exemple de réponse — Progression exercice
```json
{
  "exerciseId": "bench_press",
  "exerciseName": "Bench Press",
  "history": [
    { "date": "2026-04-01", "weight": 130, "reps": 5, "sets": 3 },
    { "date": "2026-04-08", "weight": 135, "reps": 5, "sets": 3 },
    { "date": "2026-04-15", "weight": 140, "reps": 5, "sets": 3 }
  ],
  "estimatedMax": 155,
  "trend": "↗ +10 kg en 3 semaines"
}
```

## Source de données
Firestore : `users/{userId}/workouts/` et `users/{userId}/stats/`

## Authentification requise
**OUI** — Scope : `stats:read`
- Un utilisateur ne peut accéder qu'à **ses propres stats**
- Un coach peut accéder aux stats de ses membres (via `groups:read`)

## Cas d'usage
- Dashboard personnalisé d'un utilisateur sur site web tiers
- App de suivi fitness qui s'intègre à LiftConnect
- Partage de progression publique (via lien unique)

## Questions ouvertes
- [ ] Permettre le partage public de stats via un token unique ?
- [ ] Exporter les données (CSV, PDF) ?
- [ ] Intégrer des graphiques interactifs (tendances, body recomp) ?

## Lié à
- [[Vue d'ensemble API]]
- [[Authentification API]]
- [[API Groupes]]
- [[Historique des Analyses]]
