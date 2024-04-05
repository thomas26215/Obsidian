---
MOOC: "[[Cours]]"
Ressource: 
Cours: 
Date: 
tags: 
Complete: false
Learned: false
---
[[La création de formulaires ainsi que son envoi en HTML]]

Omniprésentes dans les pages. Formulaire de contact, E-commerce
Balise `<form>`. Deux attributs:
- `action` =définit la page web pour appeler pour traiter les informations du formulaire
- `method` = Définir comment sont traitées les infos (`post` =données ajoutées au body de la requête HTTP ⇒ non visible dans URL et `get` données transférées en tant que variables dans l'URL ⇒ visible dans URL)

Plus éléments :
- Champs de txt simple et multilignes
- Case a cocher
- Boutons radio
- Liste déroulante
- Champs pour déposer fichiers
- Boutons

`input` vs `textarea`.

`<input attributs...>`
`<textarea name="">texte</textarea>`

Le `<label` sert à ce que quand on clique sur le label, la champs est automatiquement sélectionné

>**Ne jamais faire confiance à l'utilisateur**

```CSS
input{
	border: none;
	border-bottome: thick solid gray;
}
input:focus{
	border-bottom-color: blue;
	color: blue
}

/*=> Outline présente (très fine bordure qu indique que élément sélectionné => outline: none*/

input:not(:placeholder-shown){/*Si non vide*/
	border-bottom-color: green;
	color: blue;
}
```

```CSS
input:valid{
	background-color: green;
}
input:invalid{
	background-color: red;
}
```

---
**Questions :**
1. Quels sont les deux attributs principales d'un formulaire ? Quelles est la balise d'un formulaire ?
2. Quelles sont les deux types de balises qu'on ajoute à l'intérieur d'une balise formulaire ? Quels sont les principaux attributs de ces deux balises ?
3. Comment définir une zone de texte ? Quelles sont les principales différences avec `input` ?
4. Quelles est la principale règle ?
5. Donner les principaux  types de formulaires
6. Comment regrouper plusieurs champs dans un encadré ?
7. Comment crée un bouton d'envoi ?
8. Quelles sont les pseudo-classes ?
