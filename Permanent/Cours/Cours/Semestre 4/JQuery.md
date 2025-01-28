---
id: JQuery
aliases: []
tags: []
---

# Cours complet sur jQuery


## Introduction à jQuery

jQuery est une bibliothèque JavaScript très populaire et puissante, créée en 2006 par John Resig. Son slogan, "Écrivez moins, faites plus", résume parfaitement sa philosophie. jQuery simplifie considérablement l'écriture de scripts JavaScript, permettant aux développeurs de créer des fonctionnalités complexes avec moins de code.

[[Augmenter les niveaux d'endorphines]]

L'un des principaux avantages de jQuery est sa capacité à résoudre les problèmes de compatibilité entre les différents navigateurs. Avant jQuery, les développeurs devaient souvent écrire des scripts différents pour chaque navigateur, ce qui était fastidieux et source d'erreurs. Avec jQuery, un seul script fonctionne de manière cohérente sur tous les navigateurs modernes.

## Utilisation de base de jQuery

Pour commencer à utiliser jQuery, il faut d'abord l'inclure dans votre page HTML. Vous pouvez le faire en ajoutant la ligne suivante dans la section `<head>` de votre document :

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```

Une fois jQuery chargé, vous pouvez commencer à l'utiliser dans vos scripts.

## La fonction ready

La fonction `ready` (appelée fonction anonyme) est l'un des concepts fondamentaux de jQuery. Elle permet d'exécuter du code JavaScript une fois que le document HTML est entièrement chargé et prêt à être manipulé. Voici comment l'utiliser :

```javascript
$(document).ready(function() {
    // Votre code ici
});
```

Ou, en version plus courte :

```javascript
$(function() {
    // Votre code ici
});
```

***Exemple d'utilisatation*** :
```javascript
$(function() {
    var elem = $('</div');
    elem.html('An example element');
    elem.css('border', 'solid blue');
    $('body').append(elem);
})
```

Cette fonction garantit que votre code ne s'exécutera pas avant que tous les éléments du DOM ne soient chargés, évitant ainsi des erreurs potentielles.

## Quelques fonctions utiles en jQuery

- `$` : La fonction principale de jQuery, utilisée pour sélectionner des éléments du DOM. Créer des éléments, rechercher des éléments
- `append` : Ajoute du contenu à la fin des éléments sélectionnés
- `prepend` : Ajoute du contenu au début des éléments sélectionnés
- `html` : Modifie le contenu HTML des éléments sélectionnés
- `css` : Modifie les propriétés CSS des éléments sélectionnés

On peut utiliser ces fonction de cette manière :
```javascript
$(function() {
    for(var i = 0; i < 100; i++) {
        var msg = $('<div>Hello World</div>');
        msg.css('font-size', i);
        $('body').append(msg);
    }
});

## Sélection d'éléments

jQuery excelle dans la sélection d'éléments du DOM. Vous pouvez sélectionner des éléments en utilisant des sélecteurs CSS :

```javascript
$('p'); // Sélectionne tous les paragraphes
$('#monId'); // Sélectionne l'élément avec l'ID "monId"
$('.maClasse'); // Sélectionne tous les éléments avec la classe "maClasse"
```

## Manipulation du DOM

Une fois les éléments sélectionnés, vous pouvez les manipuler facilement :

```javascript
// Changer le texte d'un élément
$('#monId').text('Nouveau texte');

// Ajouter une classe
$('.maClasse').addClass('nouvelleClasse');

// Modifier le CSS
$('p').css('color', 'red');
```

## Gestion des événements

jQuery simplifie également la gestion des événements :

```javascript
$('#monBouton').click(function() {
    alert('Bouton cliqué !');
});

$('input').on('keyup', function() {
    console.log('Touche relâchée');
});
```

## AJAX avec jQuery

jQuery facilite grandement les requêtes AJAX :

```javascript
$.ajax({
    url: 'https://api.example.com/data',
    method: 'GET',
    success: function(response) {
        console.log('Données reçues :', response);
    },
    error: function(xhr, status, error) {
        console.error('Erreur :', error);
    }
});
```

## Animations

jQuery offre des fonctions simples pour créer des animations :

```javascript
$('#monElement').fadeIn(1000); // Apparition progressive
$('#monElement').slideUp(500); // Glissement vers le haut
```

## Conclusion

jQuery reste un outil puissant et polyvalent pour le développement web front-end. Bien que les frameworks modernes comme React ou Vue.js aient gagné en popularité, jQuery continue d'être largement utilisé pour sa simplicité et sa large compatibilité. Maîtriser jQuery peut considérablement améliorer votre productivité en tant que développeur web et vous permettre de créer des interfaces interactives riches avec moins d'effort.
