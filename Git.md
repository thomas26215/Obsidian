## Compte rendu – Projet _chess.js_

## UE R5·(Réal·07|Déploi·05) – Automatisation de la chaîne de production

## 1. Organisation du travail

**Binôme 1** : **Fonctionnalité 3.1** – Affichage des mouvements possibles  
**Binôme 2** : **Fonctionnalité 3.4** – Promotion du pion (reine uniquement)

## 2. Fonctionnalités développées

## 3.1 Affichage des mouvements possibles (notre binôme)

**Implémentation technique complète** dans `view.js` :

javascript

```JS
/**
 * Get all possible legal moves for a piece.
 * @param {Piece} piece - the piece to analyze
 * @return {Array.<Object>} array of {rank, file} objects
 */
let getPossibleMovesForPiece = function (piece) {
  const moves = [];
  for (let rank = 1; rank <= 8; rank++) {
    for (let file = 1; file <= 8; file++) {
      if (piece.canMove(rank, file)) {
        moves.push({ rank, file });
      }
    }
  }
  return moves;
};

```

**Logique d'affichage** dans `handleClick` :

- **Sélection pièce** → classe CSS `.selected`
    
- **Calcul mouvements** → `getPossibleMovesForPiece(piece)`
    
- **Affichage visuel** → classes CSS `.possible-move` et `.capture`
    
- **Validation coup** → `current.move(rank, file)`
    

**Classes CSS ajoutées** :

text

`.selected     { background: #4CAF50; } .possible-move { background: rgba(76,175,80,0.3); } .capture      { background: rgba(244,67,54,0.5); }`

## 3.4 Promotion du pion (autre binôme – audit)

Promotion **automatique en reine** à la 8ème rangée (blancs) / 1ère rangée (noirs)

## 3. Tests réalisés (TDD)


**Tests fonctionnels** :

- Sélection pièce → highlighting immédiat
- Clic case possible → déplacement valide

## 4. Intégration continue

```test
Pipeline GitLab CI/CD :
├── Lint (ESLint)    npm run lint
├── Tests unitaires  npm test  
├── Documentation    npm run doc (JSDoc)
└── Build            

```

## 5. Issues traitées

| #   | Titre                                               | Statut      |
| --- | --------------------------------------------------- | ----------- |
| 1   | Erreur dans les tests fonctionnels                  | Corrigé     |
| 2   | Manque de commentaires                              | Corrigé     |
| 3   | Affichage de la dame trop tard lors de la promotion | Pas corrigé |

## 6. Difficultés & solutions

**Problème** : Affichage instantané de la Reine lors de la promotion
**Solution** : 
