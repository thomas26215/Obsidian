---
MOOC: "[[Autre]]"
Thème: Réseaux informatiques
Sujet: Virtualisation
tags: 
Complete: false
Learned: false
---
Virtualisation de stockage dans un OS classique
- **Exemple 1 :** Linux et LVM2. Volumes physiques (DAS) sont regroupés en groupes de volumes, puis en volumes logiques. Ces volumes logiques sont ensuite partitionnés et formatés
- **Exemple 2** : Windows et *Storage Spaces*

Exemples de virtualisation avec [[NAS]] :
- Machine sans stockage (*diskless*) qui boote par réseau sur un [[SGF - Arborescence et système de fichiers|SGF]] NFS (*Network File System*)

Exemple de virtualisation avec [[SAN]]
- Réseau de  stockage sur infrastructure de type Fibre Channel, Ethernet ou Infiniband
- Protocole d'accès iSCSI sur [[L'utilité des adresses IP|IP]] et est le précurseur de SAS
- Ce stockage distant est mis à disposition d'un cluster de serveur physiques ou d'hyperviseurs