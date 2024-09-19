# Exercice 1
1. host transit.iut2.univ-grenoble-alpes.fr
	transit.iut2.univ-grenoble-alpes.fr is an alias for transit.iut2.upmf-grenoble.fr.
	transit.iut2.upmf-grenoble.fr has address 193.55.51.227
2. .
⇒ nslookup iut2.univ-grenoble-alpes.fr 193.55.51.34
Server:         193.55.51.34
Address:        193.55.51.34#53

Name:   iut2.univ-grenoble-alpes.fr
Address: 195.83.24.194

⇒ nslookup www.univ-grenoble-alpes.fr 193.55.51.34
Server:         193.55.51.34
Address:        193.55.51.34#53

Non-authoritative answer:
www.univ-grenoble-alpes.fr      canonical name = ksup.u-ga.fr.
Name:   ksup.u-ga.fr
Address: 195.83.24.194


⇒ nslookup ksup.u-ga.fr 193.55.51.34
Server:         193.55.51.34
Address:        193.55.51.34#53

Non-authoritative answer:
Name:   ksup.u-ga.fr
Address: 195.83.24.194

a. Le serveur DNs no 1 m'a répondu par le num de port 53
	Le nom et son domaine sont localhost
b. 
1. Une réponse non autoritaire dans les requêtes DNS (Domain Name System) indique que la réponse provient d'un serveur DNS qui n'est pas le serveur de noms autoritaire pour le domaine interrogé. Cela peut être dût à une réponse mise en cache ou dût à une réponse récursive
2. Adresses IP des sites :
	- www.univ-grenoble-alpes.fr : 195.83.24.194
	- iut2.univ-grenoble-alpes.fr : 195.83.24.194
	- ksup.u-ga.fr : 195.83.24.194
3. Valeur du champ canonical name pour les deux premiers sites :
	- www.univ-grenoble-alpes.fr : ksup.u-ga.fr
	- iut2.univ-grenoble-alpes.fr : Pas de canonical name indiqué
4. La mention "Canonical Name" signifie que le nom de domaine est un alias qui pointe vers un autre nom de domaine considéré comme le nom canonique (ou principal).
5. Le vrai nom du serveur dans tous les cas semble être ksup.u-ga.fr, car c'est le nom canonique vers lequel pointe www.univ-grenoble-alpes.fr et qui a directement l'adresse IP associée.
6. On peut en déduire qu'il n'y a pas de relation biunivoque entre noms de machines et adresses IP. Plusieurs noms de domaines peuvent pointer vers la même adresse IP.
6. L'intérêt de cette organisation est :
	- Flexibilité : Permet d'avoir plusieurs noms de domaines pour un même serveur
	- Facilité de gestion : En cas de changement d'adresse IP, il suffit de mettre à jour un seul enregistrement (le nom canonique)
	- Répartition de charge : Possibilité de diriger plusieurs noms de domaines vers différents serveurs selon les besoins

3. **dig**
	1. Différentes sections :
		- <mark style="background: #FFB86CA6;">QUESTION</mark> : Affiche la requête DNS envoyée : nom de domaine interrogé et type d'enregistrement
		- <mark style="background: #FFB86CA6;">ANSWER</mark> : Réponse directe de la requête
		- <mark style="background: #FFB86CA6;">AUTHORITY</mark> :Liste des noms faisant autorité pour le domaine interrogé. Indique quels serveurs DNS sont responsables de fournir les informations pour ce domaine
		- <mark style="background: #FFB86CA6;">ADDITIONAL</mark> : Fournir des informations supps pouvant être utiles, mais non demandées  directement. Elles peuvent par exemple contenir les adresses IP des serveurs de noms listés dans la section <mark style="background: #FF5582A6;">AUTHORITY</mark>
	2. La cinquième colonne de la section **ANSWER** contient `ix1-pv-lbl-vip-194-57-3-7.renater.fr.`
	3. Les sigles
		-  <mark style="background: #FFB86CA6;">CNAME ⇒ Canonical Name</mark> : Créer un alias pour un nom de domaine ⇒ Permet de rediriger un nom de domaine vers un autre
		- <mark style="background: #FFB86CA6;">A ⇒ Adresse</mark> : Associe un nom de domaine à un adresse IPv4. Enregristrement le plus courant pour la résolution de noms en adresse IP
		- <mark style="background: #FFB86CA6;">AAAA ⇒ IPv6 adress</mark> : Similaire à l'enregistement A, mais pour les adresses IPv6
		- <mark style="background: #FFB86CA6;">NS ⇒ Name Server</mark> : Spécifie les serveurs de noms autoritaires pour un domaine
	4.  SOA signifie "Start of Authority". Le serveur primaire est `ns1.renater.fr`
	5. Dans la section **ANSWER**, le nombre de la seconde colonne décrémente chaque seconde

