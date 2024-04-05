---
MOOC: "[[Programmation]]"
Langage: General
Type: Abstrait
---
Une expression booléenne est une expression dont l'évaluation peut être vraie ou fausse.
Ses opérandes sont de type booléan (variables booléennes, expressions dons les opérandes sont de type primitif). Les opérateurs logiques d'une opération booléan sont &, | et !
- **Egalité** : ==
- **Non égalité** : !=
- **Infériorité stricte** : <
- **Infériorité large** : >
Pour une expression booléenne, il existe la commutativité :
- a & b = b & a
- a | b = b | a
- a ^ b = b ^ a
Et la lois de Morgan :
- !(!a) = a
- !(a | b) = !a & !b
- !(a & b) = !a | !b
