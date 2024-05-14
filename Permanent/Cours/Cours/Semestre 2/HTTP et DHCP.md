Hypertext Transfert Protocol (HTTP) inventé en 1989 par Tim Berners-Lee avec les URLs et le langage  HTML pour créer le WWW (World Wide Web)
URL : adresse identifiant toute ressource sur le web.
Synthaxe : <mark style="background: #FF5582A6;">protocole</mark>  <mark style="background: #ADCCFFA6;">nomserveur ou adresse IP</mark> <mark style="background: #BBFABBA6;">/chemin ressources</mark>
→ <mark style="background: #FF5582A6;">http://</mark><mark style="background: #ADCCFFA6;">www.ietf.org</mark>
→ <mark style="background: #FF5582A6;">http://</mark><mark style="background: #ADCCFFA6;">www.iut2.univ-grenoble-alpes.fr</mark><mark style="background: #BBFABBA6;">/index.html</mark>

Format requête : 
<mark style="background: #FF5582A6;">Ligne de commande (Commande, URL, Version de protocole)</mark>
<mark style="background: #ADCCFFA6;">En-tête de requête</mark>
[Ligne vide]
<mark style="background: #BBFABBA6;">Corps de requête</mark>

# DHCP
Dynamic Host Configuration Protocol (DHCP) configurer dynamiquement une station connectée au sein d'un LAN
Sert principalement à distribuer des adresses IP sur un réseau
- filaire
- wifi
- UDP

**Nom de domaine :** Alias sur une ou plusieurs adresses IP
`ietf.org → 50.223.129.194`
`debian.org → 128.31.0.62`, `130.89.148.77`
Un Dn est plus simple à retenir et à référencer qu'une adresse IP

Un domaine peut créer des sous-domaines :
`iut2.univ-grenoble-alpes.fr`
→ `iut2` est un nom de sous-domaine dépendant entièrement du domaine principale
Pour conculter noms de domaine : `whois`

**Domaine :** Ensemble de machinesreliés à Internet et possédant une caractéristique communie : Il est structuré de manière hiérarchique
- `.fr` → Tous les équipements hébergeant des activités en France. C'est un domaine de premier niveau ou TLD
- `univ-gernoble-alpes.fr` → Tousl es équipements hébergeant des activités dans le compte de l'UGZ

![[Pasted image 20240514084631.png]]

Gestion des noms de domaines faite par zone
TLD gérés par Registres
- Pour domaine : `.fr`, `.re` .. AFNIC
Noms de domaines enregistrés par Registraires (OVH, Gandi) interagissant avec registres


# Comment traduire un nom de domaine en adresse IP
**Exemple :** `de.wikipedia.org`
1. Serveur DNS détermine d'abord qui fait autorité pour `.` (zone racine du DNS)
2. Demande ensuite qui fait autorité pour `.org`
3. Demande ensuite à ces serveurs DNS qui fait autorité pour `wikipedia.org`
4. Demande ensuite adresse IP
5. `185.15.58.225` et d'autres infos ensuite envoyéex à machine hôte

>[!tip]
>Toutes les requêtes sont envoyées au port 53

La résolution se fait en utilisant le logiciel `nslookup nomDomaine`


# Principe du SMTP
Simple mail transfert protocol
- TCP/25
- Protocole textuel
- Dedié à l'acheminement
	- Ne s'occupe pas de la récupération
- Quelques commandes : `EHLO`, `MAIL FROM`, `RCPT TO` ...
Données codées en ASCII


⇒ Architecture en niveaux car architecture du réseau fait uniquement appel aux programmes du niveau strictement inférieur et est encapsulé par l'inférieur