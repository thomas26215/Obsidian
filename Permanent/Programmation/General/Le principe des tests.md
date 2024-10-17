On écrit des assertions étant des déclarations vérifiant si une condition est vraie. Le résultat peut être succès, échec non fatal et échec fatal :
- **Echec fatal** ⇒ La fonction s'arrête mais le programme continue normalement

**Un test** = une ou plusieurs assertions pour vérifier le comportement d'un morceau de code (par exemple une méthode)
Un cas de test qui a échoué s'il a planté ou si une de ses assertions a échouée. Sinon, le cas de test est un succès

**Une suite de tests** regroupe plusieurs tests pour refléter la structure du code testé. Qd plusieurs tests d'une même suite partagent des objets et des méthodes, on peut les regrouper dans une classe de tests appelée **fixture**

**Un programme de test** peut comporter plusieures suites de tests