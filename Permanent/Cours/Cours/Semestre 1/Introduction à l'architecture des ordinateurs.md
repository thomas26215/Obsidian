---
MOOC: "[[Cours]]"
Ressource: "R1.03 : Architecture des ordinateurs (données et instructions)"
Cours: "Cours 1 : Introduction"
Date: 2023-11-13
tags: 
Complete: false
Learned: false
---
Toute instruction est codé en 0 et 1
Les données et instructions sont lues en mémoire centrale lors de l'exécution d'un programme
Le processeur passe son tps à lire des instructions codées en base 2
Pour que le processeur puisse comprendre des instructions très variées uniquement en base 2,
Il existe de très nombreuses types de données :
- Couleur
- Sons
- Images
Il faut aussi trouver une manière de coder les données (ASKII / UNICODE pour coder du texte, base 2 pour représenter des nombres)
→ **Exemple :** `'A' = %0100 0000`

>**Avoir compris :**
> → La méthode de codage : Base deux, ASCII
> → Sur quelle longueur est représentée la donnée

Fusée Arianne : explosée car données mal comprises. Pas assez long pour représenter correctement la donnée
Représentation externe = représentation pour les humains (`48`)
Représentation interne = à l'ordinateur (`0` et `1`)
externe → Codage → interne
interne → Décodage → Externe

`%0101` - Le `%` devant = notation binaire
→ 4 valeur binaires - 4 binary elemenT (Bits)
`%1000 0110` = 1 octet
Pour comprendre ce qui est encodée, il faut préciser la méthode de codage

Sur 4 bits, je peut représenter 16 valeurs distinctes ($2^4$)
Sur la droite, on parle de poids faibles et sur la gauche, de poids forts. Les bits de poids faibles ont une influence moindre sur la valeur totale par rapport aux bits de poids forts.

`%0000`, `%0001`, `%0010`, `%0011` ...
Je ne sais pas ce que ca représente, je n'ai pas précisé la méthode d'encodage


`$45E1B` - Le `$` devant = notation hexadécimale
`%0101` = `$5`
`%1000 0100` = `$86`

`<%...>` Méthode de codage
`<$...>` Méthode de codage
`<%10>deux` = `<2>dix`

**Rappel base 10 :** `<203>dix` = $2*10^2+0*10^1+3*10^0$
→ Représentation pondérée
→ Chaque nombre a une représentation unique (donc une base donnée)
→ Adaptée au calcul

Pour passer de la base 10 à la base 2 :
`<19>dix` = 16 + 2 + 1
= `<%10011>deux` = `<$13>deux` ⇒ C'est sur deux octets (`%0001 0011` ⇒ `$1 3`)
⇒ On regarde la puissance de deux la plus élevée et on continue pour chaque résultat

Pour passer de décimale à binaire, il existe mé thode simple applicable à tous nombres. Il suffit de réaliser des divisions successives. A chaque fois, on récupère le résultat que l'on redivise par deux. Le reste sert pour la représentation binaire. A la fin, on inverse et on à la représentation binaire

`<92>dix`. On divise successivement par deux :
<mark style="background: #ABF7F7A6;">92</mark> / 2 = <mark style="background: #ABF7F7A6;">46</mark>,<mark style="background: #FF5582A6;">0</mark>
<mark style="background: #ABF7F7A6;">46</mark>/2 = <mark style="background: #ABF7F7A6;">23</mark>,<mark style="background: #FF5582A6;">0</mark>
<mark style="background: #ABF7F7A6;">23</mark>/2=<mark style="background: #ABF7F7A6;">11</mark>,<mark style="background: #FF5582A6;">1</mark>
<mark style="background: #ABF7F7A6;">11</mark>/2 = <mark style="background: #ABF7F7A6;">5</mark>,<mark style="background: #FF5582A6;">1</mark>
<mark style="background: #ABF7F7A6;">5</mark>/2 = <mark style="background: #ABF7F7A6;">2</mark>,<mark style="background: #FF5582A6;">1</mark>
<mark style="background: #ABF7F7A6;">2</mark>/2 = <mark style="background: #ABF7F7A6;">1</mark>,<mark style="background: #FF5582A6;">0</mark>
<mark style="background: #ABF7F7A6;">1</mark>/2 = 0,<mark style="background: #FF5582A6;">1</mark>
(A gauche quotient à droite reste)
⇒ `<%01011100>deux` = `<$5C>deux`

`<203>dix` = `<%11001011>deux`
`<213>dix` = `<%11010101>deux`
`<4B>deux` = `<75>dix`

La dynamique du codage est liée à la capacité du système de codage à représenter un certain nombre de configurations distinctes, et dans le contexte binaire, cela est souvent lié au nombre d'bits utilisés. Une dynamique de codage plus élevée signifie généralement une capacité à représenter un plus grand nombre de valeurs uniques.

Calculer 92 + 20 : `%0101 1100` + `%0001 0100` = `%0111 0000`

---
**Questions**
1. En quoi est codée une information ?
2. Où sont lues les données et les instructions ?
3. Comment coder une information ? Donner deux manières
4. Qu'est ce que la représentation externe ? Interne ?
5. Comment s'appelle la méthode pour passer de la représentation interne à externe ? Et inversement ?
6. Comment indiquer qu'une information est en binaire ? Et en héxadécimale ?
7. Sur 4 bits, je peut représenter combien de valeurs ?
8. Comment informer la base d'une donnée (base 10, base 2 ...)
9. Convertir 4B (base deux) en base dix. De même pour 203 et 213 (base dix) en base deux
10. Pourquoi utilise-t-on différentes méthodes de codage pour représenter des informations telles que le texte, les images et les sons ?
11. Expliquez le concept de poids faibles et poids forts dans la représentation binaire.
12. Quelle est la signification du terme "dynamique du codage" dans le contexte donné ?
13. Quelle est la relation entre la dynamique du codage et le nombre d'octets nécessaires pour représenter une information?
14. Comment calculer la somme de deux nombres binaires?