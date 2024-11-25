---
MOOC: "[[Programmation]]"
Langage: PHP
Type: Chaînes de charactères
tags: 
Complete: true
Learned:
---
Les chaînes de caractères en PHP ont quelques particularités importantes :

- PHP ne supporte pas nativement l'UTF-8, les caractères sont sur 1 octet seulement.
- La concaténation se fait avec le point (.) et non le plus (+).
- Il existe deux types de délimiteurs : les apostrophes (') et les guillemets (").

## Différences entre apostrophes et guillemets

**Apostrophes ('')** :

- Aucune interprétation des caractères spéciaux sauf ' et \.
- Les variables ne sont pas interpolées.

**Guillemets ("")** :

- Interprétation des caractères d'échappement (ex: \n).
- Interpolation des variables

![[Interpolarisation des variables]]