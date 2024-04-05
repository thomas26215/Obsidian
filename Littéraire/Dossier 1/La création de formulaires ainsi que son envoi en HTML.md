# Créer un formulaire en HTML
La création de formulaire se fait grâce à la balise `<form></form>`. Dans cette balise, il faut indiquer par quel moyen le formulaire va être envoyé par l'attribut `method` qui va prendre en paramètre `get` ou `post` ainsi que `action` qui va indiquer l'adresse de la page ou du programme qui va traiter les informations (elle est utile pour le backend). Ici, on le laisse vide, car cela permet d'indiquer que l'on reste sur la même adresse (plus de facilité d'inspection)
**Exemple** :
```html
<p>Texte avant le formulaire</p>
	<form method="get" action="">
		<p>Texte à l'intérieur du formulaire</p>
	</form>
<p>Texte après le formulaire</p>
```

Nous y a jouterons par la suite une balise `<input>` qui nous permettra d'y ajouter un champs.

# Les champs en HTML
Il faut savoir qu'un champs en HTML se constitue de plusieurs parties :
- La balise en elle-même : `<input>`. Cette elle qui va nous informer du champs correspondant. On va pouvoir aussi y retrouver toute sorte de d'attributs
  ⇒ De nombreux
	- L'attribut `type` qui permet de définir le type de champs (Indispensable)
	- L'attribut `name` qui ne sera pas visible sur la page mais qui nous permettra d'identifier le champs d'où viennent les informations (Indispensable)
	- L'attribut `id` qui doit être unique pour chaque élément qui doit être placée dans la balise `<input>`. Contrairement à l'attribut `name` qui peut se retrouver à  plusieurs endroits (Ex : `checkbox`, plusieurs éléments pour celui-ci), L'attribut `id` doit être unique pour chaque élément (Quel case du `checkbox` on a coché ?)
	- `size` : agrandir le champs
	- `maxlenght` : Maximum de charactère
	- `value` : Pré-remplir
	- `placeholder` : Indication sur contenu du champs. Disparaît dès qu'infos rentrées
- La balise `<label>` qui servira à donner une indication sur ce que l'utilisateur soit rentrer. Elle peut se situer en haut si c'est une zone de monoligne ou de multiligne ou bien sur le côté si c'est une `checkbox`
	- L'attribut `for` qui se situera dans la balise `<label>`. Il sert à faire référence au champs afin de placer correctement le texte d'indication. Il doit prendre en paramètre la même chose que prend en compte l'attribut `name` dans la balise `<input>`
> **! Si nous mettons le label avant le input, alors le texte d'indication sera devant le formulaire de rentrée et inversement. Si l'on souhaite que le texte d'indication se situe au-dessus, il est nécessaire de mettre d'abord le `<label>`, ensuite la balise orpheline `<br>` puis enfin de balise `<input>`**

Ainsi, voici à quoi peut ressemble un formulaire :
```html
<form method="get" action="">
	<p>
		<input type="text" name="prenom" id="prenom"><label for="prenom">Quel est votre prenom ?</label>
	</p
</form>
```
⇒ Il peut être lu comme ceci : Nous avons ici un formulaire qui demande une réponse en une seule ligne. Son id ainsi que son nom qui serviront à pouvoir être utilisés plus tard pour des modifications ou la récupération d'éléments sont tous deux *prénom*. Nous avons comme indication qu'il faut rentrer son prénom.

Il y a plusieurs champs de base qui suivent le même principe que vut plus haut :
- `type=text` Permet une zone de texte sur une seule ligne. Pour que la zone de texte puisse se faire sur plusieures lignes, il suffit de rajouter l'attribut `input` par `textarea` : `<textarea type="text"...> `
- `<input type="email">` : Emails
- `<input type="url">` : URL commencant par `http` ou `https`
- `<input type="tel">` : Numéro de telephone
- `<input type="number">` : Que des chiffres
- `<input type="range">` : Avec un curseur
- `<input type="date">` : Une date
	- `<input type="time">` : Pour l'heure
	- `<input type="week">` : Pour la semaine
	- `<input type="month">` : Pour le mois
	- `<input type="datetime">` : Pour la date et l'heure
	- `<input type="datetime-local">` : Pour la date et l'heure sans décalage horaire
- `<input type="search">` : Une recherche

Il existe cependant des champs qui sont un peu plus compliqués que ca :
## Les questions à choix
Il peut nous arriver que l'on veuille demander à l'utilisateur de choisir un ou plusieurs choix parmis plusieurs choix définis. Pour cela, on a plusieurs possibilités :

### A - Liste à puce à choix unique
Afin de réaliser cela, il faut utiliser `type=radio`. Ici, contrairement à ce que nous avons vu avant, les attributs `name` et `id` présents dans la balise `input`  ne seront pas identiques : 
- L'attribut `name` sera le sera le même pour tous les éléments de la liste à puce (Exemple : tous les éléments auront comme `name` âge si la liste à puce est à propos de l'âge de la personne). Cela permettra à tous les boutons radios d'avoir le même nom
- L'attribut `id` sera au contraire unique pour chaque élément pour pour récupérer lequel à été cliqué (exemple 5 à 15 ans pour le premier, 15 à 25 ans pour le deuxième et + de 25 ans pour le troisième)
Voici à quoi ca peut ressembler :
```html
<form method="get" action="">
	<p>
		Quel âge avez-vous ?<br>
		<input type="radio" name="age" value="moins15" id="moins15"><label for="moins15">Moins de 15 ans</label><br>
		<input type="radio" name="age" value="medium15-25" id="medium15-25"><label for="medium15-25">Entre 15 et 25 ans</label><br>
		<input type="radio" name="age" value="medium25-40" id="medium25-40"><label for="medium25-40">Entre 25 et 40 ans</label><br>
		<input type="radio" name="age" value="plus40" id="plus40"><label for="plus40">Plus de 40 ans</label><br>
	</p>
</form>
```
On remarque que chaque élément possède son propre `<label>`

