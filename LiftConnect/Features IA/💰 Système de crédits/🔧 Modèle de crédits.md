# 🔧 Modèle de crédits

Les crédits représentent la **consommation IA réelle** (tokens/compute) proportionnelle à la complexité de la requête.

---

## 💻 Consommation par action

### 🔍 Analyse (Préprompt Analyse)
```
Analyse simple (1-2 paramètres)
  → 2 crédits
  Exemple : Volume total de la semaine

Analyse complexe (4+ paramètres)
  → 5 crédits
  Exemple : Volume + Intensity + Rest pattern + Progression détaillée

Utilisation typique : 20-25 crédits/mois
Coût moyen/analyse : ~2.5 crédits
```

### 🔄 Substitution (Préprompt Substitution)
```
Suggestion d'exercice substitut
  → 1-2 crédits
  Tient compte : équipement dispo, muscles, difficulté

Utilisation typique : 15-20 crédits/mois
Coût moyen/substitution : ~1.5 crédits
```

### 🎯 Objectifs adaptatifs (Préprompt Objectifs)
```
Prédiction progression
  → 2-5 crédits (dépend complexité historique)
  Exemple : "Tu atteindras 100kg squat dans X mois"

Détection plateau
  → 3 crédits

Recalibrage objectifs
  → 2 crédits

Utilisation typique : 10-15 crédits/mois
```

### 📝 Feedback post-séance (Préprompt Feedback)
```
Résumé IA automatique après séance
  → 1-2 crédits par séance
  Inclut : Points forts, axes amélioration, suggestions

Utilisation typique : 12-18 crédits/mois
Coût moyen : ~1.5 crédits/séance
```

### 💬 Conseils live (Préprompt Conseils live)
```
Réponse message du coach IA
  → 0,5-1 crédit par message
  Peut être : "Combien de repos ?", "Bonne forme ?", "Je stagne ?"

Utilisation typique : 30-40 crédits/mois
Coût moyen : ~1 crédit/message

Variantes :
  Question simple (-0,5 cr) : "Repos conseillé ?"
  Question complexe (-1 cr) : "Récupération adaptée à mon historique ?"
```

### 🤖 Génération (Préprompt Génération)
```
Générer 1 programme complet (4-6 semaines)
  → 25-30 crédits
  Inclut : Tous les exos, reps, sets, progressions

Générer variant/adapter
  → 15 crédits
  Exemple : "Même programme mais sans machine"

Utilisation typique : 100-120 crédits/mois
Coût moyen : ~25 crédits/génération
```

---

## 📊 Tableau synthèse

| Feature | Coût minimal | Coût maximal | Moyen | Fréquence typique |
|---|---|---|---|---|
| Analyse | 2 cr | 5 cr | 2,5 cr | 3-5x/semaine |
| Substitution | 1 cr | 2 cr | 1,5 cr | 2-3x/semaine |
| Objectifs | 2 cr | 5 cr | 3 cr | 1-2x/semaine |
| Feedback | 1 cr | 2 cr | 1,5 cr | 2-3x/semaine |
| Conseils | 0,5 cr | 1 cr | 0,75 cr | Variable |
| Génération | 15 cr | 30 cr | 25 cr | 1-2x/mois |

---

## 🎯 Principes

1. **Transparence** : Coûts alignés avec consommation réelle OpenAI/Claude
2. **Scalabilité** : Peux ajuster les coûts selon utilisation réelle
3. **Équité** : Utilisateur simple ≠ utilisateur complexe en coûts
4. **Justification** : Chaque crédit utilisé = valeur IA reçue

---

## 💡 Implémentation

### Backend
```
1. Tracer tokens pour chaque préprompt
2. Mapper tokens → crédits (ex : 100 tokens = 1 crédit)
3. Déduire crédits avant envoi IA
4. Gérer deux pools : abonnement vs bonus
```

### Frontend
```
1. Afficher "Coûtera X crédits" avant action
2. Alerter si insuffisants
3. Dashboard détaillé par action
```

---

*Dernière mise à jour : 21 avril 2026*
