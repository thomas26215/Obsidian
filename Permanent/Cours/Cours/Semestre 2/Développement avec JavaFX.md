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

# Architecture en couches
L'architecture en couches vise à structurer le logiciel en niveaux d'abstraction, où chaque niveau réalise une fonction spécifique en s'appuyant sur les niveaux inférieurs.

## Exemple de couches dans une application interactive :

- **Interface Homme-Machine (IHM)** : Interagit avec l'utilisateur.
- **Application** : Traite les fonctions logicielles.
- **Utilitaire** : Gère les objets métier.
- **Noyau** : Fournit des services techniques élémentaires et l'accès aux données.

#### Avantages :

1. **Séparation des préoccupations** : Les services de bas niveau ne sont pas mélangés avec la logique de l'application.
2. **Réduction de la complexité** : Les détails sont cachés dans les niveaux inférieurs.
3. **Maintenance facilitée** : Les modifications dans une couche n'affectent pas les autres.
4. **Réutilisation** : Les couches basses peuvent être utilisées dans plusieurs applications.

#### Inconvénients :

1. **Performance** : Traverser toutes les couches pour accéder aux fonctions de bas niveau peut être lent.
2. **Modularité difficile** : La modularité peut être compromise.
3. **Dépendances** : Les dépendances entre le noyau fonctionnel et l'interface peuvent rendre les modifications complexes.

## Modèles d'Architecture de systèmes interactifs :

### Seeheim (1983)
- **Présentation** : Interprète les actions de l'utilisateur et génère les sorties.
- **Contrôleur de dialogue** : Gère le séquencement de l'interaction.
- **Interface du noyau fonctionnel** : Adapte les entrées et sorties entre l'utilisateur et le noyau fonctionnel.
### ARCH (1992)
- **Adaptateur du domaine** : Gère les tâches spécifiques au domaine nécessaires pour l'utilisateur.
- **Composant d'interaction** : Inclut les widgets et la communication avec les périphériques.
- **Contrôleur de dialogue** : Maintient la consistance des vues et séquence les tâches.
- **Composant de présentation** : Sert de médiateur entre l'interaction et le contrôleur de dialogue.
- **Noyau fonctionnel** : Partie non interactive de l'application.

# Modèle de référence MVC
- Le modèle est le noyeau fonctionnel de l'agent. Il peut représenter. Il peut représetner des données brutes ou des objets ayant un comportement complexe. Notifie les vues qui lui sont associées à chaque fois que son état se trouve modifié par noyeau de l'application ou pas ses contrôleurs
- Vue maintient une représentation du modèle perceptible par l'utilisateur, qu'elle met à jour à chaque changement d'état du modèle. Généralement constituée d'objets graphiques
- Contrôleur reçoit et interprète évènements utilisateurs, en les répercutant sur le modèle ou la vue

![[Pasted image 20240601145431.png]]