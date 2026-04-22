# 💬 Préprompt Analyse

Analyse intelligente des séances et programmes d'entraînement.

---

## 🎯 Purpose

Fournir à l'utilisateur une analyse détaillée de sa séance/programme pour identifier :
- Force/faiblesses de la structure
- Couverture musculaire
- Intensité et volume
- Recommandations d'amélioration

---

## 💳 Coût en crédits

- **Analyse simple** (1-2 paramètres) : 2 crédits
- **Analyse complexe** (4+ paramètres) : 5 crédits
- **Utilisation typique** : 20-25 crédits/mois

---

## 🧠 Préprompt structure

```
SYSTÈME : Tu es un coach IA expert en structuration d'entraînement.
Ton rôle : Analyser les séances de l'utilisateur avec objectivité et proposer 
des améliorations basées sur les principes de progressive overload et équilibre.

CONTEXTE AUTOMATIQUE :
- Historique séances (derniers 4 semaines)
- Profil utilisateur (âge, exp, objectifs)
- Exercices présents (muscles sollicités)
- Volume total par muscle
- Progression (charges/reps trend)

ANALYSE À FOURNIR :
1. Points forts identifiés
2. Points faibles / déséquilibres
3. Couverture musculaire visualisée
4. Intensité et volume détection
5. 2-3 suggestions d'amélioration concrètes

TONE : Expert, bienveillant, actionnable
```

---

## 📋 Exemples de requêtes utilisateur

```
"Analyse ma séance d'aujourd'hui"
  → Analyse complexe des exercices, sets, reps, poids

"C'est quoi mes points faibles ?"
  → Comparaison tendance 4 semaines, détection muscles en retard

"Mes épaules stagnent, pourquoi ?"
  → Analyse volume shoulder-focused, intensité, fréquence
```

---

## 📊 Contexte injectable

```json
{
  "recent_sessions": [...],
  "user_profile": { "age": 28, "experience": "3 years", "goals": ["strength", "hypertrophy"] },
  "muscle_coverage": { "chest": 8, "back": 6, "legs": 7, ... },
  "volume_trend": { "week1": 50, "week2": 48, "week3": 52, "week4": 55 },
  "progression": { "squat": [80, 85, 90], "bench": [70, 70, 72] }
}
```

---

## ✅ Critères de succès

- ✓ Identifie déséquilibres réels
- ✓ Suggère améliorations concrètes
- ✓ Basé sur données utilisateur, pas générique
- ✓ Timeboxé (analyse rapide)

---

## 🔗 Lié à

- [[💰 Système de crédits]] — Modèle monétaire
- [[📊 Analyse d'entraînement]] — Feature complète
- [[🎯 Radar Chart Musculaire]] — Visualisation des résultats

---

*Dernière mise à jour : 21 avril 2026*
