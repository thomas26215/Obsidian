---
MOOC: "[[Cours]]"
Ressource: "R3.06 : Réseaux"
Cours: "TP 5 : Usages du chiffrement : certificats SSL et HTTPS"
Date: 
tags: 
Complete: false
Learned: false
---
# 1.2
- L'adresse du site web couverte par le certificat est :  
    authentication.univ-grenoble-alpes.fr
- L'autorité qui a vérifié le certificat (champ "Nom de l'émetteur") est :  
    GEANT OV RSA CA 4
2. La vérification du certificat par une autorité de certification est importante pour plusieurs raisons :
	- Elle permet de **crypter** les données échangées entre le navigateur de l'utilisateur et le serveur web, assurant ainsi la confidentialité des informations sensibles
	- Elle **valide l'identité** du site web, rassurant les visiteurs sur la légitimité de la plateforme
	- Elle contribue à **prévenir les attaques de phishing** en vérifiant l'authenticité du site web
	- Elle **renforce la crédibilité** du site web auprès des utilisateurs, démontrant que des mesures sont prises pour protéger leurs données
	- Elle aide à la **mise en conformité** avec les réglementations sur la protection des données personnelles
3. Ils utilisent une clé de chiffrement asymétrique. La taille de la clé de chiffrement permet de déterminer la complexité à craquer le système de chiffrement. Plus la clé de chiffrement est longue, plus elle est difficile à craquer. Une longue clé de chiffrement permet donc une meilleure résistance face aux nouveaux systèmes de crackage
4. Le certificat expire le 8 janvier 2025. Il est nécessaire d'avoir une date d'expiration pourr assurer la màj des cerificats avec les normes mis à jour. Cela permet également de limite les risques en cas de compromission des certificats obsolètes
5. L'information "SHA-384 avec chiffrement RSA" indique que le site utilise le système de hachage SHA-384 pour créer l'empreinte numérique du certificat et que RSA est l'algorithme de chiffrement asymétrique utilisé pour signer cette empreinte 

---
1. Analyse de la chaîne de certificat
	1. "authentication.univ-grenoble-alpes.fr"  
	   ↑ vérifié par
	2. "GEANT OV RSA CA 4" 
	   ↑ vérifié par
	3. "USERTrust RSA Certification Authority"
2. Cette configuration est nécessaire pour plusieurs raisons :
	1. Point de confiance : Préinstallé dans les niveaux et systèmes d'exploitation comme une ancre de confiance ultime
	2. Fin de la chaîne : Il marque la fin de la chaîne de certification, évitant ainsi une régression infinie de vérifications
	3. Contrôle
	4. Longévité

# 2.1
3. La CSR contient :
	- La clé publique correspondant à la clé privée générée
	- Les informations d'identification fournies (ville, organisation, etc.)
	- La signature numérique créée avec la clé privée
Cette requête devrait être envoyée à une autorité de certification (CA) pour obtenir un certificat SSL/TLS signé
1. Le coût d'une certification varie selon le type de certificat et le fournisseur. Par exemple, chez DigiCert, un certificat SSL standard peut coûter entre 200$ et 400$ par an environ.
2. Comparaison avec Let's Encrypt :
	- Let's Encrypt fournit des certificats gratuits
	- Les certificats Let's Encrypt sont valides pendant 90 jours
	- Ils doivent être renouvelés automatiquement tous les 60-90 jours

# 2.2
Lorsqu'un navigateur tente de se connecter à un site utilisant un certificat auto-signé, plusieurs problèmes peuvent survenir :

1. Avertissements de sécurité : Les navigateurs afficheront des avertissements de sécurité explicites, informant l'utilisateur que la connexion n'est pas sécurisée
2. Perte de confiance des utilisateurs : Ces avertissements effraient souvent les utilisateurs, les incitant à quitter le site immédiatement[
3. Baisse du trafic : Environ 9 utilisateurs sur 10 renoncent à accéder à un site web lorsqu'ils voient une alerte de sécurité
4. Risque d'attaques : Les utilisateurs ne peuvent pas distinguer un certificat auto-signé légitime d'un faux créé par des pirates, augmentant le risque d'attaques de type "Man in the Middle"
5. Blocage ou restriction : Certains navigateurs modernes comme Chrome et Safari peuvent bloquer ou restreindre l'accès aux sites utilisant des certificats auto-signés
6. Perturbations et erreurs : De nombreux services et outils refuseront de se connecter via des certificats auto-signés, causant des perturbations dans le fonctionnement normal du site
7. Problèmes d'intégration : Les intégrations avec d'autres services ou applications peuvent échouer en raison du rejet du certificat auto-signé
8. Impact sur le référencement : La baisse du trafic due aux avertissements de sécurité peut entraîner une diminution du classement du site dans les résultats des moteurs de recherche

# 3.2
- Firefox vous prévient que le site est dangereux car :
    - Le certificat utilisé est auto-signé et non émis par une autorité de certification reconnue
    - Le navigateur ne peut pas vérifier l'authenticité du site, ce qui représente un risque potentiel pour la sécurité
- Pour constater que c'est un certificat auto-signé :
    - Dans les détails du certificat, le champ "Émetteur" et le champ "Sujet" contiennent les mêmes informations
    - Il n'y a pas de chaîne de certification menant à une autorité de certification racine reconnue
- La démarche pour que Firefox accepte d'accéder au site sans exception serait :
    - Importer le certificat racine auto-signé dans le magasin de certificats de Firefox.
    - Marquer ce certificat comme digne de confiance pour identifier les sites web.
    - Alternativement, obtenir un certificat émis par une autorité de certification reconnue pour le site

# 4
1. Messages HelloClient et HelloServer :
	- Ces messages font partie de la phase de "handshake" TLS.
	- Le ClientHello propose une liste de suites cryptographiques supportées par le client.
	- Le ServerHello répond en sélectionnant une suite cryptographique parmi celles proposées
2. 1. Messages HelloClient et HelloServer :
	- Ces messages font partie de la phase de "handshake" TLS.
	- Le ClientHello propose une liste de suites cryptographiques supportées par le client.
	- Le ServerHello répond en sélectionnant une suite cryptographique parmi celles proposées