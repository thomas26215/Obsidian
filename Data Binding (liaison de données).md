| Type de liaison                  | Syntaxe                     | Usage                                                           | Exemple concret                                  |
| -------------------------------- | --------------------------- | --------------------------------------------------------------- | ------------------------------------------------ |
| Interpolation (binding de texte) | `{{ expression }}`          | Afficher une donnée du composant dans le template               | `<h2>{{ hero.name }}</h2>`                       |
| Property binding                 | `[property]="expression"`   | Lier une propriété d’un élément DOM (ou directive) à une donnée | `<img [src]="hero.imageUrl" />`                  |
| Event binding                    | `(event)="handler($event)"` | Réagir à un événement utilisateur                               | `<button (click)="onClick()">Click moi</button>` |
| Two-way binding                  | `[(ngModel)]="property"`    | Synchronisation bidirectionnelle entre vue et modèle            | `<input [(ngModel)]="hero.name" />`              |

Exemple concret dans un composant :

```ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-binding-example',
  standalone: true,
  imports: [CommonModule, FormsModule],
  template: `
    <h3>Exemple Data Binding</h3>
    <p>Nom : {{ name }}</p>
    <input [(ngModel)]="name" placeholder="Tape ton nom" />
    <button (click)="reset()">Reset</button>
  `
})
export class BindingExampleComponent {
  name: string = 'Jean';

  reset() {
    this.name = '';
  }
}
```

- On affiche la propriété `name` via interpolation
- On lie l’`input` avec `ngModel`
- On écoute l’événement `click` sur le bouton pour appeler la méthode `reset()`
    