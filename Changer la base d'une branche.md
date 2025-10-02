# Cours sur Git Rebase (avec `git checkout`)

## 1. Qu’est-ce que git rebase ?

La commande `git rebase` permet de **changer la base d’une branche**.  
Elle prend une série de commits et les **rejoue sur un autre commit**, souvent pour intégrer les dernières modifications d’une branche principale sans créer de commit de fusion (`merge commit`).

**Objectifs principaux :**

- Simplifier l’historique de développement
    
- Intégrer des modifications d’une branche dans une autre sans commit de fusion
    
- Réécrire l’historique pour le rendre plus lisible
    

---

## 2. Fonctionnement de git rebase

### 2.1 Concept

Supposons deux branches :

```text
master: A---B
feature:  C---D
```

Si on fait :

```bash
git checkout feature
git rebase master
```

Git va :

1. Identifier le commit commun (`A`) entre les deux branches
    
2. Décoller les commits `C` et `D` de `feature`
    
3. Les réappliquer **après le dernier commit de `master` (`B`)**
    

Résultat :

```text
master: A---B
feature:     C'---D'
```

- Les commits `C'` et `D'` sont **nouveaux commits**, identiques dans le contenu mais avec des identifiants différents.
    
- L’historique devient **linéaire**, sans commit de fusion.
    

---

### 2.2 Rebase vs Merge

|Point|Merge|Rebase|
|---|---|---|
|Historique|Peut créer des commits de fusion|Réécrit l’historique linéaire|
|Clarté|Historique non linéaire|Historique plus clair|
|Partage des branches|Peut être partagé|Risque si branche déjà partagée|
|Conflits|À résoudre lors du merge|À résoudre commit par commit|

---

## 3. Utilisation de git rebase

### 3.1 Rebase simple

1. Se placer sur la branche à intégrer :
    

```bash
git checkout feature
```

2. Rebase sur la branche cible :
    

```bash
git rebase master
```

- Git rejoue tous les commits de `feature` sur `master`.
    
- Si des conflits apparaissent, Git stoppe le rebase et signale les fichiers conflictuels.
    

**Résolution d’un conflit pendant le rebase :**

```bash
# Modifier le fichier en conflit
git add <fichier>
git rebase --continue
```

- Pour abandonner le rebase :
    

```bash
git rebase --abort
```

---

### 3.2 Rebase interactif (`-i` ou `--interactive`)

Permet de **réécrire l’historique** et de modifier plusieurs commits.

```bash
git rebase -i <commit_ancien>
```

- Chaque commit est listé avec la commande par défaut `pick`.
    
- Les actions possibles :
    
    - `pick` : conserver le commit tel quel
        
    - `reword` : modifier le message du commit
        
    - `edit` : modifier le contenu du commit
        
    - `squash` : fusionner ce commit avec le précédent
        
    - `fixup` : comme `squash` mais ignore le message de commit
        
    - `drop` : supprimer le commit
        

**Exemple de fichier interactif :**

```text
pick ac1345c initial commit
reword 74d41b0 doc: README
pick 882c921 code: first version
squash 0aaccd9 code: fix shabang
```

- Après modification, enregistrer et quitter l’éditeur.
    
- Git rejoue les commits en appliquant les actions demandées.
    

---

### 3.3 Rebase depuis la racine (`--root`)

```bash
git rebase -i --root
```

- Permet de réécrire l’historique **depuis le premier commit**.
    
- Très utile pour corriger ou fusionner les premiers commits du projet.
    

---

## 4. Bonnes pratiques avec git rebase

- **Ne jamais rebaser une branche partagée publiquement** → risque de conflits et perte de commits pour les autres contributeurs.
    
- **Faire un backup ou clone du dépôt** avant de faire un rebase complexe.
    
- **Utiliser le mode interactif** pour :
    
    - Corriger des messages de commit
        
    - Fusionner ou supprimer des commits inutiles
        
    - Simplifier l’historique avant l’intégration
        
- **Résoudre les conflits étape par étape** avec `git status` et `git rebase --continue`.
    

---

## 5. Exemple complet

1. Branches initiales :
    

```text
master: A---B
feature:  C---D
```

2. Rebase de `feature` sur `master` :
    

```bash
git checkout feature
git rebase master
```

3. Résultat :
    

```text
master: A---B
feature:     C'---D'
```

- L’historique est linéaire.
    
- Plus clair que `merge` avec un commit de fusion.
    

4. Rebase interactif pour fusionner `C'` et `D'` :
    

```bash
git rebase -i B
# Choisir squash sur D'
```

- Résultat final : un seul commit `C+D` appliqué après `B`.
    

---

### 6. Résumé

- `git rebase` = déplacer une branche pour la rebaser sur une autre.
    
- Historique linéaire → plus lisible.
    
- Mode interactif → puissant pour modifier et simplifier l’historique.
    
- Attention à ne pas réécrire l’historique partagé.
    
- Toujours résoudre les conflits étape par étape avec `git status` et `git rebase --continue`.
    