# 💬 Système de Prompts

Index du système de prompts IA avancés avec préprompts et contexte injectable.

## Features principales

- [[💬 Prompts IA Avancés]] — Questions personnalisées + contexte riche + préprompts
- [[🔧 Mécanisme - Préprompts combinés]] — Explication : préprompts pré-remplissent + utilisateur enrichit

## Caractéristiques

- **Préprompts** : 5 catégories (Analyse, Optimisation, Récupération, Progression, Diagnostic)
- **Contexte injectable** : Profil, Programme, Stats, Séance, Profil étendu
- **Combinaison** : Préprompt (base) + Prompt libre (enrichissement)
- **Réponse** : Hybrid (texte + structuré + visualisations optionnelles)
- **Historique** : Sauvegarder et réutiliser les prompts

## Flux utilisateur

```
1. Sélectionner un préprompt (optionnel)
   ↓ Pré-remplit le textarea
   
2. Modifier/ajouter du contenu libre
   ↓ Enrichissement du prompt
   
3. Sélectionner le contexte à injecter
   ↓ Profil, Programme, Stats, etc.
   
4. Aperçu du contexte (transparence)
   ↓ Validation avant envoi
   
5. Envoyer → IA analyse → Réponse structurée
   ↓ Sauvegarde optionnelle
```

## Données stockées
Firestore : `users/{uid}/ai_prompts/`

## Lié à
- [[📊 Analyse d'entraînement]] — Analyses automatisées (complémentaire)
- [[Analyse IA d'un programme]] — Concept base partagée
