# 🤖 Préprompt Génération

Création de programmes d'entraînement personnalisés avec IA.

---

## 🎯 Purpose

Générer des programmes complets adaptés à :
- Objectifs utilisateur (force, hypertrophie, endurance)
- Expérience et niveau
- Équipement disponible
- Temps disponible
- Historique et préférences

---

## 💳 Coût en crédits

- **Générer programme complet** (4-6 semaines) : 25-30 crédits
- **Générer variant/adapter** (modifier existant) : 15 crédits
- **Utilisation typique** : 100-120 crédits/mois (4-5 générations)

---

## 🧠 Préprompt structure

```
SYSTÈME : Tu es un coach programmer expert en structuration d'entraînement.
Ton rôle : Créer des programmes complets et adaptés à l'utilisateur.

CONTEXTE AUTOMATIQUE :
- Objectifs (force, hypertrophie, endurance, mix)
- Expérience (débutant, intermédiaire, avancé)
- Équipement disponible/non disponible
- Temps dispo par semaine (3-5 sessions)
- Historique (exos préférés/détestés)
- Blessures/limitations
- Préférences (low-frequency, high-frequency, etc.)

PROGRAMME À GÉNÉRER :
1. Structure macrocycle (ex: 4 semaines linear progression)
2. Répartition musculation (PPL, Upper/Lower, Full-body)
3. Pour chaque séance :
   - Exercises (nom + variantes)
   - Reps/sets prescrit
   - Tempo si pertinent
   - Rest periods
4. Progression scheme (ex: +2.5kg/semaine)
5. Deload instructions

FORMAT : JSON + Markdown lisible

TONE : Expert, structuré, detaillé mais compréhensible
```

---

## 📋 Exemples de requêtes utilisateur

```
"Génère un programme force, 4 semaines, 4 jours/semaine"
  → Programme complet avec progressions

"Même programme mais sans barbell"
  → Variant avec dumbbells/machines uniquement

"Je veux du hypertrophy explosif"
  → Programme volume-focused, tempo excentrique
```

---

## 📊 Contexte injectable

```json
{
  "objectives": ["hypertrophy", "strength"],
  "experience_level": "intermediate",
  "sessions_per_week": 4,
  "equipment_available": ["barbell", "dumbbells", "cables", "machines"],
  "equipment_unavailable": ["leg_press"],
  "user_history": {
    "favorite_exercises": ["incline_dumbbell", "squat"],
    "disliked": ["leg_curl"]
  },
  "injuries": [],
  "time_per_session": 60,
  "duration_weeks": 4,
  "preferences": { "low_frequency": false, "high_intensity": true }
}
```

---

## 📋 Exemple output (partiel)

```markdown
# Program: Upper/Lower Split 4 Weeks
*Designed for hypertrophy + strength*

## UPPER A (Monday)
### Warm-up
- Band pull-aparts 2x10
- Scapular pull-ups 2x5

### Main
**Incline Barbell Bench Press**
- Week 1: 4x6 @ 70kg
- Week 2: 4x6 @ 72.5kg
- Week 3: 4x7 @ 72.5kg
- Week 4: 3x5 @ 75kg (deload reduced)
- Rest: 3 min

**Bent Over Barbell Row**
- Week 1-3: 4x6-8 @ 80kg
- Week 4: 3x5 @ 82.5kg
- Rest: 2 min

...

## Progression Scheme
- Add 2.5kg when hitting reps goal
- Deload week 4: -10% weight, same volume target
```

---

## ✅ Critères de succès

- ✓ Programme cohérent (pas aléatoire)
- ✓ Adaptée vraiment à l'utilisateur (pas générique)
- ✓ Progressive overload clair
- ✓ Progression timeline réaliste
- ✓ Format pratique à utiliser

---

## 🔗 Lié à

- [[💰 Système de crédits]] — Modèle monétaire
- [[💬 Prompts IA Avancés]] — Système général

---

*Dernière mise à jour : 21 avril 2026*
