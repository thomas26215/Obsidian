L'ordonnanceur a pour objectif de classer les processus prêts
⇒ Il doit choisir quel processus est prêts quand le CPU devient libre. Egalement, il doit se demander s'il faut retirer un processus actif pour l'accorder à un prêt

Il doit quand même respecter quelques critères :
- Chaque processus doit avoir un accès correct au processus
- Un certain rendement : il doit occuper le CPU le plus possible (entre 40 et 90%)
- Débit : nombre de travaux terminés par unité de temps (1 à 10/s)
- temps de réalisation d’un job : temps entre sa soumission et sa terminaison
- temps d’attente : uniquement temps passé dans l’état prêt
- temps de réponse : temps entre requête et réponse (interactif)
- prise en compte de la nature différente des processus (noyau/user)