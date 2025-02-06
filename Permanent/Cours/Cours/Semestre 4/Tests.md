**Un test** est vérifié par l'éxecution, confronte à une réalisation à sa spécification et a un critère d'arrêt avec un mise en `succès` ou en `échec`.
**Un cas de test** est un tuple composé de3 objets : Un état initial, un état final et un oracle qui va prédire l'état d'arrivé en fonction de l'état de départ et comparer le résultat théorique et le résultat pratique.

Phase du projet :
- Test unitaire
- Test d'intégration
- Tests système


# Tests
## Tests unitaires
Test unitaire : Teste une unité de code (fonction, méthode, classe) de manière isolée.
Unité de code : Plus petite partie de code testable.
En isolation : Pas de dépendance à l'environnement d'exécution.

Les tests unitaires doivent être rejoués pour vérifier la non régression du code.

## Tests fonctionnels vs tests structurels
Tests fonctionnels : On a uniquement accès aux entrées sorties. On vérifie si une fonction est correctement codée au regard des spécifications en testant plusieurs paires d'E/S. et il y a peu de test
Test structurels : On a un connaissance complète du code. On vérifie si toutes les unité de code ayant permis à l'implémentation de la fonctionnalité ont bien été codées. Il y a ici beaucoup de tests
