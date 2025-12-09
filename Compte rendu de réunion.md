**Compte rendu de réunion du Mardi  9 décembre de 8h à 10h**
**Ordre du jour** : Comment éviter de reproduire une suppressino de base de données ?

**Membres de la réunion** :
- M.Mathias
- M.Valentin
- M.Maxime
- M.Corentin
- M.Adam
- M.Corentin

Début de la réunion après présentation à 8h12. 

# 8h12 : Présentation de solutions

**Solution 1 (BDD) : Ruteck** : Bibliothèque Python
**Ajouts de triggers** : On peut programmer des blocages
**Backup** : Une commande backup. Avec serveurs externes mais lesquels prendre ?
**PCA**
**Tests unitaires et tests d'intégrations** : Mettre des tests en place pour mettre en place des actions pour vérifier que ce qui est mis en backend ne fait pas des suppressions dans la BDD
8h17 Noah propose avec l'équipe la discussion sur les normes ISO

8h19, ils passent à la partie frontend
Mathis amène l'idée qu'il n'y a rien à faire côté Frontend
Adam contredit avec la mise en place de garde fou (double confirmation) pour éviter à l'utilisateur de rentrer de mauvaises informations par erreur
8h21, Mathias propose de mieux configurer les rôles ainsi qu'aux problèmes d'injection
8h22, Noah propose de mettre des logs. Mathias contredit mais propose plutot un dahsboard
8h24, Corentin propose de séparer environnement de test, production, environnement
8h25, Adam propose un mode bac à sable pour permettre à l'utilisateur de prendre en main l'application
8h26, Valentin et Corentin discutent de l'authentification

---

8h28 Discussion sur les priorités :
Backup priorisé
Confirmation suppression priorisé. Valentin dis que c'est déjà à peu près fait, donc ca prendrait seulement une demi journée
8h29 Maxime dis qu'il a déjà un fichier backup, donc seulement deux jours
8h31 Valentin parle d'un nouveau serveur (production, test). Valentin estime en deux jours le coût
Maxime explique à Valentin qu'il peut etre interessant de mettre en place Rutech et pas si coûteux en terme de temps
8h34 Valentin réévoque l'idée d'un deuxième serveur pour le test
8h35. L'ensemble de l'équipe tend à s'accorder que ces modifications ne prendront pas longtemps

Noah demande concernant le recrutement et Mathias informe que pas encore de CV mais que oui, nécessaire car beaucoup de travail

8h37 FIN DE REUNION 