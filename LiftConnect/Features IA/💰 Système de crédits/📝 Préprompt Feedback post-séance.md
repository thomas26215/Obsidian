# 📝 Préprompt Feedback post-séance

Résumés IA automatiques et insights après chaque entraînement.

---

## 🎯 Purpose

Fournir à l'utilisateur un feedback immédiat post-séance :
- Résumé de ce qui s'est bien passé
- Points à améliorer
- Suggestions pour la prochaine séance
- Tracking fatigue

---

## 💳 Coût en crédits

- **Feedback simple** : 1 crédit
- **Feedback complexe** (multi-paramètres) : 2 crédits
- **Utilisation typique** : 12-18 crédits/mois (après chaque séance)

---

## 🧠 Préprompt structure

```
SYSTÈME : Tu es un coach IA qui analyse chaque séance post-training.
Ton rôle : Fournir feedback constructif et motivant basé sur la séance.

CONTEXTE AUTOMATIQUE :
- Exercices de la séance (exos, poids, reps, sets)
- RPE/RIR (perçu par utilisateur)
- Notes personnelles de l'utilisateur
- Historique comparé (progression vs précédent)
- Fatigue ressenti

FEEDBACK À FOURNIR :
1. Résumé séance (ex: "Bonne session, progression squats +2kg")
2. Points forts identifiés (ex: "Excellent contrôle excentrique")
3. Axes d'amélioration (ex: "Repos entre séries à optimiser")
4. Suggestion pour prochaine séance
5. Score global (motivation + data)

TONE : Positif mais honnête, motivant, actionable
```

---

## 📋 Exemples de requêtes utilisateur

```
User complète séance → Trigger automatique
  → Reçoit feedback 2 secondes après

"Comment c'était ma séance ?"
  → Même feedback qu'avant mais sur demand
```

---

## 📊 Contexte injectable

```json
{
  "session_exercises": [
    { "name": "squat", "weight": 90, "reps": 8, "sets": 4, "rpe": 7 },
    { "name": "leg_press", "weight": 150, "reps": 10, "sets": 3, "rpe": 6 },
    { "name": "leg_curl", "weight": 60, "reps": 12, "sets": 3, "rpe": 5 }
  ],
  "session_notes": "Felt strong, good pump",
  "fatigue_level": 6,
  "previous_session": {
    "date": "2026-04-14",
    "squat_weight": 88
  },
  "progression": 2.3
}
```

---

## 📊 Exemple output

```
"Session 💪 — 21 avril

✅ Points forts
- Squat +2kg vs last week (88 → 90) — progression solide !
- Excellent contrôle excentrique sur leg curl
- Bon mind-muscle connection détecté

⚠️ À améliorer
- Repos leg press : 60sec → vise 90sec pour hypertrophie

💡 Pour demain
- Legs bien traités, focus upper body à la prochaine
- Reste bien hydraté, bonne fatigue !

⭐ Note séance : 7.5/10"
```

---

## ✅ Critères de succès

- ✓ Feedback spécifique à la séance (pas générique)
- ✓ Identifie vraie progression/régression
- ✓ Motivant et actionable
- ✓ Rapide (quelques secondes après séance)

---

## 🔗 Lié à

- [[💰 Système de crédits]] — Modèle monétaire
- [[💬 Prompts IA Avancés]] — Système général

---

*Dernière mise à jour : 21 avril 2026*
