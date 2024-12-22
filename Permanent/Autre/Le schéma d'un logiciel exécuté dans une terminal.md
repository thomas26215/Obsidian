---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet: terminal
tags: []
---

## Schéma d'un logiciel exécuté dans un terminal

Etat initial avant lancement :

- Processus : terminal, shell
- Plomberie initiale entre terminale et shell - **Connexions** : clavier → terminal → shell - **Connexions** : Shell → terminale → écran
  Etat après lancement logiciel en avant-plan :
- Processus : terminal, shell, logiciel
- Plomberie après lancement :
    - **Connexions** : clavier → terminal → logiciel
    - **Connexions** : logiciel → terminale → écran

