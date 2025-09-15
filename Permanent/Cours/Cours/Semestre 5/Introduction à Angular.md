---
MOOC: "[[Cours]]"
Ressource: "R5.05 : Angular"
Cours: "Cours 1 : Introduction à Anngular"
Date:
tags:
Complete: false
Learned: false
---
# 📘 Cours : Angular et Data Binding

## 1. Introduction à Angular

- **Angular** est un [[Framework]] **JavaScript côté client**.
    
- Il permet de développer des **[[SPA (Single page application)|applications web monopages (SPA)]]**.
    
- Multiplateforme, open source (licence MIT).
    
- Repose sur une **[[Le modèle - MVC|architecture MVC]]** et s’appuie principalement sur **TypeScript**.
    

### TypeScript

- Sur-ensemble de JavaScript (ES6), rétrocompatible avec ES5.
    
- Ajoute des fonctionnalités avancées :
    
    - classes, classes abstraites
        
    - interfaces
        
    - typage statique
        
    - etc.
        

⚠ Ne pas confondre **Angular** (versions récentes) avec **AngularJS** (ancienne version).

---

## 2. Les outils nécessaires

- **Node.js** et son gestionnaire de paquets NPM → [nodejs.org](https://nodejs.org/)
    
- **IDE recommandé** : WebStorm (ou équivalent VS Code).
    
- **Débogage** : intégré dans le navigateur (DevTools) ou dans l’IDE.
    
- **Firebase** : service web pour l’hébergement et la base de données temps réel.
    

---

## 3. Installation d’Angular

1. Installer **Node.js LTS (22.x)** + gestionnaire NPM.
    
2. Recommandation : utiliser **nvm** (Node Version Manager) pour gérer plusieurs versions.  
    → [nvm-sh](https://github.com/nvm-sh/nvm)
    
3. Installer **Angular CLI (20.x)**  
    → [angular.dev/installation](https://angular.dev/installation)
    

---

## 4. Structure d’une application Angular

Une application Angular contient :

- **Point d’entrée** : script principal de lancement.
    
- **Feuille de style globale**.
    
- **Fichiers de configuration** : Angular, Node, TypeScript.
    
- **Sources** de l’application : composants, services, modèles.
    
- **Composant principal** `app`.
    

---

## 5. Les Composants

- Un **composant** est une unité de base d’Angular.
    
- Création via la CLI :
    
    ```bash
    ng generate component heroes
    ```
    
- Cela génère un dossier avec 4 fichiers :
    
    - `.ts` → logique du composant
        
    - `.html` → template (vue)
        
    - `.css` → style
        
    - `.spec.ts` → tests unitaires
        

### Exemple d’annotation

```ts
@Component({
  selector: 'app-heroes',
  templateUrl: './heroes.component.html',
  styleUrls: ['./heroes.component.css'],
  imports: [ … ]
})
```

- `selector` : balise HTML personnalisée pour utiliser le composant.
    
- `templateUrl` : vue associée.
    
- `styleUrls` : styles associés.
    

---

## 6. Le Data Binding

Le **data binding** permet de synchroniser **modèle ↔ vue**.  
Il existe plusieurs formes :

### 1) Interpolation

Affiche une donnée du modèle dans le DOM.

```html
<h2>{{ hero.name }}</h2>
```

### 2) Property Binding

Lie une propriété DOM à une donnée du modèle.

```html
<li [class.selected]="hero === selectedHero"></li>
```

### 3) Event Binding

Exécute une méthode lors d’un événement.

```html
<li (click)="onSelect(hero)"></li>
```

Événements possibles : `click`, `focus`, `blur`, `keydown`, etc.

### 4) Two-Way Data Binding

Synchronisation bidirectionnelle **modèle ↔ vue**.

```html
<input [(ngModel)]="hero.name" placeholder="name"/>
```

---

## 7. Les Directives Structurelles

Elles permettent de manipuler le DOM.

- **Boucle (@for)**
    
    ```html
    @for (hero of heroes; track hero.id) {
      <li>{{hero.name}}</li>
    }
    ```
    
- **Condition (@if / @else if / @else)**
    
    ```html
    @if (selectedHero) {
      <p>{{selectedHero.name}}</p>
    }
    ```
    
- **Switch (@switch)**
    
    ```html
    @switch (role) {
      @case ('admin') { … }
      @default { … }
    }
    ```
    

---

## 8. Composants imbriqués

- Un composant peut inclure un autre.
    
- Exemple : `hero-detail` affichant les détails d’un héros.
    
- Passage de données avec `@Input` :
    
    ```ts
    @Input() hero: Hero;
    ```
    
- Utilisation dans un autre composant :
    
    ```html
    <app-hero-detail [hero]="selectedHero"></app-hero-detail>
    ```
    
