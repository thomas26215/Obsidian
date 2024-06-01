---
MOOC: "[[Cours]]"
Ressource: "R2.02 : IHM"
Cours: "Cours 2 : Développement avec JavaFX"
Date: 2024-05-13
tags: 
Complete: false
Learned: false
---
# La création des éléments
**Démarrer une application :**
```Java
public class App extends Application{ //=> Gère cycle vie de l'application
	public static void main(String[] args){
		launch(); //Lancer l'application
	}
}
```

**Créer des composants :**
```Java
Vbox vbox = new Vbox();
GridPane gridPane = new GridPane();
gridPane.setPadding(new Insets(0, 20, 20, 20));
gridPane.setalignment(Pos.CENTER);
```

**Evènements en JavFX** : Correspond à la structure de données qui contient la source de l'évènement, la cible et le type de l'évènement
- La source de l'évènement
- La cible est le noeud sur lequel il se produit
- Type d'évènement ⇒ Classification


```Java
/**
 * Code Java Pur
 */
TextField tfNom = new TextField();
TextField tfPrenom = new TextField();
...
Button btnReset = new Button("Reset");
...
btnReset.setOnAction(n ew EventHandler<ActionEvent>(){
	@Override
	public void handle(ActionEvent event){
		tfNom.setText("")
		tfPrenom.setText("");
		labelLoginCalcule.setText("");
		pfMdp.setText("");
	}
})
```

```Java
/**
 * Java + FXML
 */

//Code FXML dans un autre fichier

//Code suivant dans la classe Controller 

@FXML
private TextField tfNom;
@FXML
private TextField tfPrenom;
...
@FXML
private void resetButtonAction(ActionEvent event){
	tfNom.setText("");
	tfPrenom.setText("");
	labelLoginCalcule.setText("");
	pfMdp.setText("");
}
```

```FXML
...
<HBOX alignment="CENTER" fillHeight="false" prefHeight="50.0"...>
	<children>
		<Button mnemonicParing="false" onAction="#resetButtonAction" text"Reset"/>
	</children>
</HBox>
```
# Programmation d'une IHM
⇒ **Modifier, agir sur le système** : Clavier, souris, Ecran tactile ..
⇒ **Percevoir / Comprendre Etat du système** : Ecran, Imprimante, Haut-parleur ...
⇒ **Système interactif** : Interface ↔ Noyeau fonctionnel

Exemple de noyeau fonctionnel :
```Java
float kelvin celcius;
float fahrenheit;

kelvin = sensor.getValue()

celsius = kelvin - 273.15
fahrenheit = 32 + 1.8*celcius
```


# Programmation d'une IHM
Séparation du code :
- Noyeau fonctionnel
	- Logique de l'application
	- Modèle
- Interface utilisateur
	- Affichage des éléments graphique
	- Traitement entrées utilisateurs
	- Réaction aux évènements

# Modularité
Chaque module doit pouvoir être réalisé et compris par un programmeur d'une façon relativement indépendante des autres (Méthode Feyman)
- **Continuité modulaire** : Impact d'une modification dans un modul doit être réduit à un minimum de modules
- **Protection modulaire** : Effet  d'une erreur se produisant dans unmodule doit être réduit à un minimum de modules
- **Réutilisation :** Un module doit être conçu de façon à favoriser sa réutilisation dans d'autres applications
- **Minimiser nombre d'interconnexions** pour minimiser effets de propagation à d'autres classes
- **Couplage faible** ⇒ Eviter variables globales et limiter paramètres dans fonction publique
- **Masque info** Seules fonctions publiques
- **Cohérence interne forte** : Assure une fonction unique relevant du problème
- **Taille cohérente** (< 1000 lignes)