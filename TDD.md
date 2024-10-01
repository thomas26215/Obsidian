---
MOOC: "[[Autre]]"
Sujet: Gestion de projets
Type: Méthodes agiles
tags:
---
Le principe du TDD consiste à coder les tests avant le code. Ainsi, cela force le développeur à se contraindre aux tests et donc à ne pas sortir du sentier. Il est nécessaire de faire de       l'[[Intégration continue|intégration continue]] pour faire du TDD et inversement
**Le process est le suivant** : On écrit un test qui échoue, on écrit ensuite le code minimal pour faire passer le test, nous refactorisons par la suite le code si nécessaire et on répète le process
>[!info]
>La courbe d'apprentissage peut être importante ce qui ralentit le développement initial

Il y a plusieurs avantages : une documentation vivante de code sous forme de tests, une meilleure conception du code ...
Cela permet également la [[non-regression]] du code
Il existe de nombreux frameworks comme Junits sur Java