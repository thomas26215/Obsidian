Un conteneur est un processus / ensemble de processus tournant de façon isolée sur un système hôte. C'est l'environnement d'exécution contenant tout ce qui est nécessaire pour faire tourner et isoler ces processus

Il y a une facilité d'accès à tous les outils de développements et une facilité pour le déploiement d'applications

---

# Mécanismes système nécessaires aux conteneurs

## Besoins

=> **Isolation** : Un processus qui est dans un conteneurs ne peut voir que ce qui est à l'intérieur de celui-ci : Il ne voit ni les fichiers, ni les autres processus à l'extérieur de ce conteneur
Il doit également être isolé niveau réseau, c'est à dire détenir sa propre adresse IP. Finalement, un conteneur peut avoir ses propres utilisateurs distincts de l'OS hôte

Un conteneur détient de la RAM, un CPU, un début des E/S disque et un réseau. On peut lui imposer des limites, définir des priorités et faire un comptabilité (Exemple : faire payer à la consommation)

## Mécanismes d'isolation
La commande  `chroot()` isole un processus dans un répertoire spécifique. C'est à dire qu'il modifie son répertoire racine apparent pour faire en sorte que ce processus et ses descendants perçoivent un nouvel environnement racine isolé du reste du système
Cela permet de restreindre l'accès du processus au système de fichiers, c'est ç dire qu'il n'a plus accès aux fichiers et répertoires en dehors de son nouvel environnement racine.

>[!Important]
>Cette restriction est imposée par le noyau Linux pour assurer un niveau d'isolation

Pour que cela fonctionne correctement, il est nécessaire de mettre en place une mini arborescence Linux dans le nouveau répertoire racine. Elle doit contenir les éléments essentiels (`/usr`, `/etc` ...) ainsi que les bibliothèques et exécutables nécessaires au fonctionnement du processus

>[!Example] Exemples d'utilisation
>Améliorer la sécurité en isolant un processus, faciliter la maintenant du système, créer des environnements de test isolés ...

---

Les **Linux namespaces** sont un mécanisme clé du noyau Linux pour isoles différentes ressources pour les processus. Ils sont essentiels pour la virtualisation légère comme dans les conteneurs.
1. **Mount namespace** : Permet à chaque processus d'avoir ses propres points de montage. Utiles pour isoler les systèmes de fichires, notamment les conteneurs. C'est une version plus moderne et plus flexible que ` chroot()`
2. **PID Namespace** : Fournit un espace isolé pour les identifiants de processus (PIDs). Les processus dans ce namespace ne voient que ceux qui y sont crées. Le premier processus a toujours le PID 1, comment un processus init
3. **Network namespace** : Virtualise les fonctionnalités réseau. Chaque namespace peut être complètement isolé et avoir son propre réseau virtuel
4. **User namespace** : Permet d'avoir des utilisateurs et groupes différents de l'OS hôte Cela permet de renforcer la sécurité en isolant les permissions
5. **UTS Namespace** : Isole des mécanismes de communication inter-processus
6. **Cgroup Namespace** : Isole l'arborescence des groupes de contrôle (cgroups) utilisés pour gérer les ressources des processus

- `clone()` créer un nouveau processus dans un namespace indiqué
- `unshare()` détache le processus courant d'un namespace partagé
- `setns()` permet à un preocessus de rejoudre un namespace existant

>[!Example]
>`unshare --map-root-user --pid --fork --mount-proc`

## Mécanisme de gestion de ressources
### Controle group
C'est un groupe de processus auquel on peut imposer des limites, définit des priorités et faire une comptabilité

### Note sur la sécurité
Au départ, certains appels système pouvaient être fait uniquement par le root Grâce aux namespace, ils ont été autorisés pour n'importe quel utilisateur non root Cependant, cela a augmenté la surface d'attaque du noyau Linux car pour les utilisateurs root, ce n'étaient que des bugs

# Présentation de Docker
C'est un gestion gestionnaire de conteneurs C'est un logiciel libre écrit en **Go** et est multi-plateformes