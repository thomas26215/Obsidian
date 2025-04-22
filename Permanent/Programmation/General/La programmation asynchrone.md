Une donnée asynchrone n'est pas disponible immédiatement quand le widget est construit. Contrairement à une donnée synchrone qui est récupérée immédiatement, une donnée asynchrone met du temps à être récupérée / traitée. Par exemple, la récupération d'une donnée depuis une API distante peut prendre du temps en fonction de la connexion de l'utilisateur, de la disponibilité du service API ... Bref, quelque soit la donnée récupérée, chaque donnée prenant du temps à être récupérée est considérée comme donnée asynchrone.

Pour une meilleure expérience utilisateur fluide, nous souhaitons éviter de bloquer l'application lors de la récupération de la donnée asynchrone (Exemple : animation de chargement / Continuer d'utiliser l'application normalement puis afficher le résultat au moment de la récupération de la donnée) : Dart peut récupérer cette donnée en arrière plan ! Ainsi, l'application continue à fonctionner sans interruption

> [!Example] Exemple de fonction asynchrone
> Récupérer les données d'une API concernant des films. Nous souhaitons affichre sur notre page une liste de films avec nom, auteur ... ainsi que l'image du film. Cependant, récupérer et afficher cette image prend généralement + de temps que pour le texte. Ainsi, nous allons immédiatement afficher le texte puis l'image quand celle-ci sera disponible

Grâce à l'asynchronisme, nous pouvons :
- **Améliorer la fluidité de l'application**
- **Gérer les tâches réseau** : Les appels HTTP sont généralement asynchrone car dépendent du réseau
- **Accéder aux bases de données ou aux fichiers** : L'accès aux données peut prendre un certains temps et il est important de ne pas bloque l'appli pendant la récupération de ces données
