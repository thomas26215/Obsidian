---
MOOC: "[[Cours]]"
Ressource: 
Cours: 
Date: 
tags: 
Complete: false
Learned: false
---
# 1. Taille des différentes mémoires de la hiérarchie

| Type de mémoire                               | Taille dans votre station |     |
| --------------------------------------------- | ------------------------- | --- |
| Registres d'usage général                     | 31 GiB                    |     |
| Cache de données de niveau 1 (L1 D cache)     | 288KiB                    |     |
| Cache d'instructions de niveau 1 (L1 I cache) | 192kib                    |     |
| Cache unifié de niveau 2 (L2 cache)           | 7.5Mib                    |     |
| Cache unifié de niveau 3 (L3 cache)           | 18Mib                     |     |
| Mémoire RAM                                   | 31G                       |     |
| Swap                                          | 1G                        |     |

# 2. Comparaison entre registres et mémoire
**Question 1**

| Numéro d'expérience | Mot clé lors de la déclaration des variables | Temps d'exécution du programme en secondes                   |
| ------------------- | -------------------------------------------- | ------------------------------------------------------------ |
| 1                   | volatile                                     | real    0m2,261s  <br>user    0m2,259s  <br>sys     0m0,000s |
| 2                   | register                                     | real    0m0,573s  <br>user    0m0,567s  <br>sys     0m0,005s |
| 3                   | ø                                            | real    0m0,574s  <br>user    0m0,567s  <br>sys     0m0,004s |
**Question 2**

> **Analyse du code assembleur**
>1. `i < N;` : Cette comparaison est traduite par `cmp rax, 1500000000`, où rax contient la valeur de i.
>2. `++i` : L'incrémentation est effectuée avec `add rax, 1`.
>3. `if (i%STEP)` : Cette condition est traduite par `test al, 3`, qui vérifie si les deux bits de poids faible de i sont non nuls (équivalent à i%4).
>4. `suite += R;` : Cette addition est effectuée avec `addsd xmm0, xmm1`, où xmm0 contient suite et xmm1 contient R.
>
>**Impact des déclarations**
>
>1. Sans `register` : Le code assembleur reste inchangé car le compilateur avec -O2 optimise déjà l'utilisation des registres.
>2. Avec `volatile` : L'utilisation de `volatile` empêche certaines optimisations:
>  
>    - Les variables sont chargées depuis et stockées en mémoire à chaque accès.
 >   - La boucle n'est pas déroulée.
>    - Les calculs ne sont pas simplifiés ou éliminés.
>    
>
>**Observations**
>
>- Les constantes #define sont directement intégrées dans le code assembleur, sans occuper de registre.
>- L'optimisation -O2 produit un code efficace, utilisant les registres de manière optimale.
>- `volatile` force le compilateur à accéder à la mémoire pour chaque opération, ralentissant l'exécution mais garantissant que les accès sont effectués comme spécifié dans le code source.
# 3. Caches, RAM et swap
## 3.1. Compréhension du code

**Question 1**
> 1. Toutes les données nécessaires sont déjà présentes dans ce niveau de cache.
>2. Les accès répétés au tableau se font sans avoir besoin d'aller chercher des données dans les niveaux supérieurs.
>3. Cela minimise les défauts de cache pour ce niveau spécifique.

**Question 2**
>1. Chaque accès saute à une adresse non contiguë, empêchant l'utilisation efficace du préchargement des lignes de cache.
>2. Les données chargées dans les niveaux inférieurs sont rapidement remplacées avant d'être réutilisées.
>3. Cela force des défauts de cache fréquents dans les niveaux inférieurs, invalidant leur localité temporelle.

## 3.2. Expériences

| Numéro d'expé. | Expérience à réaliser sur un tableau... | Taille du tableau en octets | durée CPU | durée réelle | Nombre de défauts de page mineurs | Nombre de défauts de page majeurs | Nombre d'accès au tableau par seconde |     |
| -------------- | --------------------------------------- | --------------------------- | --------- | ------------ | --------------------------------- | --------------------------------- | ------------------------------------- | --- |
| 1              | occupant la moitié du cache L1          |                             |           |              |                                   |                                   |                                       |     |
| 2              | occupant la moitié du cache L2          |                             |           |              |                                   |                                   |                                       |     |
| 3              | occupant la moitié du cache L3          |                             |           |              |                                   |                                   |                                       |     |
| 4              | occupant la moitié de la RAM            |                             |           |              |                                   |                                   |                                       |     |
| 5              | débordant sur le swap                   |                             |           |              |                                   |                                   |                                       |     |

# 4. Effet de la régularité des accès mémoire sur le cache
**Question 1**
> Le programme tableau2d.c utilise un tableau carré à 2 dimensions et permet de le parcourir de deux manières différentes : par lignes ou par colonnes.

**Question 2**
>Par défaut, le programme réalise un parcours par lignes.


**Question 4**

| Expérience à réaliser | Nombre de lignes du tableau (= nb de colonnes) | Taille du tableau en octets | Durée CPU   | Durée réelle | Nombre d'accès au tableau par seconde | Taux de défauts de cache de données L1 en lecture (D1 miss rate, colonne rd) |
| --------------------- | ---------------------------------------------- | --------------------------- | ----------- | ------------ | ------------------------------------- | ---------------------------------------------------------------------------- |
| parcours par lignes   | [à remplir]                                    | [à remplir]                 | [à remplir] | [à remplir]  | [à remplir]                           | [à remplir]                                                                  |
| parcours par colonnes | [à remplir]                                    | [à remplir]                 |             |              |                                       |                                                                              |