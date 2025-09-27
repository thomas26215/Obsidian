---
MOOC: "[[Cours]]"
Ressource: "R5.05 : Angular"
Cours: "Cours 1 : Introduction à Anngular"
Date:
tags:
Complete: false
Learned: false
---
[[Concepts de base & installation]]
[[Composants & templates]]
[[Data Binding (liaison de données)]]
[[Directives et pipes]]

---

## 5. Services & injection de dépendances

### Objectifs

- Comprendre le rôle des services (logique métier, accès aux données)
    
- Apprendre l’injection de dépendances (`@Injectable`)
    
- Séparer la logique du composant
    

### Théorie

- Les **services** sont des classes qui fournissent des fonctionnalités (ex : récupérer des données, partager des états)
    
- On décore un service par `@Injectable({ providedIn: 'root' })` pour le rendre injectable partout
    
- Dans un composant, on l’injecte via le constructeur : `constructor(private heroService: HeroService) { }`
    
- Cela encourage la séparation des préoccupations (composant = vue/interaction, service = logique/données)
    

### Exemple concret : gestion de héros

**hero.service.ts**

```ts
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';

export interface Hero {
  id: number;
  name: string;
}

const HEROES: Hero[] = [
  { id: 1, name: 'Alpha' },
  { id: 2, name: 'Beta' },
  { id: 3, name: 'Gamma' }
];

@Injectable({
  providedIn: 'root'
})
export class HeroService {
  getHeroes(): Observable<Hero[]> {
    return of(HEROES);
  }
  getHero(id: number): Observable<Hero | undefined> {
    return of(HEROES.find(h => h.id === id));
  }
}
```

Dans un composant :

```ts
constructor(private heroService: HeroService) { }

ngOnInit() {
  this.heroService.getHeroes().subscribe(hs => this.heroes = hs);
}
```

---

## 6. Routage (Router)

### Objectifs

- Comprendre le rôle du routeur
    
- Définir des routes
    
- Naviguer entre vues
    
- Récupérer les paramètres de route
    

### Théorie

- Le routeur Angular permet de changer de “vue” dans une SPA selon l’URL
    
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

---

## Où aller ensuite ?

Si tu veux, je peux te générer **un pack complet “cours + exemples + exercices” en fichiers Markdown** (à mettre dans Obsidian) pour toutes les sections ci-dessus (et plus). Tu pourras ensuite l’étudier dans Obsidian, lier les notes et avancer. Veux‑tu que je prépare ça pour toi maintenant ?