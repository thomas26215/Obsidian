---
MOOC: "[[Programmation]]"
Langage: Angular
Type:
Outil: []
tags:
---

- Découvrir les directives structurelles (`*ngIf`, `*ngFor`), les directives d’attribut (`ngClass`, `ngStyle`)
- Comprendre les pipes (formatage de données comme date, uppercase, custom pipe)

### Théorie & exemples

#### Directives structurelles

```html
<ul>
  <li *ngFor="let hero of heroes; let i = index">
    {{ i + 1 }}. {{ hero.name }}
  </li>
</ul>

<div *ngIf="selectedHero">
  <h4>Détail :</h4>
  <p>{{ selectedHero.name }}</p>
</div>
```

- `*ngFor` : boucle sur une collection
- `*ngIf` : afficher / masquer des éléments
    

#### Directives d’attribut

```html
<div [ngClass]="{ 'selected': hero === selectedHero }">
  {{ hero.name }}
</div>

<div [ngStyle]="{ color: hero.color, 'font-weight': hero === selectedHero ? 'bold' : 'normal' }">
  ...
</div>
```

#### Pipes

Angular possède des pipes intégrés :

- `{{ now | date:'dd/MM/yyyy' }}`
- `{{ name | uppercase }}`
- `{{ amount | currency:'EUR' }}`

On peut aussi créer des pipes personnalisés pour transformer ces données