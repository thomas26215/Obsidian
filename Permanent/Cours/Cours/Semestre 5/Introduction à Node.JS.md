---
MOOC: "[[Cours]]"
Ressource: "R4.08 : Node.JS"
Cours: "Cours 1 : Introduction à Node.JS"
Date:
tags:
Complete: false
Learned: false
---
Node.JS est une environnement d'exécution permettant d'exécuter du Java sur PC.

---

Du côté de **Node.js**, on retrouve des fonctionnalités liées au système d’exploitation, comme l’accès au **système de fichiers**, l’exécution de **programmes externes**, la gestion de **fenêtres applicatives** (par exemple avec Electron) et l’interaction avec le **shell**. Ces capacités permettent à Node.js d’être utilisé comme un environnement serveur ou comme moteur d’applications.

À l’inverse, le **navigateur** offre des outils spécifiques à l’affichage et à l’interactivité des pages web. Il gère notamment le **DOM** (Document Object Model), qui représente la structure HTML d’une page, ainsi que les **feuilles de style (CSS)**, indispensables pour la mise en forme et le rendu visuel.

Les deux environnements partagent cependant un socle commun : le langage **ECMAScript** (la norme de JavaScript), l’utilisation des **promesses** pour gérer l’asynchronisme, et un modèle d’exécution en **mono-thread**.

# Premier programme
1. Créer un fichier `hello-world.js` avec le code suivant :
```js
console.log("Hello world !");
```
2. Exécuter avec `node hello-world.js` 
```shell
>>> node hello-world.js
Hello world !
```

# Programmation modulaire
Pour créer un module, il faut créer un fichier dans lequel des éléments sont exportés à l'aide du mot-clé `export`. Comme en python, un élément non exporté ne sera pas visible en dehors du module.
On peut exporter différents types de d'éléments :
- Variable
- Constante
- Classe
- ...


> [!Example]
> ```js
> export const factorial
> 	if (n === 0) return 1;
> 	else if (n === 1) return 1;
> 	else return n * factorial(n - 1);
> };
> ```
> ---
> ```js
> import { factorial } from './factorial.js';
> console.log(factorial(4)); // ??
> ```


# Installer, créer et publier des packages
**Un package** est un ou plusieurs modules groupés ensemble. Il est communément importé dans un autre package.
Node.JS s'appuie sur NPM pour installer et publier des packages. npmjs.org est le gestionnaire de package privilégié pour Node.JS

# Installer un package
Pour installer un package, il faut utiliser `npm` :
```shell
>>> npm install lorem-ipsum #Instal