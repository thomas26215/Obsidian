---
MOOC: "[[Cours]]"
Ressource: "R3.07 : SQL"
Cours: "Cours 2 : Durabilité"
Date: 
tags: 
Complete: false
Learned: false
---
Doit assurer le contenu même en cas de panne. Si un défaillance de périphérique, il est capable de reconstruire un  étât de la base qui soit cohérent. De même si panne logiciel

>[!attention]
>Il ne revient pas forcément au dernier état de la base

⇒ Si trasfert, soit il termine, soit il annule
Si transaction terminée normalement, confirmée ⇒ On doit voir ses effets sur base. Sinon, pas d'effets sur la base
⇒ On va donc regarder où était la transaction au moment de la panne

**Exemple :** 
Si T1 terminée correctement mais T2 en cours d'exécution
- T1 doit survivre à la panne
- Défaire T2

Méchanisme de backup
