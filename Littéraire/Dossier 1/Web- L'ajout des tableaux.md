# La création d'une table en HTML
La création de table en HTML se fait avec les balises `<table></table>`.
A l'intérieur, on peut y mettre :
- `<tr></tr>` : Cela permet de spécifier le début et la fin d'un tableau
- `<td></td>` : Cela permet de spécifier le début et la fin d'une cellule.
⇒ **Ainsi, un table de 3x2 peut d'écrire comme ceci :**
```html
<table>
	<tr>
		<td>Carmen</td>
		<td>33 ans</td>
		<td>Espagne</td>
	</tr>
	<tr>
		<td>Michelle</td>
		<td>26 ans</td>
		<td>Etat Unis</td>
	</tr>
</table>
```
**Resultat :**
![[Capture d’écran 2023-08-24 003456.png]]
> A noter qu'un tableau est de type `block` ; Il doit donc être en dehors d'un paragraphe ou d'une balise `<div>`






# Ajouter des bordures dans un tableau HTML
Après avoir crée un tableau, on se rend compte que celui-ci ne contient pas de lignes pour séparer les différents éléments. Il est donc nécessaire d'y ajouter les bordures.
Il faut pour ceci utiliser la propriété CSS `border` suivit de 3 paramètres dans l'ordre suivant :
→ **taille - type - couleur**
**Exemple :**
```css
td{
	border: 1px solid black;
}
```

Il y a un problème, c'est qu'il y a une double bordure. Pour régler cela, il faut utiliser la propriété CSS `border-collapse` associé d'un des deux paramètres suivants :
- `collapse` : Cela crée des bordures collées
- `separate` : Cela crée des bordures disscociées

# Mettre un titre dans un tableau HTML
Il est tout à fait possible de mettre un titre dans notre tableau HTML. Pour cela, il suffit de mettre dans le tableau un `<caption></caption>` de la même manière qu'on va mettre [un élément] `<tr></tr>` ou `<td></td>`

# Aérer nos éléments dans un tableau HTML
Nous avons réussi à mettre [des bordures] dans notre tableau HTML. Cependant, nous voyons que celles-ci sont vachement collées à nos éléments. Pour y ajouter de l'espace, on peut simplement utiliser un pading

# Fusionner des cellules dans un tableau HTML
Dans notre tableau HTML, il est tout à fait possible de fusionner des cellules. Pour cela, on peut utiliser  :
- `colspan` qui nous permet de fusionner des colonnes
- `rowspan` qui nous permet de fusionnser des lignes
Le code suivant :
```html
<table>
   <tr>
       <th>Titre du film</th>
       <th>Pour enfants ?</th>
       <th>Pour adolescents ?</th>
   </tr>
   <tr>
       <td>Massacre à la tronçonneuse</td>
       <td >Non, trop violent</td>
       <td rowspan="2">Oui</td>
   </tr>
  <tr>
       <td>The Ring</td>
       <td>Effrayant</td>
   </tr>
   <tr>
       <td>Les bisounours font du ski</td>
       <td>Oui, adapté</td>
       <td>Pas assez violent...</td>
   </tr>
   <tr>
       <td>Lucky Luke, seul contre tous</td>
       <td colspan="2">Pour toute la famille !</td>
   </tr>
</table>
```
permet de donner le résultat suivant :
![[Capture d’écran 2023-08-24 010308.png]]


