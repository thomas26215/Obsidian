---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
  - status_finish
  - note_permanent
---
Plusieurs utilisateurs peuvent utiliser le système simultanémet. Un utilisateur peut lancer plusieurs logiciels en même temps. L'éxecution d'un logiciel donne naissance à un tâche ou processus qui est donc un programme en train de s'éxecuter. C'est une entité dont le noyeau Linux contrôle l'état, de la vie à la mort
- **Système à temps partagé** : Le processus est partagé entre plusieurs processus concurrents
- **Système multi-préemptif** : L'ordonnanceur peut interrompre de force un processus pour redonner le contrôle du processeurs au noyeau Linux ou à un autre processeur

Les processus sont crées par clonae d'un processus existant. Ainsi, les processsu sont organisés en arbre. Il est possible de le visualiser grâce aux commandes
- `ps`
- `pstree`
- `top` → Se réactualise en instantané (utile pour voir qui consomme le plus en terme de processeur)

On peut mettre fin à un processus :
- `kill`
- `killall`

# Attributs d'un processus
- **PID** : Identifiant unique unmérique
- **PPID** : Numéro de son père
- **UID** : Utilisateur au nom duquel le processus s'exécute
- **GID** : Goupe auquel le processus est rattaché
- **Priorité** : Elle va influencer sur la fréquence à laquelle l'ordonnanceur donnera le processeur au processus. peut varier de `-20` à `19`, mais est à `0` par défaut. Cette priorité peut être modifiée par la commande `nice` et `renice`. Un utilisateur de base ne peut pas modifier cette priorité