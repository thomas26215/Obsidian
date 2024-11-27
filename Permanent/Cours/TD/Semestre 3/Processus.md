---
MOOC: "[[Cours]]"
Ressource: "R3.05 : Programmation système"
Cours: "TD1 : Processus"
Date: 
tags: 
Complete: false
Learned: false
---
## Exercice 1
**Question 1**
> Le $a$ serait impossible si le processeur avait uniquement un coeur car avec un coeur,  deux processus ne peuvent pas s'éxecuter en même temps
> Le $c$ car il ne peut pas se terminer à bloqué
> Le $d$ car il ne peux pas passer de prêt à bloqué sans passer par l'état actif



Quand un processus fait un appel au système, il est bloqué. (prints, read, write ...)
- Un processus ne peut pas revenir à un état "prêt" ou "bloqué" après avoir été marqué comme "mort".
- Les transitions doivent respecter un ordre logique :
    - "Prêt" (●) → "Actif" (—).
    - "Actif" (—) → "Bloqué" (○) ou "Mort" (×).
- Un processus ne peut pas être simultanément dans plusieurs états.



**Question 2**
> Le processus 1 s'exécuterait sur 2 unités de temps
> Le processus 2 s'écexuterait sur 7 unités de temps

**Question 3**
> Le processus 1 s'éxecuterait sur 3 unités de temps
> Le processus 2 s'éxecuterait sur 6 unités de temps

**Question 4**
> Le processus 1 s'exécuterait sur 1 unités de temps
> Le processus 2 s'exécuterait sur 8 unités de temps

**Question 5**
> 