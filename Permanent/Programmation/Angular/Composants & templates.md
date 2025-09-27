---
MOOC: "[[Programmation]]"
Langage: Angular
Type:
Outil: []
tags:
---
- Un composant est une unité réutilisable qui encapsule :
    1. une **classe TypeScript** (logique)
    2. un **template HTML** (vue)
    3. un (ou des) fichier(s) CSS (style)
- Dans Angular, le décorateur `@Component` sert à définir un composant.
- Si `standalone: true`, ce composant est utilisable sans être déclaré dans un module.
- Un composant peut importer (dans `imports: [...]`) les modules nécessaires (CommonModule, FormsModule, RouterModule, etc.) pour fonctionner dans son template.

### Exemple concret : un composant “HelloWorld”

**app/hello-world.component.ts**

```ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-hello-world',
  standalone: true,
  imports: [CommonModule],
  template: `
    <p>Hello, bienvenue à Angular !</p>
  `,
  styles: [`
    p { color: darkgreen; font-size: 1.2em; }
  `]
})
export class HelloWorldComponent {
  // ici tu peux mettre des propriétés et des méthodes
}
```

Pour utiliser ce composant dans `AppComponent` :

**app/app.component.ts**

```ts
import { Component } from '@angular/core';
import { HelloWorldComponent } from './hello-world.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HelloWorldComponent],
  template: `
    <h1>Mon application Angular</h1>
    <app-hello-world></app-hello-world>
  `
})
export class AppComponent {}
```

Au final, tu verras dans la page le texte “Hello, bienvenue à Angular !”.