# Alphabets, langages et expressions régulières

## Alphabets, langages

Un alphabet noté $A$ est un ensemble non vide de symboles appelés lettres

Un mot, définit sur un alphabet $E$ est une suite d'éléments de $A$

La longueur d'un mot $u$ définit sur un alphabet $A$ est noté $|u|$ et est le nombre de symboles qui composent $u$
Le mot vide noté $e$ est définit sur tous les alphabets et est le mot de longueur 0. Ainsi, $|e|=0$
$A⁺$ désigne des mots de longueurs de longueur supérieur ou égale à 1 que l'on peut construire à partir de l'alphabet $A$
$A^*$ désigne l'ensemble des mots que l'on peut construire à partir de $A$ y compris le mot vide : $A^*=\{e\}^\cup A^+$

Sur un alphabet $A$, on peut faire suivre deux mots $u$ et $v$ notés $uv$. $uv$ est donc le mot formé en faisant suivre les lettres de $u$ puis les lettres de $v$

Un langage définit sur $A$ est un ensemble de mots définis sur $A$. Autrement dit, un langage est un sous-ensemble de $A^*$
On distingues deux langages particuliers :
- Le langage vide
- Le langage contenant le seul mot vide
## Langages réguliers et expressions régulières

La classe des langages réguliers est la classe la plus petite qui contienne
les langages finis et qui soit stable par les opérations de réunion, concaténation, "étoile".
Autrement dit, les seuls langages réguliers sont les langages qu’il est possible de fabriquer à
l’aide des deux règles suivantes :
- Tout langage fini est régulier
- Si L et L′ sont réguliers, alors L ∪ L′, L.L′ et L∗ sont réguliers

Une expression E est une expression régulière sur
un alphabet A si et seulement si
- $E = ∅$ ; ou
- $E = ϵ$ ou
- $E = a$ avec $a ∈ A$ ou
- $E = E1 + E2$ et $E1$ et $E2$ sont deux expressions régulières sur A ou
- $E = E1.E2$ et $E1$ et $E2$ sont deux expressions régulières sur A ou
- $E = E∗$
$1$ et $E1$ est une expression régulière sur $A$.
Les opérateurs $∗, .$ et $+$ ont une priorité décroissante. Si nécessaire, on peut ajouter des
parenthèses.

e langage L(E) décrit par
une expression régulière E définie sur un alphabet A est défini par
- $L(E) = ∅$ si $E = ∅$
- $L(E) = {ϵ}$ si $E = ϵ,$
- $L(E) = {a}$ si $E = a$,
- $L(E) = L(E1) ∪ L(E2)$ si $E = E1 + E2$,
- $L(E) = L(E1).L(E2)$ si $E = E1.E2$,
- $L(E) = L(E1)∗$ si $E = E∗$
$1$ où $E1$ est une expression régulière sur $A$

# Cours sur les Automates Finis

## 1. Définition d'un automate fini

Un automate fini est défini comme un quintuplet $A = (\Sigma, Q, \delta, I, F)$, où $\Sigma$ est l'alphabet d'entrée, $Q$ est l'ensemble fini d'états, $\delta$ est la fonction de transition ($\delta : Q \times \Sigma \rightarrow Q$), $I \subseteq Q$ est l'ensemble des états initiaux, et $F \subseteq Q$ est l'ensemble des états finaux (ou terminaux). Dans notre cas spécifique, les états initiaux sont 1 et 4, et les états finaux sont 3 et 6.

## 2. Représentation graphique

Un automate fini est représenté par un graphe orienté, où les nœuds représentent les états, les arcs représentent les transitions étiquetées par les symboles de l'alphabet, les états initiaux sont indiqués par une flèche entrante, et les états finaux sont représentés par des cercles doubles.

![[Pasted image 20250310214226.png]]

## 3. Types d'automates finis

### 3.1 Automate fini déterministe (AFD)

Un automate fini déterministe possède un seul état initial et une seule transition par état et symbole d'entrée. Cela signifie que pour chaque état et chaque symbole de l'alphabet, il n'existe qu'une seule transition possible.

### 3.2 Automate fini non déterministe (AFN)

Un automate fini non déterministe peut avoir plusieurs états initiaux et plusieurs transitions possibles pour un même état et symbole d'entrée. De plus, il peut inclure des transitions $\varepsilon$ (epsilon), qui permettent de changer d'état sans consommer de symbole.

## 4. Automate complet

Un automate est dit complet si pour chaque état et chaque symbole de l'alphabet, il existe au moins une transition sortante. Cela garantit que l'automate peut toujours évoluer vers un autre état, quel que soit le symbole lu.

## 5. Fonctionnement d'un automate

Le fonctionnement d'un automate commence par le départ d'un état initial. Ensuite, il lit les symboles d'entrée un par un et effectue une transition vers un nouvel état selon la fonction $\delta$ pour chaque symbole lu. Finalement, le mot est accepté si l'automate se trouve dans un état final après avoir lu tous les symboles.

## 6. Opérations sur les automates

### 6.1 Complétion d'un automate

Pour compléter un automate, on ajoute d'abord un état puits. Ensuite, on ajoute des transitions manquantes vers cet état puits pour chaque état et symbole pour lequel aucune transition n'existe. Enfin, on ajoute des transitions de l'état puits vers lui-même pour tous les symboles de l'alphabet.

### 6.2 Déterminisation

La déterminisation consiste à convertir un automate fini non déterministe (AFN) en un automate fini déterministe (AFD) équivalent. Cela permet de simplifier l'analyse et la manipulation des automates.

### 6.3 Minimisation

La minimisation d'un automate consiste à réduire le nombre d'états tout en préservant le langage reconnu. Cela améliore l'efficacité de l'automate en réduisant sa complexité.

## 7. Applications des automates finis

Les automates finis sont utilisés dans divers domaines, notamment l'analyse lexicale dans les compilateurs, le traitement des langues naturelles, la conception de circuits logiques, et la vérification de protocoles de communication.

## Conclusion

Les automates finis sont des outils essentiels en informatique théorique et appliquée, offrant un modèle simple mais puissant pour représenter des systèmes à états finis.


# AF vers AFDC
## Equivalence entre AF et AFDC
La famille des langages acceptés par un AF déterministe est identique à la famille des langages acceptés par un AF non déterministe 