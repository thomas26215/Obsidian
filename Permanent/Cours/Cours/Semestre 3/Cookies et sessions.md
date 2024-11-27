---
MOOC: "[[Cours]]"
Ressource: "R3.01 : Développement Web"
Cours: "Chapitre 9 : Cookies et sessions"
Date: 
tags: 
Complete: false
Learned: false
---
Les cookies permettent de retenir les utilisateurs sur un utilisateur. C'est une solution pour grader son état cat le protocole HTTP est sans état. Il es tintroduit au HTTP (avec Netscape). Cela permet également d'identifier une navigation de manière unique
C'est le serveur qui envoie la valeur initiale du cookie. Le navigateur doit alors systématiquement renvoyer le cookie 
>[!info] Sécurité
>Le stockage n'est pas sécurisé car c'est généralement stocké dans un fichier texte

- Création et envoie d'un cookier
	- Crée un header HTTP manuellement (déconseillé)
	- Utiliser `setcookie(nom, valeur)`
- Cookie dans l'entête HTTP
	- Utiliser la fonction avant la sortie  de tout code HTML
- Lecture d'un cookie
	- `$_COOKIE[nom]` ⇒ Récupérer la valeur
	- Tableau en lecture seule


>[!info]
>Il faut lister le tableau pour avoir la liste complète des cookies

- Pour effacer un cookie ⇒ `setcookie[]` - Sans valeur