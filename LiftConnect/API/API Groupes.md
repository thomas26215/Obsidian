# 👥 API Groupes

## Description
Permet à des plateformes tierces de gérer les membres d'un groupe LiftConnect.
Cas d'usage principal : **intégration avec une plateforme d'abonnement** (Stripe, etc.)

## Endpoints
| Méthode | Route | Description |
|--------|-------|-------------|
| POST | `/groups/{groupId}/members` | Ajouter un membre |
| DELETE | `/groups/{groupId}/members/{userId}` | Retirer un membre |
| GET | `/groups/{groupId}/members` | Lister les membres |
| GET | `/groups/{groupId}` | Infos du groupe |

## Flux typique (Stripe webhook)
```
Stripe "payment_succeeded"
  → Backend du coach
    → POST /groups/{id}/members { "email": "..." }
      → LiftConnect ajoute l'utilisateur au groupe
```

## Questions ouvertes
- [ ] Identification par email ou userId Firebase ?
- [ ] Que faire si l'utilisateur n'a pas encore de compte ? → invitation email ? compte en attente ?
- [ ] Notification push à l'utilisateur quand il est ajouté ?

## Sécurité
- API key liée au propriétaire du groupe
- Un coach ne peut gérer **que ses propres groupes**
- Scope nécessaire : `groups:write`

## Firestore
Collection : `groups/{groupId}/members`

## Lié à
- [[Vue d'ensemble API]]
- [[Authentification API]]
