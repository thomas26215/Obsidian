# Prérequis
- La classe **`Application`** :
```Java
import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;

  

public class App extends Application{
private Stage stage;

@Override
public void start(Stage primaryStage) {
	stage = primaryStage;
}

public static void main(String[] args) {
	launch(args);
}

}
```

- Créer la classe `FirstController` and `SecondController`
- Associer les fichiers FXML aux contrôllers (Dans le `Pane` ajouter l'argument `fx:controller="FirstController`)
