- Dans la page modification `ModificationsController` et `modifications.fxml`,Si un champs n'est pas rentré quand on clique sur valider, ne pas passer à la suite et mettre les TextField en encadré rouge. 1 exemple dest déjà donné dans la classe `ModificationController`, faire poue les autre
  ⇒ Faire de même pour le fichier Création : `CreationController` et `Creation.fxml`
- Réorganiser les fonctions : D'abord les attributs puis les fonctions utiles et enfin les getters et setters. Si les attributs sont : att1 att2 att3 getter1 setter1 getter2 setter2 getter3 setter3. Si des méthodes courtes en plus (ex : addatt1) le mettre à la suite du gette + setter correspondant
- Réagencer les Labels de l'affichage générale de la brocante (`MainController` et `MainView.fxml`)
- Rendre fonctionnel le bouton retour de `ModificationController` ⇒ Méthode `app.Affichage();`
- Dans `ModificationsController` S'assurer que le TextField reprenne la date actuelle si présente (Récup la date en `String` : `organisation.getDate()`)
- FAIRE LA CLASSE `BUVETTE`
- FAIRE LA CLASSE `MATERIEL` - NOUVELLE FENETRE (A GAUCHE) POUR AJOUTER DU MATERIEL DISPONIBLE AU VIDE GRENIER, NON A UN VENDEUR

- **FAIRE LES TESTS UNITAIRES** ⇒ **ELIOTT ET JULIAN** ⇒  A TERMINER AVANT CE SOIR
- **FAIRE LES LOGGERS** ⇒ **Joshua** A TERMINER AVANT MIDI
- **AMELIORER LE DESIGN DES INTERFACES PUIS TOUT PASSER EN BOUTON CE QUI EST NECESSAIRE** ⇒ **BRAYAN** ⇒  A TERMINER AVANT MIDI