# Cours sur le merge (intégration de modifications)

## Qu’est-ce que le merge dans Git ?

La commande `git merge` permet de combiner le travail de plusieurs branches en une seule. Elle sert à intégrer les modifications de différentes lignes de développement dans une branche cible, généralement la branche principale (souvent appelée `main` ou `master`).

Le merge permet de reconstituer un historique qui peut être « forké » et fusionné, c’est-à-dire que Git va rassembler les modifications effectuées indépendamment dans plusieurs branches.

---

## Comment fonctionne git merge ?

Lorsque tu exécutes une commande comme :

```bash
git merge <branche_source>
```

Git va :

1. Trouver le **commit commun le plus récent** entre la branche courante (branche cible) et la branche source.
    
2. Comparer les différences sur les deux branches depuis ce commit commun.
    
3. Fusionner automatiquement ces différences si possible.
    
4. En cas de divergence (modifications concurrentes), créer un **commit de fusion** (merge commit) qui a **deux parents** : un pour chaque branche fusionnée. Ce commit synthétise les deux historiques.
    
5. Si Git ne peut pas fusionner automatiquement à cause de conflits, il te le signale, et tu dois intervenir pour résoudre ces conflits.
    

---

## Types de fusion dans Git

### 1. Fast-forward (avancement rapide)

- C’est la fusion la plus simple.
    
- Elle se produit si la branche courante est un ancêtre de la branche source.
    
- Git "avance" simplement le pointeur de la branche courante sans créer de commit de fusion.
    

Exemple :

Avant fusion :

```
master: A---B
feature:      C---D
```

Commande :

```bash
git checkout master
git merge feature
```

Résultat (fast-forward) :

```
master: A---B---C---D
```

---

### 2. Fusion à trois voies (Three-way merge)

- Se produit lorsque les deux branches ont divergé avec des commits différents.
    
- Git crée un commit spécial de fusion avec deux parents, qui combine les deux historiques.
    

Exemple :

Avant fusion :

```
A---B---E (master)
      \
       C---D (feature)
```

Après fusion :

```
A---B---E------M (master)
      \       /
       C---D
```

(M est le commit de fusion)

---

## Commandes importantes liées au merge

- Se positionner sur la branche cible avant de fusionner :
    

```bash
git checkout master
git merge feature
```

- Forcer la création d’un commit de fusion, même si fast-forward possible :
    

```bash
git merge --no-ff feature
```

- Faire un merge rapide uniquement, sinon échouer :
    

```bash
git merge --ff-only feature
```

- Annuler une fusion en cours en cas de conflit ou d’erreur :
    

```bash
git merge --abort
```

---

## Résolution des conflits

Quand Git ne peut pas fusionner automatiquement certaines modifications (exemple : même fichier modifié différemment dans les deux branches), il marque un conflit dans les fichiers :

```
<<<<<<< HEAD
version branche actuelle
=======
version branche fusionnée
>>>>>>> feature
```

Pour résoudre ce conflit :

1. Modifier les fichiers pour choisir ou fusionner les modifications.
    
2. Ajouter les fichiers corrigés à l’index avec :
    

```bash
git add <fichier>
```

3. Terminer la fusion avec un commit automatique généré par Git :
    

```bash
git commit
```

Tu peux aussi utiliser des outils graphiques comme `git mergetool` pour visualiser et résoudre les conflits plus facilement.

---

## Bonnes pratiques pour le merge

- Toujours faire un `git fetch` et `git pull` pour être sûr d’avoir les dernières modifications avant de fusionner.
    
- Favoriser des merges clairs et éviter des branches trop anciennes pour minimiser les conflits.
    
- Utiliser `--no-ff` pour garder une trace explicite des merges et conserver une meilleure lisibilité historique.
    
- Résoudre soigneusement les conflits ; en cas d’erreur, utiliser `git merge --abort`.
    

---

## En résumé

- Le merge combine deux branches en intégrant les modifications.
    
- La fusion peut être un **fast-forward** simple ou une **fusion à trois sources** avec commit de fusion.
    
- En cas de conflits, une intervention manuelle est requise.
    
- Les options comme `--no-ff` ou `--ff-only` permettent de contrôler la nature de la fusion.
    
- La commande `git merge` est un pilier de la collaboration avec Git, idéal pour intégrer facilement des lignes de développement parallèles.
    
