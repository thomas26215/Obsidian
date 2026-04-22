# 💬 Prompts IA Avancés (Préprompts + Libre)

#liftconnect #ia #feature #advanced

status: 🟡 À faire
priorité: haute (complément puissant à l'analyse basique)
lié à: [[Analyse IA d'un programme]]

## Concept
Système flexible permettant aux utilisateurs de poser des **questions personnalisées** à l'IA tout en injectant automatiquement du **contexte riche** (programme, stats, profil).

Combine préprompts (quick start) + prompt libre poussé (flexibilité) en **même temps**.

## Fonctionnement

### Flux utilisateur
```
1. Sélectionner un préprompt (optionnel)
   → Pré-remplit le textarea avec la base
   
2. Modifier/compléter le prompt libre
   → Utilisateur peut ajouter des détails spécifiques
   → Le préprompt agit comme "base", pas comme rigide
   
3. Sélectionner le contexte à injecter :
   ✓ Profil utilisateur (auto)
   ✓ Programme : [dropdown]
   ✓ Stats : [checkboxes : PR, volume, progression]
   ☐ Séance spécifique (optionnel)
   ☐ Comparaisons (optionnel)
   
4. Aperçu du contexte avant envoi (transparence)
   
5. Envoyer → IA analyse → Réponse structurée
   
6. Sauvegarder dans historique (optionnel)
```

## Catégories de Préprompts (5 principales)

### 🔍 ANALYSE POUSSÉE
- "Analyse complète de ce programme"
- "Identifie les points faibles et déséquilibres"
- "Compare cette séance aux standards de récupération"
- "Tendances détectées dans mon historique"

### ⚙️ OPTIMISATION
- "Suggestions d'exercices substituts (équipement limité)"
- "Progressions naturelles et variances pour cet exercice"
- "Comment adapter ce programme à mon niveau/objectif ?"
- "Structures alternatives pour le même stimulus"

### 😴 RÉCUPÉRATION & BIEN-ÊTRE
- "Mon plan de récupération est-il optimal ?"
- "Récupération estimée pour cette séance"
- "Fréquence optimale pour ce groupe musculaire"
- "Signes de surtraining et prévention"

### 📈 PROGRESSION
- "Stratégie pour atteindre mon prochain PR"
- "Suis-je sur la bonne trajectoire ?"
- "Conseils pour briser un plateau"
- "Phases de progression recommandées"

### 🔴 DIAGNOSTIC
- "Déséquilibres musculaires détectés dans ce split"
- "Pourquoi je me blesse à cet exercice ?"
- "Analyse de mes tendances : patterns anomalies"
- "Adaptations nécessaires suite à blessure/limitation"

### ⚪ VIERGE
- Commencer avec textarea vide pour prompt 100% libre

## Contexte Injectable (5 niveaux)

### Niveau 1 : Profil utilisateur (AUTO)
```json
{
  "level": "intermediate",
  "age": 28,
  "training_age": 5,
  "goal": "hypertrophy",
  "limitations": ["lower_back"],
  "equipment": ["barbell", "dumbbells", "cable"]
}
```

### Niveau 2 : Programme spécifique
```json
{
  "id": "ppl_v3",
  "name": "Push Pull Legs",
  "type": "push_pull_legs",
  "workouts": [full_workout_data],
  "duration_weeks": 12,
  "deload_week": 6
}
```

### Niveau 3 : Stats complètes
```json
{
  "personal_records": {
    "bench_press": 140,
    "squat": 180,
    "deadlift": 220
  },
  "volume_last_month": 12500,
  "consistency_score": 0.87,
  "trend": "↗ +5kg bench en 4 semaines",
  "exercises_history": [...]
}
```

### Niveau 4 : Séance isolée (optionnel)
```json
{
  "name": "Push - Monday",
  "exercises": [...],
  "total_volume": 85,
  "estimated_fatigue": 8.2,
  "estimated_recovery_time": "72h"
}
```

### Niveau 5 : Profil étendu (optionnel)
```json
{
  "diet": "high_protein",
  "sleep_avg": 7.5,
  "stress_level": "moderate",
  "body_composition": "tracked",
  "recovery_priority": "sleep"
}
```

## Interface UI (Flutter)

### Formulaire principal
```
┌────────────────────────────────────────────────────┐
│  💬 Prompts IA Avancés                              │
├────────────────────────────────────────────────────┤
│                                                      │
│  Préprompt (optionnel) :                            │
│  [ Sélectionner une catégorie  ▼ ]                 │
│    • Analyse poussée                                │
│    • Optimisation                                   │
│    • Récupération                                   │
│    • Progression                                    │
│    • Diagnostic                                     │
│    • ─────────────────────────────────────         │
│    • Vierge (texte libre)                           │
│                                                      │
│  Ta question :                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │ "Analyse complète de ce programme             │   │
│  │  Focus particulier : améliorer les épaules"  │   │
│  │                                               │   │
│  │ (Le préprompt pré-remplit,                   │   │
│  │  tu peux modifier/ajouter ici)               │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│  Contexte à injecter :                              │
│  ✓ Mon profil (auto)                               │
│  ✓ Programme : [ Push Pull Legs v3  ▼ ]           │
│  ✓ Stats : [ 6 derniers mois  ▼ ]                 │
│  ☐ Séance spécifique : [ Lundi  ▼ ]               │
│  ☐ Comparaison programme                           │
│  ☐ Profil étendu (alimentation, sommeil)           │
│                                                      │
│  📋 Aperçu du contexte :                            │
│  ┌──────────────────────────────────────────────┐   │
│  │ Intermediate, 28y, 5y training, objectif     │   │
│  │ hypertrophy, limitation lower_back           │   │
│  │                                               │   │
│  │ Programme : PPL 12 sem, Push/Pull/Legs       │   │
│  │ Stats : Bench 140, Squat 180, Deadlift 220   │   │
│  │ Consistency 87%, trend +5kg bench en 4sem     │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│  [ 🚀 Analyser ]  [ 🗑️ Effacer ]                   │
│                                                      │
└────────────────────────────────────────────────────┘
```

## Format de réponse

### Réponse Hybrid (multi-format)

**Partie 1 : Introduction textuelle**
```
"Basé sur ton profil (intermediate, hypertrophie) et ton PPL, 
voici mon analyse..."
```

**Partie 2 : Points clés (bulleted)**
```
• Couverture pectoraux excellente (bench 4x/sem)
• Épaules arrière sous-travaillées (-1-2 sets)
• Volume global bon (12500/mois) mais déséquilibré
```

**Partie 3 : Actions concrètes**
```
Actions recommandées :
1. Ajouter 2 sets de face pulls le lundi (Push)
2. Remplacer 1 set de bench par incline DB press
3. Réduire cable fly (2→1 set) pour plus de compound work
```

**Partie 4 : Visualisations (si pertinent)**
```
[Graphique : Progression Bench estimée]
[Heatmap : Couverture musculaire avant/après recommandations]
[Tableau : Comparaison ratio Push/Pull]
```

## Données à sauvegarder

### Historique des prompts
```json
{
  "id": "prompt_20260421_001",
  "user_id": "user_123",
  "timestamp": "2026-04-21T14:30:00Z",
  "preprompt_category": "Analyse",
  "original_text": "Analyse complète de ce programme",
  "user_modified_text": "Analyse complète... focus épaules",
  "context_used": {
    "profile": true,
    "program_id": "ppl_v3",
    "stats": true,
    "include_extended": false
  },
  "response_text": "...",
  "response_key_points": ["Couverture excellente...", "Épaules arrière..."],
  "response_actions": ["Ajouter face pulls...", "Remplacer bench..."],
  "starred": false,
  "tags": ["ppl", "shoulders", "analysis"]
}
```

### Firestore structure
```
users/{uid}/ai_prompts/
  ├─ prompt_20260421_001/
  ├─ prompt_20260421_002/
  └─ ...

preprompts/ (collection publique)
  ├─ preprompts_analysis.json
  ├─ preprompts_optimization.json
  ├─ preprompts_recovery.json
  ├─ preprompts_progression.json
  └─ preprompts_diagnostic.json
```

## Intégration avec autres features

### Complémentaire à :
- **Analyse basique** (Radar + Global Score) → synthétique et rapide
- **Prompts avancés** → exploration en profondeur et questions spécifiques
- **Historique des analyses** → sauvegarde des résultats

### Flux complet utilisateur
```
1. Voit l'Analyse basique (Radar + Score) → quick feedback
2. Clique "Poser une question" → ouvre formulaire prompts avancés
3. Sélectionne préprompt OU écrit libre (ou les deux)
4. Ajoute contexte spécifique (programme, stats, séance)
5. IA analyse avec contexte riche → réponse structurée
6. Peut sauvegarder et réutiliser ce prompt plus tard
```

## Cas d'usage concrets

### Exemple 1 : Utilisateur intermediate
```
Préprompt : "Analyse poussée"
Modifie : "... focus sur l'équilibre push/pull"
Contexte : Programme + Stats + Séance lundi
Réponse : "Ton ratio est 60/40 au lieu de 50/50, 
recommandations pour le rééquilibrer..."
```

### Exemple 2 : Utilisateur avancé
```
Prompt libre : "Comparaison : mon PPL vs ULUL pour hypertrophie"
Contexte : Profil + Programme + Stats complètes
Réponse : Tableau comparatif, pros/cons, adaptation recommandée
```

### Exemple 3 : Diagnostic
```
Préprompt : "Diagnostic"
Modifie : "Je me blesse à la rotule sur du squat récemment"
Contexte : Profil + Historique séances + Profil étendu
Réponse : Analyse biomécanique estimée, modifications d'exercice
```

## Questions ouvertes

- [ ] Export réponses (PDF, image) ?
- [ ] Partage de prompts/réponses avec coach ? (futur)
- [ ] Favoris (star) et réorganisation des préprompts ?
- [ ] Analytics : quels prompts sont les plus utilisés ?
- [ ] Intégration avec Google Gemini / LLaMA via API ?

## Lié à
- [[🔧 Mécanisme - Préprompts combinés]] — Comment préprompts + texte libre fonctionnent ensemble
- [[Analyse IA d'un programme]] — analyse basique
- [[../📊 Analyse d'entraînement/🎯 Radar Chart Musculaire]] — visualisation résultats
- [[../📊 Analyse d'entraînement/📈 Historique des Analyses]] — sauvegarde réponses IA
- [[Architecture Firebase]] — stockage prompts
