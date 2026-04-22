# 🔧 Mécanisme : Préprompts + Texte libre combinés

#liftconnect #ia #feature #mechanics

**Clarification clé pour [[💬 Prompts IA Avancés]]**

## Le principe : "Base + Enrichissement"

Au lieu d'un choix **OU** (préprompt OUOU prompt libre), c'est un **ET** (préprompt ETPUIS enrichissement libre).

### Analogie
```
C'est comme un formulaire pré-rempli :
- Le préprompt = les champs pré-remplis
- Le texte libre = tu peux éditer/ajouter dans le textarea
- Résultat = la combinaison des deux
```

## Comment ça marche en détail

### Étape 1 : Utilisateur sélectionne un préprompt
```
Dropdown : [ Sélectionner  ▼ ]
  • Analyse poussée
  • Optimisation
  • Récupération
  • Progression
  • Diagnostic
  • ─────────────────
  • Vierge (start libre)

→ Utilisateur clique "Analyse poussée"
```

### Étape 2 : Textarea pré-remplie
```
La textarea se pré-remplit avec le contenu du préprompt :

┌────────────────────────────────────────────────┐
│ "Fais une analyse complète de ce programme :   │
│                                                 │
│  - Évalue la couverture musculaire              │
│  - Identifie les points faibles                 │
│  - Donne des recommandations spécifiques        │
│  - Format : points clés + actions concrètes"   │
│                                                 │
│ [Curseur ici - utilisateur peut modifier]      │
└────────────────────────────────────────────────┘
```

### Étape 3 : Utilisateur modifie/ajoute
```
L'utilisateur peut :
1. Ajouter des détails AU-DESSUS
   "Utilise mon profil (intermédiaire, hypertrophie).
    Fais une analyse complète de ce programme : ..."

2. Ajouter EN-DESSOUS
   "... Format : points clés + actions concrètes.
    Focus particulier : améliorer mes épaules arrière !"

3. Modifier la moitié du préprompt
   "Simplement une analyse complète [continuer avec le reste]"

4. Partir du préprompt et le réécrire complètement
   (C'est juste une base, pas un carcan)
```

### Résultat : Prompt final
```
"Utilise mon profil (intermédiaire, hypertrophie).
 Fais une analyse complète de ce programme :
 
  - Évalue la couverture musculaire
  - Identifie les points faibles
  - Donne des recommandations spécifiques
  - Format : points clés + actions concrètes
  
 Focus particulier : améliorer mes épaules arrière !"
```

## Options de flux

### Option A : Préprompt uniquement
```
✓ Sélectionner "Analyse poussée"
✗ Modifier
→ Envoyer le préprompt tel quel
```

### Option B : Préprompt + enrichissement léger
```
✓ Sélectionner "Analyse poussée"
✓ Ajouter "Focus épaules arrière" en fin
→ Envoyer préprompt + détail user
```

### Option C : Préprompt profondément modifié
```
✓ Sélectionner "Diagnostic"
✓ Réécrire presque complètement en gardant la structure
→ Envoyer texte finalisé (inspiré du préprompt)
```

### Option D : Texte 100% libre (Vierge)
```
✓ Sélectionner "Vierge"
✓ Écrire n'importe quoi
→ Envoyer prompt complètement libre
```

## Avantages de ce design

| Aspect | Bénéfice |
|--------|----------|
| **Accessibilité** | Novice peut juste utiliser préprompt tel quel |
| **Flexibilité** | Avancé peut modifier/combiner préprompts |
| **Contextualisation** | Préprompt structure la pensée de l'IA |
| **Rapidité** | Pas besoin de réécrire à zéro chaque fois |
| **Découverte** | L'utilisateur voit des exemples de prompts efficaces |

## Cas d'usage concrets

### User Story 1 : Débutant (utilise préprompt tel quel)
```
1. "Je vais cliquer sur 'Analyse poussée'"
2. "Je vois un texte pré-rempli, ça me plaît"
3. "Je vais envoyer comme c'est"
4. "L'IA me donne une analyse complète !"

Résultat : Impact rapide, utilisateur satisfait
```

### User Story 2 : Intermédiaire (enrichit le préprompt)
```
1. "Je vais cliquer sur 'Optimisation'"
2. "Je vois le texte, mais j'ai un besoin spécifique"
3. "J'ajoute en fin : 'Je n'ai que des haltères, pas de barre'"
4. "L'IA me propose des exercices adaptés"

Résultat : Réponse hyper-personnalisée
```

### User Story 3 : Avancé (crée son propre prompt)
```
1. "Je vais cliquer sur 'Vierge' ou 'Diagnostic'"
2. "Je vois la base... mais je vais la réajuster"
3. "Je réécrire mon prompt pour ma situation très spécifique"
4. "L'IA comprend exactement ce que je demande"

Résultat : Contrôle total
```

### User Story 4 : Réutilise un ancien prompt
```
1. "Je vais dans 'Historique'"
2. "Je vois mes anciens prompts en liste"
3. "Celui du 15 avril était bon → Je clique 'Réutiliser'"
4. "Le préprompt se charge automatiquement"
5. "Je peux le modifier pour cette nouvelle analyse"

Résultat : Itération rapide
```

## Implémentation Flutter

### Pseudo-code
```dart
class AIPromptScreen {
  TextEditingController promptController = TextEditingController();
  String selectedPreprompt = 'vierge';
  
  void onPrepromptSelected(String category) {
    // Charger le texte du préprompt
    String prepromptText = getPrepromptText(category);
    // Pré-remplir le textarea
    promptController.text = prepromptText;
    // Utilisateur peut maintenant modifier
  }
  
  void onSendPrompt() {
    // Récupérer le texte final (modifié ou non)
    String finalPrompt = promptController.text;
    // Ajouter contexte
    String contextualizedPrompt = injectContext(finalPrompt);
    // Envoyer à l'IA
    callAI(contextualizedPrompt);
  }
}
```

### TextField éditable (Flutter)
```dart
TextField(
  controller: promptController,
  maxLines: 8,
  decoration: InputDecoration(
    labelText: "Ta question (modifie le préprompt si besoin)",
    border: OutlineInputBorder(),
  ),
  // L'utilisateur peut éditer librement
)
```

## Sauvegarder le "prompt modifié"

### Tracking
```json
{
  "id": "prompt_20260421_001",
  "preprompt_selected": "Analyse poussée",
  "preprompt_original": "Fais une analyse complète...",
  "prompt_modified_by_user": "Utilise mon profil... Focus épaules",
  "was_changed": true,
  "change_type": "enrichment" // ou "major_rewrite" ou "unchanged"
}
```

Cela permet de :
- Savoir d'où vient le prompt
- Tracker ce que les users modifient
- Proposer des améliorations aux préprompts basé sur les edits

## Lié à
- [[💬 Prompts IA Avancés]] — Feature principale
