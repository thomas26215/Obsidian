---
MOOC: "[[Programmation]]"
Langage: Angular
Type:
Outil: []
tags:
---
- Angular est un framework front-end (“full framework”) : il fournit le squelette pour construire des applications web complexes (routing, composants, services, etc.).
- Il suit le modèle MVC / MVVM selon les usages (séparation vue / logique).
- On code souvent en **TypeScript** (ajoute typage, classes, interfaces).
- Depuis Angular v14+, on a la possibilité de construire des **composants standalone** (sans modules NgModule) pour alléger la configuration.
- Le CLI Angular permet de générer une base de projet, des composants, des services, gérer les builds, etc.

### Exemple concret d’installation

```bash
# Installe Angular CLI globalement (si pas déjà)
npm install -g @angular/cli

# Crée un projet standalone
ng new my‑cours-angular --standalone

# Va dans le dossier
cd my‑cours-angular

# Lance le serveur local
ng serve
```

Quand tu ouvres `http://localhost:4200`, tu devrais voir la page d’accueil Angular.

Tu verras les fichiers principaux dans `src/` : `main.ts`, `app/`, `index.html`, `styles.css`, etc.

Dans **main.ts**, tu verras une instruction comme :

```ts
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';

bootstrapApplication(AppComponent);
```

C’est cette ligne qui “démarre” Angular avec le composant racine `AppComponent`.