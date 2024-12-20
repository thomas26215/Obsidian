# Pourquoi utiliser **React**

- Meilleure expérience utilisateur
	- Rendement du composant et non de la page
- Meilleure expérience développeur
	- Réutilisabilitédu composant
⇒ Gain de temps

Philosophie en composant
[[Pasted image 20241201181156.png]]

## Créer son premier composant
3 fichiers de bases :
- `index.html` ⇒ Il y a une seule div avec l'id `root`
- `index.js`
	- la balise d'id `root` dans le fichier html est récupérer dans ce fichier js avec `getElementById("root");` que l'on range dans une vraiable `rootElement`
	⇒ `const rootElement = document.getElementById("root");`
	- On dit ensuite au fichier de `render` le fichier `App`, cela va donc rendre rendre tout ce qu'il y a dans le fichier `App`
```js
root.render(
	<SctictMode>
		<App />
	</SctictMode>
);
```
- `App.js` ⇒ Le fichier `index.js` va rendre tout ce qu'il y a dans ce fichier. Ainsi, nous n'avons plus besoin des fichiers `index.html` et `index.js` car les modifications seront effectuées dans le fichier `App.js`. Voici le code de base du fichier :
```js
import "./style.css";

export default function App(){
	return (
		<div className="App">
			<h1> Hello Vi </h1>
			<h2> Voici un sous titre </2>
		</div>
	):
}
```

# Comment est crée le composant `App`

Il faut déjà savoir que les composants crées en react sont dits fonctionnels. Qui dit fonction dit `function`. Comme toute fonction, un composant doit avoir un **nom**, des **paramètres** et **un ensemble d'instructions**
> [!info] Nom
>Le nom de la fonction doit être en majuscules

```js
function App(){
	//Ensemble d'instructions
}
```

## C'est quoi un composant react ?

Chaque composant est composée de 3 parties internes
- 1 partie `state` ⇒ 1 Etat / données
- 1 partie `comportements`
- 1 partie `affichage` (`render`). On va y mettre que du `JSX`

> [!Définition] **Définition** JSX
> Le JSX est un langage crée par **Facebook** qui nous permet d'injecter du code `HTML` dans un fichier `JS`


Les trois **composants** vont interagir ensemble grâce à des flux Ces flux vont rendre les composants interactifs. Cela fonctionne de cette manière :
1. On va définir un `state` qui va accueillir de la donnée dynamique
2. On va ensuite projeter ce `state` sur notre `affichage` pour le rendre lui aussi dynamique. Il y a plusieurs éléments d'affichage (lien, bouton ..) Et sur chacun des éléments d'affichage, on va brancher des comportements (gâce à des "evènements").
3. Grâce à ces évènements, on va pouvoir définir de manière arbitraire ce qu'ils font. Généralement, ces instructions vont impliquer le fait de modifier le composant `state`
4. Le composant va donc réagir en réactualisant l'affichage ⇒ Il va **rerender**

Maintenant, le cas pratique :
Le code suivant :
```js
function App(){
	// state

	//comportement
	
	// affichage (render)
	return <h1>1</h1>
}
```

Cette fonction affiche le texte `1` sous forme de titre. Je veux incrémenter cette valeur

1. Définir un state. On utilise la fonction `useState`. C'est un **hook** qui nous permet de définir un State. Cette fonction retourne un tableau que l'on range dans un tableau : `const tableau* = useState(...);` 
	- Il faut tout d'abord lui mettre la valeur d'initialisation : `1`
	  
	  >[!info]
	  >⇒ Il faut savoir qu'on peut déconstruire ce tableau pour récupérer en son premier index la première valeur d'initialisation (on l'appelle ici `compteur` ⇒ `const [compteur] = useState()`)
	  
	- Ce hook peut être modifié par une fonction dédiée qui porte le nom de `setter`, que l'on va appeler ici `setCompteur` ⇒ `const [compteur, setCompteur] = useState(1);`
2. Je vais maintenant projeter mon State sur mon affichage pour le rendre lui aussi dynamique. Cependant, dans le `render`, si j'écris `<h1>compteur</h1>`, react comprend que je veux affficher le mot et non la variable. Ainsi, je dois faire une interpolation **JSX**, ce qui me permet d'inclure du code JS dans du JSX. Je vais donc à la place l'écrire entre deux accolades : `return <h1>{compteur}</h1>`. Je vais donc maintenant ajouter un bouton pour pouvoir ajouter 1 quand je clique dessus


**Résumé** :
1. J'ai donc définit un state initialisé à 1 que je récupère dans `compteur` et que je ne pourrai modifier que avcec son `setter` appelé `setCompteur`

>[!definition] **Définition** hook
> Fonctions spéciales de librairie react permettant de définir quelque chose. Ca commence généralement par `use` :
> - `useState` ⇒ Définir un State
> - `useRef`
> - `useContexte`

