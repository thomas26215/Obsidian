Les tests doivent être indépendants et doivent pour être répétés aussi souvent que nécessaires
- Chaque test doit tourner de façon isolée sur un objet (utilisation d'objets *mock*)
- Qd un test échoue, on doit pouvoir ne relancer que lui pour déboguer rapidement

Les tests doivent être bien organisés pour refléter la structure du code testé (une suite de test par classe, un cas de test par méthode) - Exception : [[fixture]]

Les tests doivent être portables et réutilisables
Quand les tests échouent, ils ne doivent as interrompre les tests suivants et ils doivent fournir le plus d'informations possibles pour aider au débogage

Finalement, les tests doivent être répides pour pouvoir être rejoués 