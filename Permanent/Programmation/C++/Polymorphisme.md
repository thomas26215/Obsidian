---
MOOC: "[[Programmation]]"
Langage: C++
Type: Classes
tags:
---
Si plusieurs classes dérivent d'une classe, il est possible de faire du polymorphisme :
```cpp
Personne* p1 = new Personne("dupond", "10 rue de l'Isère");
Personne* p1 = new Etudiant("durand", "15 rue de l'Isère");
Personne* p1 = new Salarie("dumoulin", "21 rue de l'Isère", "shneider", 4000.0);
```

Nous voyons que nous ajoutons 3 adresse d'objets de différents types à des variables déclarés comme pointeurs sur Personne. C'est possible car les classes Salarie et Etudiant sont des classes héritées de la classe Personne