---
MOOC: "[[Autre]]"
Thème: Systèmes d'exploitation
Sujet:
tags:
---

Dans le mode texte, deux protocoles sont couramment utilisés :

- **Telnet**: Bien que ce protocole soit ancien, il est de moins en moins utilisé en raison de ses vulnérabilités en matière de sécurité. Les mots de passe et les sessions sont transmis en clair sur le réseau, ce qui en fait une option peu sécurisée. Les machines de l'IUT n'ont généralement pas de serveur Telnet installé.
- **SSH (Secure Shell)**: SSH est un protocole sécurisé qui chiffre les mots de passe et les données de session. Il propose deux modes d'authentification : par mot de passe ou par clé SSH. Des dispositifs de sécurité, tels que fail2ban, sont en place pour bloquer les paquets IP en cas de trois tentatives de mot de passe incorrectes, ce qui renforce la sécurité.
