# 📊 Dashboard utilisateur

Interface de gestion des crédits affichée à l'utilisateur.

---

## 🎯 Purpose

Donner visibilité totale sur :
- Crédits disponibles (abonnement vs bonus)
- Consommation du mois
- Configuration auto-achat
- Options d'achat bonus

---

## 📱 Design principal

```
┌─────────────────────────────────────────────────┐
│                💳 MES CRÉDITS                   │
├─────────────────────────────────────────────────┤
│                                                 │
│  ABONNEMENT (expire 30/04)                     │
│  ⏰ 8 crédits restants / 30                    │
│  ⚠️ Attention : expirents demain !             │
│                                                 │
│  BONUS PERMANENTS (sans limite)                │
│  💰 47 crédits accumulés                       │
│                                                 │
├─────────────────────────────────────────────────┤
│         📊 CONSOMMATION CE MOIS                 │
│                                                 │
│  Analyses :                                    │
│    • Simples (-2 cr) × 4 = -8                  │
│    • Complexes (-5 cr) × 1 = -5                │
│  Feedbacks (-1 cr) × 5 = -5                    │
│  Substitutions (-1,5 cr) × 2 = -3              │
│                                                 │
│  ➊ Total utilisé : -21 crédits                │
│  ├─ Du abonnement : -13 cr                     │
│  └─ Des bonus : -8 cr                          │
│                                                 │
├─────────────────────────────────────────────────┤
│        🔧 MES ABONNEMENTS                      │
│                                                 │
│  ✓ Analyse (0,99€/mois)                        │
│    └─ Auto-achat : 20 bonus/mois (+1,49€)      │
│                                                 │
│  Renouvellement : 01 mai (10 jours)            │
│                                                 │
├─────────────────────────────────────────────────┤
│         🛍️ ACHETER CRÉDITS BONUS               │
│                                                 │
│  [20 crédits - 1,49€] [50 - 3,49€] [100 - 6,49€]
│                                                 │
└─────────────────────────────────────────────────┘
```

---

## 🎨 Sections détaillées

### Section 1 : Crédits disponibles

```
Status: Deux pools clairs

ABONNEMENT
├─ Nombre restants / Total
├─ Barre de progression
├─ Date expiration
└─ Alerte si bas (< 10 crédits)

BONUS
├─ Total accumulé
├─ Pas de limite
└─ Non-expirant badge
```

### Section 2 : Consommation

```
Détail par type d'action :
├─ Analyses : X utilisés / coût total
├─ Feedbacks : X utilisés
├─ Substitutions : X utilisés
├─ Générations : X utilisés
├─ Conseils : X utilisés
└─ Objectifs : X utilisés

Avec breakdowns :
├─ Par pool (abonnement vs bonus)
└─ Par jour/semaine optionnellement
```

### Section 3 : Abonnements actifs

```
Liste abonnements en cours :
├─ Nom + prix
├─ Auto-achat : [On/Off] + quantité
├─ Renouvellement countdown
└─ [Modifier] [Changer] [Annuler]
```

### Section 4 : Achat bonus

```
Trois options claires :
├─ Pack petit (20) - 1,49€
├─ Pack moyen (50) - 3,49€
└─ Pack grand (100) - 6,49€

Chacun avec :
├─ Prix/crédit affichée
├─ Économie vs petit
└─ [Acheter] button
```

---

## 🔄 Alertes et notifications

### Défaut proactive

```
"3 crédits abonnement restants"
  → Suggestion : "Générer 1 programme (-30) utiliserait bonus"

"Tu dépenses bonus souvent"
  → Suggestion : "Activer auto-achat -20 cr/mois ?"

"Abonnement expire demain"
  → Alerte : "Renouvellement automatique le 01 mai"
```

### Lors d'action

```
Avant utiliser feature IA :
"Génération programme coûtera 30 crédits"
├─ Tu as : 8 (abonnement) + 47 (bonus) = 55 total ✓
└─ Après : 25 crédits restants

Button : [Confirmer] ou [Annuler]
```

---

## 📱 Mobile-first design

```
Stack layout vertical :
├─ Crédits (big numbers)
├─ Consommation (progressbar)
├─ Abonnements (cards)
└─ Achat bonus (buttons prominence)

Touch-friendly :
├─ Big buttons (50px minimum)
├─ Swipes pour détails
└─ Scroll pour historique
```

---

## 🎯 Critères success

✅ Clair à première vue (crédits disponibles)  
✅ Transparent sur consommation  
✅ Configuration auto-achat simple  
✅ Alerte proactive si bas  
✅ Easy achat bonus en 1-2 taps  

---

## 🔗 Lié à

- [[💰 Système de crédits]] — Système global
- [[💳 Accumulation & Auto-achat]] — Mécanique

---

*Dernière mise à jour : 21 avril 2026*
