# 🗺️ Vue d'ensemble — LiftConnect API

## Objectif
Ouvrir LiftConnect à des intégrations tierces (coachs, salles de sport, plateformes d'abonnement).
Positionner LiftConnect comme une **plateforme**, pas juste une app mobile.

## Modèles cibles
- **B2C** : développeurs qui veulent intégrer des données fitness
- **B2B** : coachs / salles de sport avec leur propre site

## APIs prévues
- [[API Exercices]] — base de données publique d'exercices
- [[API Programmes]] — programmes d'entraînement
- [[API Stats & Progression]] — statistiques utilisateur
- [[API Groupes]] — gestion des membres et sessions

## Authentification
→ Voir [[Authentification API]]

## Stack envisagée
- [ ] FastAPI (Python)
- [ ] Node.js / Express
- Base de données : Firestore (existant)

## Priorité de développement
1. API Exercices (read-only, sans risque)
2. API Groupes (valeur B2B forte)
3. API Stats
4. API Programmes
