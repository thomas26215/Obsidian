---
MOOC: "[[Programmation]]"
Langage: Angular
Type:
Outil: []
tags:
---
- Le routeur Angular 
- permet de changer de “vue” dans une SPA selon l’URL
- On définit un tableau de `Routes` avec des chemins (`path`) et les composants associés
- Dans le composant racine, on inclut `<router-outlet></router-outlet>` pour indiquer où les vues doivent s’afficher
- On utilise `routerLink` dans les templates pour naviguer
- On peut récupérer les paramètres de route via `ActivatedRoute`

### Exemple concret : routing basique

**app.routes.ts**

```ts
import { Routes } from '@angular/router';
import { DashboardComponent } from './dashboard/dashboard.component';
import { HeroesComponent } from './heroes/heroes.component';
import { HeroDetailComponent } from './hero-detail/hero-detail.component';

export const routes: Routes = [
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'dashboard', component: DashboardComponent },
  { path: 'heroes', component: HeroesComponent },
  { path: 'hero/:id', component: HeroDetailComponent },
];
```

**app.component.ts**

```ts
import { Component } from '@angular/core';
import { RouterOutlet, RouterLink } from '@angular/router';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterOutlet, RouterLink],
  template: `
    <h1>Mon App</h1>
    <nav>
      <a routerLink="/dashboard">Dashboard</a>
      <a routerLink="/heroes">Heroes</a>
    </nav>
    <router-outlet></router-outlet>
  `
})
export class AppComponent {}
```

Dans le composant `HeroDetail`, pour obtenir l’`id` :

```ts
this.route.paramMap.subscribe(params => {
  const id = Number(params.get('id'));
  // appeler le service pour récupérer le héros
});
```