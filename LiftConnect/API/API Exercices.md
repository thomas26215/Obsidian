# 💪 API Exercices

## Description
Permet d'accéder à la base de données d'exercices LiftConnect.
Read-only — pas de données sensibles utilisateur.

## Endpoints
| Méthode | Route | Description |
|--------|-------|-------------|
| GET | `/exercises` | Liste avec filtres |
| GET | `/exercises/{id}` | Détail d'un exercice |

## Paramètres de filtre (`GET /exercises`)
- `muscle` — ex: `chest`, `back`, `legs`
- `equipment` — ex: `barbell`, `dumbbell`, `bodyweight`
- `difficulty` — ex: `beginner`, `intermediate`, `advanced`

## Exemple de réponse
```json
{
  "id": "bench_press",
  "name": "Bench Press",
  "muscles": ["chest", "triceps", "shoulders"],
  "equipment": "barbell",
  "substitutions": ["dumbbell_press", "push_up"]
}
```

## Source de données
Firestore : `exercises/` (327 exercices existants)

## Authentification requise
Non — endpoint public (rate limiting quand même)

## Cas d'usage
- Site d'un coach qui affiche une bibliothèque d'exercices
- App tierce qui veut des suggestions de substitutions

## Lié à
- [[Vue d'ensemble API]]
- [[Authentification API]]
