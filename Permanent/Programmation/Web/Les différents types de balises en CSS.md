---
MOOC: "[[Programmation]]"
Langage: Web
Type: CSS
tags:
---
Il existe plusieurs types de balises :
1. **Par type d'élément** : `p{...}`
2. **Par classe** : `.rounded{...}` (⇒  Tous les éléments du mm type)
3. **Par type et classe** : `img.rounded{...}`
4. **Par identifiant (`id=""`)** : `#r102-intro{...}`
On peut aussi sélectionner plusieurs sélecteurs :
1. **Par factorisation** : `a, .abstract{...}`
2. **Par imbrication** : `section p{...}` (⇒ Tous les paragraphes `<p>` dans les balises `<section>`)
3. **Par imbrication indirecte** : `p section{...}`(Tous les `<p>` qui ont pour parent direct ou indirect `<section>`)
4. **Par imbrication** : `p > section{...}`
---
**Links :**
[[La base du CSS - Les règles]]