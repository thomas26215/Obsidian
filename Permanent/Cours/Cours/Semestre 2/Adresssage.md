---
MOOC: "[[Cours]]"
Ressource: R2.04a  :Fonctionnement bas niveau
Cours: "Cours 1 : Adressage"
Date: 2024-02-07
tags: 
Complete: false
Learned: false
---
11- **Adressage immédiat :** La données est contenue dans l'instruction
  ⇒ MOVE.W *#10*, %D0
- **Adressage direct :** La valeur est rangée dans un registre
  ⇒ NEG *%D1*
- **Adressage absolu :** On connaît à l'avance l'adresse de la donnée qu'on manipule
  ⇒ MOVE.W *# 0xFFFF*
- **Adressage indirect :** Comme pour adressage absolu mais la value d'adresse est contenue dans un registre d'adresse
  ⇒ MOVE.W *(%A1)*, %D0 - D0.W = MEM(%A1)
- **Adressage indirect avec déplacement :** Même principe que pour adressage indirect mais on raoute un déplacement. Le déplacement peut être positif ou négatif. Ainsi, on ne prendra pas directement la valeur associée à l'adresse mais on prendra la valeur %A1 + x
  ⇒ MOVE.W 4(%A1), %D0
- **Adressage indirect indexé** : Comme pour adressage avec déplacement, sauf que le déplacement ne se fait pas avec une valeur brute mais avec un registre de données
  MOVE.W (%A1, %D0), %D1
- **Adressage indirect indexé avec déplacement :** Une combinaison des deux précédants
  ⇒ MOVE.W4(%A1, %D0), %D1
- **Adressage indirect post incrémenté :** Une fois que l'on a exécuté l'instruction, l'adresse mémloire rangée dans Ai est incrémentée :
	- .B : +1
	- .W : +2
	- .L : +4
	⇒ MOVE.W (%A1)+, %D0
- **Adressage indirect pré décrémenté :** Même principe que pour le post incrémenté sauf qu'il qu'on lui retire 1 AVANT l'exécution de l'instruction
  ⇒ MOVE.W -(%A1), %D0
- **Calcul d'adresse effective :** Ca sert à ranger l'adresse exacte d'une donnée en mémoire dans un registre 
  ⇒ LEA `<ea>`, %An (Exemple : LEA 2(%A1), %A0)
- **Calcul d'adresse effective :** Incrémenter ou décrémenter une valeur d'adresse par addition ou soustraction
  ⇒ ADDA.L `<ea>`, %An :Addition
  ⇒ SUBA.L `<ea>`, %An : Soustraction

