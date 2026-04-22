# 📋 API Programmes

## Description
Permet aux coachs et développeurs de consulter, créer et modifier des programmes d'entraînement.
Interface principale pour la gestion des workouts.

## Endpoints
| Méthode | Route | Description |
|--------|-------|-------------|
| GET | `/programs` | Lister les programmes (propres + publics) |
| GET | `/programs/{programId}` | Détail d'un programme |
| POST | `/programs` | Créer un nouveau programme |
| PUT | `/programs/{programId}` | Modifier un programme |
| DELETE | `/programs/{programId}` | Supprimer un programme |
| POST | `/programs/{programId}/clone` | Dupliquer un programme |
| GET | `/programs/{programId}/workouts` | Lister les séances du programme |

## Paramètres de filtre (`GET /programs`)
- `type` — ex: `push_pull_legs`, `upper_lower`, `full_body`, `push`, `pull`, `legs`
- `level` — ex: `beginner`, `intermediate`, `advanced`
- `public` — `true` ou `false` (défaut: false)
- `creator_id` — ex: `coach_123` (pour lister les programmes d'un coach)

## Exemple de réponse — Programme complet
```json
{
  "id": "ppl_v3",
  "name": "Push Pull Legs - Advanced",
  "description": "Split classique PPL optimisé pour hypertrophie",
  "type": "push_pull_legs",
  "level": "advanced",
  "duration_weeks": 12,
  "isPublic": false,
  "creator": {
    "id": "coach_123",
    "name": "Coach Jean"
  },
  "workouts": [
    {
      "id": "push_mon",
      "name": "Push - Monday",
      "day": 1,
      "focus": ["chest", "shoulders", "triceps"],
      "exercises": [
        {
          "id": "bench_press",
          "name": "Bench Press",
          "sets": 4,
          "reps": "6-8",
          "weight": "RPE 8",
          "rest": 180
        }
      ]
    }
  ],
  "deload_week": 6,
  "createdAt": "2026-03-15T10:00:00Z",
  "updatedAt": "2026-04-20T14:30:00Z"
}
```

## Créer un programme (`POST /programs`)
```json
{
  "name": "Custom Push Day",
  "type": "push",
  "level": "intermediate",
  "description": "Focus pectoraux et épaules",
  "duration_weeks": 4,
  "isPublic": false,
  "workouts": [...]
}
```

## Source de données
Firestore : `programs/` et `users/{userId}/programs/`

## Authentification requise
- `programs:read` — consulter les programmes
- `programs:write` — créer/modifier ses propres programmes
- `programs:admin` — modifier les programmes d'autres utilisateurs (admin uniquement)

## Permissions
| Action | Owner | Coach du groupe | Admin |
|--------|-------|-----------------|-------|
| Lire programme privé | ✅ | ✅ | ✅ |
| Modifier programme | ✅ | ❌ | ✅ |
| Supprimer programme | ✅ | ❌ | ✅ |
| Publier programme | ✅ | ❌ | ✅ |
| Cloner programme | ✅ | ✅ | ✅ |

## Cas d'usage
- Coach qui crée des programmes via une plateforme tierce
- Intégration avec Notion / Google Sheets
- App tierce qui propose des templates de programmes
- Partage de programmes entre membres d'un groupe

## Questions ouvertes
- [ ] Versioning des programmes (v1.0, v1.1, etc.) ?
- [ ] Support des variantes (alternates) pour un même exercice ?
- [ ] Metrics de popularité (likes, utilisations) pour les programmes publics ?
- [ ] Import depuis des formats standards (PDF, JSON) ?

## Lié à
- [[Vue d'ensemble API]]
- [[Authentification API]]
- [[API Exercices]]
- [[API Groupes]]
- [[Analyse IA d'un programme]]
