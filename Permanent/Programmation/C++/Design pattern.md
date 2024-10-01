Ca décrit un problème générique, récurrent et sa solution sont des **modèles de conception réutilisable** mais qui doivent quand même être adaptés
On parle aussi de forme de conception, pattern ...

Ca permet de :
- trouver la bonne représentation objet et en particulier de bien choisir la granularité de ses objets
- spécifier l'interface des objets
- spécifier l'implémentationd es objets
- Réutiliser une solution générique en l'adaptant à un besoin spécifique
**Référence** : Design patterns : Elements of reusable Object-Oriented software



**Pattern** = Résoudre un problème de conception, ses solutions et ses conséquences. Le nom doit être court et très descriptif
1. Le **problème** décrit dans quelles circonstances le pattern doit être appliqué. Description de la problématique et de son contexte
2. La **solution** = 
3. Les **conséquences** =


# Le pattern Composite
⇒ Assembler des objets selon une structure d'arbres pour représenter des hiérarchies et manipuler de façon transparente par une interface uniforme les aobjets atomiques et les objets composés

<mark style="background: #BBFABBA6;">Exemple</mark> : Dans un éditeur graphique, on veut laisser la possibilité à l'utilisateur de grouper des figures simples pour former une structure complexe qui lui-même peut être regroupé à d'autres figures simples. La pattern **Composite** permet de régler ce problème