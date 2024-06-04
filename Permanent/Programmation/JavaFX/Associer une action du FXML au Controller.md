En JavaFX, il est possible de définir des actions sur des boutons, images, et autres composants de l'interface utilisateur. Ici, nous allons prendre l'exemple d'un bouton.

## Définition des attributs dans le fichier FXML

Pour définir une action à effectuer lorsqu'on clique sur un bouton, il suffit de définir un attribut `onAction` dans le fichier FXML :

xml

Copy code

`<Button fx:id="button0_0" mnemonicParsing="false" onAction="#handleButtonAction" GridPane.rowIndex="0" GridPane.columnIndex="0"/>`

- **`fx:id="button0_0"`** : Identifiant unique pour ce bouton, permettant de le référencer dans le contrôleur Java.
- **`mnemonicParsing="false"`** : Désactive le parsing des mnémoniques (raccourcis clavier).
- **`onAction="#handleButtonAction"`** : Spécifie que la méthode `handleButtonAction` du contrôleur sera appelée lorsque ce bouton est cliqué.
- **`GridPane.rowIndex="0"` et `GridPane.columnIndex="0"`** : Positionne le bouton dans un `GridPane`.

## Appel dans le contrôleur Java

Après avoir défini le code FXML, il faut définir la méthode qui sera appelée quand le bouton sera appuyé. Une fois le bouton appelé Le nom de la méthode doit correspondre au nom spécifié dans l'attribut `onAction` du fichier FXML, et doit être annoté avec `@FXML`.

java

Copy code

`@FXML private void handleButtonAction(ActionEvent event) {     // Code à exécuter lorsque le bouton est cliqué     System.out.println("Bouton cliqué!"); }`