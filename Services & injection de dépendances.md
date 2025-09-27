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
