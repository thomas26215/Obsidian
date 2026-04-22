# 🔐 Authentification API

## Approche recommandée : API Keys

### Fonctionnement
- Chaque développeur/coach génère une **API key** depuis son compte LiftConnect
- La clé est passée dans le header : `Authorization: Bearer <api_key>`
- La clé est liée à un userId → définit les droits d'accès

### Scopes envisagés
| Scope | Accès |
|-------|-------|
| `exercises:read` | Lire la base d'exercices |
| `programs:read` | Lire les programmes publics |
| `groups:read` | Lire les membres d'un groupe |
| `groups:write` | Ajouter / retirer des membres |
| `stats:read` | Lire les stats d'un utilisateur |

## Alternative : OAuth 2.0
Plus robuste mais plus complexe à implémenter.
À envisager si des **apps tierces** veulent agir au nom d'un utilisateur.

## Sécurité
- [ ] Rate limiting par API key
- [ ] Logs des appels API
- [ ] Révocation de clé possible depuis l'app

## Lié à
- [[Vue d'ensemble API]]
- [[API Groupes]]
