Un **callback** est une fonction que l'on passe en argument à une autre fonction pour qu'elle soit appelée plus tard, souvent quand un évènement se produit ou qu'une action est terminée.
On utilise des callbacks pour gérer des évènements (clicks, saisie, fin de téléchargement ...), pour permettre à un composant d'avertie un autre composant d'un changement ou d'une action, pour rendre le code plus flexible et réutilisable ...

Concrètement :
1. Une fonction A fait le travail
2. On lui passe en paramètre une fonction B (le callback)
3. Quand A a fini son travail, elle appelle B pour lui dire que c'est terminé ou pour lui passer des données
4. B peut alors faire quelque chose avec ces données ou simplement réagir à l'évènement

> [!Example]
> ```pseudo
> fonction A(callback) {
>   // Faire quelque chose
>   callback();
> }
>
> fonction B() {
>   afficher "Travail terminé !";
> }
>
> A(B); // Appelle A et passe B comme callback
> ```
