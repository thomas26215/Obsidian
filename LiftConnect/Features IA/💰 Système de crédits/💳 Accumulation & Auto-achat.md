# 💳 Accumulation & Auto-achat

Gestion des crédits : expiration vs accumulation et configuration de l'auto-achat.

---

## 🎯 Overview

```
Crédits ABONNEMENT
  → Renouvelés 1er du mois
  → EXPIRENTS fin du mois
  → Créent urgence d'utilisation

Crédits BONUS
  → Achetés une fois
  → GARDÉS INDÉFINIMENT
  → S'accumulent sans limite
```

---

## 📊 Cycle mensuel

### Jour 1 du mois
```
Renouvellement abonnement :
├─ Paiement 1 : Abonnement (0,99€-5€)
│  └─ +X crédits ABONNEMENT (expirents fin mois)
└─ Paiement 2 (si auto-achat activé) : Bonus (1,49€-6,49€)
   └─ +Y crédits BONUS (persistents)

Exemple Analyse + Auto-achat 20 :
├─ 0,99€ → +30 crédits abonnement
└─ 1,49€ → +20 crédits bonus
   Total mensuel : 2,48€
```

### Jour 30 du mois
```
Fin de période :
├─ Crédits abonnement non-utilisés = PERDUS
├─ Crédits bonus = ACCUMULÉS
└─ Reste de bonus = reporté au mois suivant
```

---

## 💬 Auto-achat bonus (configuration)

Utilisateur peut configurer automatique à chaque renouvellement :

### Interface configuration
```
⚙️ Auto-achat de crédits bonus
├─ Actif : [Oui] [Non]
├─ Quantité : [10 / 20 / 50 / 100 crédits]
├─ Prix : 1,49€ / 3,49€ / 6,49€
├─ Fréquence : Chaque renouvellement
└─ Prochain : [Affiche date]

✓ Facile à modifier/désactiver
✓ Transparent sur le coût
```

---

## 📈 Exemple accumulation réaliste

### Scénario : Utilisateur Analyse + Auto-achat 20

```
MOIS 1 :
  Jour 1 : +30 (abonnement) + 20 (bonus) = 50 cr
  Jour 15 : Analyse simple (-2) + complexe (-5) = -7 cr
  Jour 31 : Fin mois
    → Crédits abonnement non-utilisés : -23 cr (PERDUS)
    → Crédits bonus restants : +20 cr (PERSISTENTS)
    → Total conservé : 20 cr bonus

MOIS 2 :
  Jour 1 : 20 (bonus restants) + 30 (nouvel abon) + 20 (auto-achat) = 70 cr
  Jour 20 : Analyses (-10) = -10 cr
  Jour 31 : Fin mois
    → Abonnement non-utilisé : -20 cr (PERDUS)
    → Bonus restants : +40 cr (PERSISTENTS)

MOIS 3 :
  Jour 1 : 40 (bonus) + 30 (abon) + 20 (auto-achat) = 90 cr
  → Utilisateur peut faire 1 générations (-30) confortablement
  → Reste 60 bonus après

MOIS 6 :
  → Potentiellement 100+ crédits bonus accumulés
  → Énorme flexibilité d'utilisation
```

---

## 🎯 Psychologie du système

```
UTILISATEUR LÉGER :
"Zut, j'ai perdu mes crédits"
→ Décide d'activer auto-achat pour ne pas perdre

UTILISATEUR RÉGULIER :
"Ça accumule, j'ai une réserve!"
→ Se sent "investi", reste abonné plus longtemps

UTILISATEUR POWER :
"J'ai 150+ bonus, je peux tester tout"
→ Utilise aussi d'autres features (cross-selling)
```

---

## 💡 Design choices

✅ **Expiration crédits abonnement** : Crée urgence, limite inflation usage  
✅ **Accumulation crédits bonus** : Réduit frustration, crée habituel usage  
✅ **Auto-achat** : Revenue prévisible, UX fluide, opt-in (pas de friction)  
✅ **2x plus cher bonus** : Incite abonnement régulier  

---

## 🔗 Lié à

- [[💰 Système de crédits]] — Vue d'ensemble
- [[📋 Abonnements & Pricing]] — Tarification

---

*Dernière mise à jour : 21 avril 2026*
