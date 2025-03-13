---
MOOC: "[[Programmation]]"
Langage: NodeJS
Type: Tests Unitaires
Outil:
  - assert
tags:
---
Le module `assert` de nodeJS fonctionne dans un environnement Node.js. Ce module est conçu pour être utilisé dans Node.JS et n'est pas directement compatible avec les navigateurs sans une adaptation

Ce module peut néanmoins fonctionner avec du code JavaScript standard. Le "code JavaScript standard" fait référence à tout code écrit en JavaScript, qu'il soit destiné à être exécuté dans un navigateur ou dans Node.js. Tant que le code respecte les spécifications ECMAScript, il peut être testé avec `assert` dans un environnement Node.js. Voici pourquoi :
- Node.js peut exécuter tout code JavaScript standard.
- Le module `assert` de Node.js fonctionne comme une bibliothèque d'assertions pour vérifier les conditions dans le code.
## Limites
Cependant, **le module `assert` ne fonctionne pas directement dans un navigateur** car il est spécifique à Node.js. Si vous souhaitez utiliser des assertions similaires dans un environnement de navigateur, vous devrez utiliser une librairie comme Chai qui porte le module `assert` pour les navigateurs.