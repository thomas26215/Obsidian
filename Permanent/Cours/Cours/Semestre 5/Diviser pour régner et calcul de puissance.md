---
MOOC: "[[Cours]]"
Ressource: "R5.04 : Qualité algorithmique"
Cours: "Cours 2 : Approche diviser pour régner, Première fonction qui calcule une puissance, Tri rapide, Tri par fusion"
Date:
tags:
Complete: false
Learned: false
---


# Qualité algorithmique – Cours 2 (Résumé Complet)

## Plan du cours

- **Approche Diviser pour Régner**
    
- **Calcul de Puissance (Trois algorithmes)**
    
- **Tri Rapide (Quick Sort)**
    
- **Tri par Fusion (Merge Sort)**
    

---

## 1. **Approche Diviser pour Régner**

La méthode "Diviser pour régner" consiste à :

1. Diviser le problème en sous-problèmes plus petits,
    
2. Résoudre chaque sous-problème (souvent de façon récursive),
    
3. Fusionner les solutions des sous-problèmes pour obtenir la solution globale.
    

**Exemple général :**

text

`Résoudre_le_problème(D)     si Trivial(D):        Renvoie un résultat direct    sinon:        (D1, D2) <- Diviser(D)        R1 <- Résoudre_le_problème(D1)        R2 <- Résoudre_le_problème(D2)        Résultat <- Fusionner(R1, R2)    fin`

_En tri, la division correspond à la séparation des données, la fusion correspond à la reconstruction du tableau trié._

---

## 2. **Calcul de puissance : trois algorithmes et leur coût**

## a. **Méthode itérative**

Pour calculer valn\text{val}^nvaln, multiplie n−1n-1n−1 fois si n>1n > 1n>1.

- Pour n=0n = 0n=0 ou n=1n = 1n=1 : 0 multiplication
    
- Pour n>1n > 1n>1 : n−1n-1n−1 multiplications
    

## b. **Récursion "brute" diviser pour régner**

Algorithme qui sépare nnn en deux à chaque étape, mais fait deux appels récursifs à chaque étape.

- Coût, pour n=2kn = 2^kn=2k : n−1n-1n−1 multiplications  
    (Jusqu'ici, aucun gain sur l'itératif)
    

## c. **Récursion "intelligente" diviser pour régner**

Un seul appel récursif à chaque étape (mémorise le calcul intermédiaire).

- Pour n=2kn = 2^kn=2k, nombre de multiplications : log⁡2n\log_2 nlog2n
    
- Beaucoup plus rapide pour les grands nnn.
    

**Formule finale :**

- Itératif : O(n)O(n)O(n) multiplications
    
- Récursif brut : O(n)O(n)O(n)
    
- Récursif optimisé : O(log⁡n)O(\log n)O(logn)
    

---

## 3. **Tri Rapide (Quick Sort)**

- **Découvert par Tony Hoare**
    
- **Non stable**
    

## Principe

- Choisir un pivot dans le tableau,
    
- Partager le tableau en deux :
    
    - A1A_1A1 : éléments ≤\leq≤ pivot
        
    - A2A_2A2 : éléments ≥\geq≥ pivot
        
- Trier A1A_1A1 et A2A_2A2 récursivement
    
- Fusion: rien à faire (le pivot et les deux sous-tableaux sont déjà ordonnés)
    

## Choix du pivot

- Idéal: médian, mais coûteux
    
- Pratique: "médian de trois" (gauche, milieu, droite) pour éviter cas défavorables
    

## Coût

- **Meilleur cas:** Ω(Nlog⁡2N)\Omega(N \log_2 N)Ω(Nlog2N) comparaisons
    
- **Pire cas:** O(N2)O(N^2)O(N2) (tableau déjà trié ou tous identiques)
    
- **Moyen:** O(Nlog⁡2N)O(N \log_2 N)O(Nlog2N)
    
- **In-place**, pas besoin de mémoire supplémentaire
    

---

## 4. **Tri par fusion (Merge Sort)**

- **Développé par John von Neumann**
    
- **Stable**
    

## Principe

- Diviser le tableau en deux moitiés
    
- Trier chaque moitié récursivement
    
- Fusionner les moitiés triées
    

## Algorithme (structure)

java

`void mergeSort(AnyType[] a, AnyType[] tmpArray, int left, int right) {     if (left < right) {        int center = (left + right) / 2;        mergeSort(a, tmpArray, left, center);        mergeSort(a, tmpArray, center + 1, right);        merge(a, tmpArray, left, center + 1, right);     } }`

**Fonction merge:** fusionne les deux sous-tableaux triés dans un tableau auxiliaire.

## Coût

- **Tous les cas** : O(Nlog⁡2N)O(N \log_2 N)O(Nlog2N) affectations et comparaisons
    
- Besoin de mémoire intermédiaire O(N)O(N)O(N)
    

---

## 5. **Bilan et comparaison**

|Algorithme|Stabilité|Complexité (Meilleur)|Complexité (Pire)|Complexité (Moyenne)|Mémoire|
|---|---|---|---|---|---|
|Quick Sort|Non|Ω(Nlog⁡2N)\Omega(N \log_2 N)Ω(Nlog2N)|O(N2)O(N^2)O(N2)|O(Nlog⁡2N)O(N \log_2 N)O(Nlog2N)|Faible|
|Merge Sort|Oui|Ω(Nlog⁡2N)\Omega(N \log_2 N)Ω(Nlog2N)|O(Nlog⁡2N)O(N \log_2 N)O(Nlog2N)|O(Nlog⁡2N)O(N \log_2 N)O(Nlog2N)|O(N)O(N)O(N)|

---

## **Pour réviser**

- Revoir l'idée de "diviser pour régner"
    
- Comprendre la différence entre les variantes d'exponentiation
    
- Savoir expliquer les principes et le coût du tri rapide vs tri fusion
    

**Pour être sûr d'avoir compris :**  
Pouvez-vous expliquer, avec vos mots :

- Ce qu'est le principe "diviser pour régner" ?
    
- Quelle est la différence entre un algorithme stable et instable pour le tri ?
    

Si besoin, dites-moi pour quel niveau ou pour quel examen vous révisez, je peux adapter ce résumé ou proposer des exercices !

1. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/24277945/2ae187c8-33ca-430b-b82d-05c3b554ee63/Cours-2.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/24277945/2ae187c8-33ca-430b-b82d-05c3b554ee63/Cours-2.pdf)