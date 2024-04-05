---
MOOC: "[[Cours]]"
Ressource: "R1.02 : Développement d'interfaces Web"
Cours: "Cours 3 :"
Date: 
tags: 
Complete: false
Learned: false
---
**Document object model** = représentation d'une page web en structure web qui est un modèle interne utilisé par navs pour rendre une page. Cela permet la représentation mentale facilitant l'écriture de sélecteurs CSS et cela offre une API pour manipuler le DOP programmatiquement
**DOM** = arbre
**Noeud** = Elément HTML
**Arc** = relation entre un élément parent et une éléments enfant. Un enfant n'a qu'un seul parent
**Relation entre frères et soeurs** = Chaque enfant peut avoir un frère / soeur, un à sa gauche et un à sa droite

**Exemple :**
```HTML
<ul>
	<li>
		<a href="">Accueil</a>
	</li>
	<li>
		<a></a>
	</li>
	<li>
		<a></a>
	</li>
</ul>
```

```HTML
<p>
	Ceci est un <strong> paragraphe </strong> avec de la <u><i>mise en forme</i></u>
</p>
```

**Le lien entre le DOM et le CSS**
```CSS
ul li{} /*Tous les enfants li de ul*/
ul > li{} /*Enfant directs seulement*/
li ~ li{} /*Elements adjacents et non adjacents*/
li + li{} /*Elements adjacents seulement*/
```

[[La mise en page d'un site Web - Flexbox]]