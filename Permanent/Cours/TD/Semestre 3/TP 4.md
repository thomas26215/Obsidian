---
MOOC: "[[Cours]]"
Ressource: "R3.06 : Réseaux"
Cours: "TP 4 : Usages du chiffrement : protocole SSH et logicielOpenSSH"
Date: 
tags: 
Complete: false
Learned: false
---
# Exercice 1
**Question 2 :**
> 3. L'avertissement de SSH indique que l'authenticité de l'hôte 'transit' ne peut pas être établie. Il affiche l'empreinte de la clé ECDSA du serveur
> 4. Oui l'empreinte de le clé est bien la même que sur le site
> 5. Ce moyen offre un système de sécurité modéré. En effet, cela repose sur la confiance accordée à la page Web qui pourrait être potentiellement compromise. Cette méthode reste tout de même courante pour un premier niveau d'authentification
> 8. Les trois parties sont :
> 	- L'identifiant de la machine (nom d'hôte / adresse IP)
> 	- Le type de clé
> 	- La clé publique encodée en base64
> 9. Les deux lignes ajoutées correspondent probablement à deux clés différentes pour le même hôte. Il est courant que les serveurs aient plusieurs types de clés (ex: RSA, ECDSA, Ed25519) pour assurer la compatibilité avec différents clients.
> 10. Lors d'une nouvelle connexion SSH vers transit, la confirmation n'est plus demandée car SSH a déjà enregistré la clé du serveur dans le fichier known_hosts. Il peut donc vérifier automatiquement l'authenticité du serveur sans intervention de l'utilisateur.


**Question 3 :**
> 2. La version locale d'OpenSSH est OpenSSH_9.2p1 Debian-2+deb12u3
> 3. La version distante d'OpenSSH est également OpenSSH_9.2p1 Debian-2+deb12u3
> 5. :
> 	- Protocoles d'échanges de clés (KEX algorithms) :  
> 	  Client : [sntrup761x25519-sha512@openssh.com](mailto:sntrup761x25519-sha512@openssh.com), curve25519-sha256, [curve25519-sha256@libssh.org](mailto:curve25519-sha256@libssh.org), ecdh-sha2-nistp256, ecdh-sha2-nistp384, ecdh-sha2-nistp521, diffie-hellman-group-exchange-sha256, diffie-hellman-group16-sha512, diffie-hellman-group18-sha512, diffie-hellman-group14-sha256, ext-info-c, [kex-strict-c-v00@openssh.com](mailto:kex-strict-c-v00@openssh.com) Serveur : [sntrup761x25519-sha512@openssh.com](mailto:sntrup761x25519-sha512@openssh.com), curve25519-sha256, [curve25519-sha256@libssh.org](mailto:curve25519-sha256@libssh.org), ecdh-sha2-nistp256, ecdh-sha2-nistp384, ecdh-sha2-nistp521, diffie-hellman-group-exchange-sha256, diffie-hellman-group16-sha512, diffie-hellman-group18-sha512, diffie-hellman-group14-sha256, [kex-strict-s-v00@openssh.com](mailto:kex-strict-s-v00@openssh.com)
> 	  - Algorithmes de chiffrement (ciphers ctos et stoc) :  
> 	   Client et serveur : [chacha20-poly1305@openssh.com](mailto:chacha20-poly1305@openssh.com), aes128-ctr, aes192-ctr, aes256-ctr, [aes128-gcm@openssh.com](mailto:aes128-gcm@openssh.com), [aes256-gcm@openssh.com](mailto:aes256-gcm@openssh.com)
> 	   - Algorithmes MAC (MACs ctos et stoc) :  
> 	     Client et serveur : [umac-64-etm@openssh.com](mailto:umac-64-etm@openssh.com), [umac-128-etm@openssh.com](mailto:umac-128-etm@openssh.com), [hmac-sha2-256-etm@openssh.com](mailto:hmac-sha2-256-etm@openssh.com), [hmac-sha2-512-etm@openssh.com](mailto:hmac-sha2-512-etm@openssh.com), [hmac-sha1-etm@openssh.com](mailto:hmac-sha1-etm@openssh.com), [umac-64@openssh.com](mailto:umac-64@openssh.com), [umac-128@openssh.com](mailto:umac-128@openssh.com), hmac-sha2-256, hmac-sha2-512, hmac-sha1
> 6. Dans ce contexte, MAC signifie "Message Authentication Code". C'est un code utilisé pour authentifier et vérifier l'intégrité des messages échangés.
> 7. "ctos" signifie "client to server" (du client vers le serveur) et "stoc" signifie "server to client" (du serveur vers le client).


**Question 4 :**
> 1. `ssh-keygen -t rsa -b 4096`
> 2. Les fichiers générés sont généralement `id_rsa` (clé publique) et `id_rsa.pub` (clé privée)
> 3. Les permissions Unix sur ces fichiers sont restrictives (généralement 600 pour la clé privée et 644 pour la clé publique) car seul le propriétaire doit avoir accès à la clé privée pour des raisons de sécurité
> 4. La clé publique est généralement encodée en base64