# Exercice 2
1. 195.221.57.62 : pelvoux.iut2.upmf-grenoble.fr
2. La commande nslookup représente l'adresse IP donnée en paramètre sous la forme d'une adresse IP inversée suivie de ".in-addr.arpa".
3. Dans la section **ANSWER**, la commande dig représente l'adresse IP sous la forme `IP.in-addr.arpa`
4. Un enregistrement PTR (Pointer Record) est utilisé pour les recherches DNS inversées. Il permet d'associer une adresse IP à un nom de domaine￼￼.

# Exercice 3
1. iut2-dg-ns2.iut2.upmf-grenoble.fr
   meije.iut2.upmf-grenoble.fr.
2. Ces serveurs ne sont probablement pas dans le même réseau physique. C'est possible car :
	- Cela permet une redondance et une meilleure disponibilité du service DNS.
	- Les serveurs DNS peuvent être géographiquement distribués pour améliorer les performances.
3. Les 4 dernières commandes correspondent à des requêtes DNS pour obtenir les serveurs de noms (NS) des domaines suivants :
	- univ-grenoble-alpes.fr
	- fr (domaine de premier niveau pour la France)
	- . (domaine racine)
4. Le "." dans la dernière commande représente le domaine racine du DNS.
5. D'après la dernière commande, il existe 13 serveurs DNS pour le domaine racine.
6. La particularité de leur nom est qu'ils sont nommés de a.root-servers.net à m.root-servers.net.
```text
                    . (a.root-servers.net)
                   / \
                  /   \
         fr (d.nic.fr) org (a0.org.afilias-nst.info)
         /             \
univ-grenoble-alpes.fr  kernel.org
(eip1.u-ga.fr)         

in-addr.arpa (a.in-addr-servers.arpa)
    |
  195.in-addr.arpa
    |
  221.195.in-addr.arpa
    |
  57.221.195.in-addr.arpa
```

# Exercice 4
1. Le premier serveur DNS interrogé est le serveur racine (root server). Cela est logique car la résolution DNS commence toujours par les serveurs racine qui sont au sommet de la hiérarchie DNS. Ils dirigent ensuite vers les serveurs de domaine de premier niveau (TLD).
2. Les différents serveurs DNS qui ont répondu sont :
	- Un serveur racine (k.root-servers.net)
	- Un serveur TLD pour le domaine .fr (d.nic.fr)
	- Un serveur autoritaire pour qwant.fr (ns-224-a.gandi.net)
3. Le mécanisme utilisé pour relayer des requêtes DNS est une résolution récursive. Voici un schéma simplifié du processus :

```text
Client DNS -> Serveur DNS local
    |
    v
Serveur racine (.root-servers.net)
    |
    v
Serveur TLD (.fr - d.nic.fr)
    |
    v
Serveur autoritaire (qwant.fr - ns-224-a.gandi.net)
    |
    v
Réponse finale (www.qwant.fr CNAME webredir.gandi.net)
    |
    v
Client DNS
```

# Exercice 5
`AdresseIP "1..*" --- "1..*" NomMachine`

# Exercice 6
1. Utilisation du serveur DNS d'Orange (194.2.0.20 ou 194.2.0.50) :
www.univ-grenoble-alpes.fr : Probablement une réponse avec l'adresse IP du site.
www.kernel.org : Probablement une réponse avec l'adresse IP du site.
sci-hub.se : Il est possible que cette requête ne renvoie pas de résultat ou renvoie une adresse IP de blocage.
2. Utilisation du serveur 1.1.1.1 de Cloudflare :
www.univ-grenoble-alpes.fr : Réponse avec l'adresse IP du site.
www.kernel.org : Réponse avec l'adresse IP du site.
sci-hub.se : Probablement une réponse avec l'adresse IP réelle du site.
3. Conclusions :
La principale différence attendue concerne probablement la requête pour sci-hub.se. Le serveur DNS d'Orange, étant un fournisseur d'accès Internet français, est susceptible de bloquer ou de rediriger les requêtes vers des sites considérés comme illégaux ou problématiques en France.

# Exercice 7