### B - Question à choix multiple
Ensuite, pour les questions à choix multiples, cela fonctionne sur le même principes à quelques choses prêt :
- On remplace `type=radio` par `type=checkbox`
- Le `name` et l'`id` de chaque est élément est le même
- Le `name` est différent pour chaque élément
Voici à quoi ca pourrait ressembler :
```html
<form method="get" action="">
	<p>
		Cocher les aliments que vous aimez manger :<br>
		<input type="checkbox" name="frites" id="frites"> <label for="frites">Frites</label><br>
		<input type="checkbox" name="steak" id="steak"> <label for="steak">Steak</label><br>
		<input type="checkbox" name="epinards" id="epinards"> <label for="epinards">Epinards</label><br>
	</p>
</form>
```

### C - Liste déroulante
Enfin, pour les listes déroulantes, c'est légèrement différent. En effet, nous aurons un unique `<label></label>` qui servira de question. Ensuite la liste déroulante en elle même sera identifiée par la balise `select` ayant un `name` et un `id` identique et à l'intérieur des balises `<select></select>`, il y aura des balises `<option></option>` pour chaque élément présents dans la liste déroulante. Dans cette balise se trouvera l'attribut `value` (afin de pouvoir identifier quel élément de la liste a été choisi) et entre ces deux balises se trouvera le texte de l'élément. Voici un exemple :
```html
<form method="get" action="">
	<p>
		<label for="pays"> Dans quel pays habitez-vous ?</label><br>
		<select name="pays" id="pays">
			<option value="espagne">Espagne</option>
			<option value="france">France</option>
			<option value="chine" selected>Chine</option>
			<option value="Japon">Japon</option>
		</select>
	</p>
</form>
```




# Regrouper plusieurs champs dans un encadré
Il se peut que nous ayons beaucoup de formulaires et qu'il devient donc difficile pour l'utilisateur de se repérer sur la page web. C'est pourquoi il est possible de regrouper plusieurs forms dans un encadré contenant une indication sur l'utilité des formulaire.
Pour faire cela, il faut utiliser la balise `<fieldset></fieldset>` qui est un grand champs regroupant plusieurs petits champs. Il est nécessaire d'y ajouter dedans la balise `<legend></legend>` qui est une indication sur les champs présents à l'intérieur. Voici un exemple :
```html
<form method="get" action="">
	<fieldset>
		<legend>Vos coordonnées</legend>
		<label for="nom">Nom</label><input type="text" name="nom" id="nom">
		<label for="prenom">Prenom</label><input type="text" name="prenom" id="prenom">
		<label for="email">email</label><input type="email" name="email" id="email">
	</fieldset>
</form>
```

**Résultat :**
![[Capture d’écran 2023-08-26 165914.png]]

# Finaliser un formulaire et ajouter un bouton d'envoi



- Attribut `autofocus` dans balise `<input>` permet de placer curseur automatiquement sur form dès que page chargée
- Attribut `required` dans balise `<input>` = champs obligatoire

⇒ Pseudo-classe en CSS :
- `:required` qui agit sur élément nécessitant d'être remplis
- `:invalid` qui agit sur élément qui ne comporte  pas les bonnes choses (ex : majuscule manquante)
**Exemple** :
```css
:required{
	background-color: #F2A3BB;
}
```
Ainsi, si un champs doit être remplit et qu'il ne l'est pas, la couleur de fond de l'élément va changer

Bouton d'envoi avec `<input>` :
- `type="submit"` : Utilisé le + souvent. Le visiteur sera conduit à la page indiquée dans l'attribut `action` du formulaire
- `type="reset"` : Remet le formulaire à 0
- `type="image"` : Ajouter attribut `src` pour ajouter image personnalisée à la place du bouton
- `type="button"` : Bouton générique

> **HTML et CSS ne sont pas suffisants pour traiter ces infos, nécessaire d'utiliser PHP pour récupérer les infos saisies et en faire quelque chose**
