- Il est nécessaire de rédiger des tests pour confirmer la validité du code que l'on produit
- Cela prend du temps (pour tester une grande quantité de code, il faut produire une quantité équivalente de tests) mais cela a un effet bénéfique à long terme ⇒ L'application soigneusement testée est plus stable et fiable
- Au cours de la durée de vie d'un projet, les opérations réalisées sont susceptibles de changer sans pour autant que les API ne soient modifiées ⇒ Les tests unitaires sons là pour garantir le bon fonctionnement de son travail à tout instant
- Egalement, cela constitue une forme de spécification et de documentation d'une application
- Finalement, quand un codeur reprend le travail d'un autre, il sera beaucoup plus facile de maintenir et de déboguer le code grâce à cette batterie de tests

> [!info]
> La culture du test est peu répendue chez les vieux développeurs et cela nécessite une mise en place très coûteuse mais la situation générale s'améliore ! (Utilisation du [[TDD]])


Il existe des tests unitaires servant un tester une partie du code et des tests fonctionnaires qui servent à tester un scénario d'utilisation du logiciel. Il existe des outils pour chaque type de test pour faciliter l'écriture et l'exploitation de leurs résultats
Il existe aussi des outils permettant de faire tourner automatiquement des tests afin de vérifier qu'une application en cours de développement ne régresse pas (*Jenkin, GitLab*) ⇒ [[TDD]]
Si on prend l'exemple de Java, nous avons le framework [[Tests unitaires avec JUnit5|Junit]]. Il a été porté dans d'autres langages (CPPUnit, PhpUnit ...)

![[Le principe des tests]]


![[Pasted image 20241102235235.png]]