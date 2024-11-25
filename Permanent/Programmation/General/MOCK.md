---
MOOC: "[[Programmation]]"
Langage: General
Type: MOCK
tags:
---
Le mocking est une technique de programmation utilisable dans de nombreux langages.

Le <mark style="background: #ADCCFFA6;">principe fondamentale</mark> est la simulation de comportement d'objets réels de manière contrôlée pour les tests et est universelle en langage de programmation. C'est un processus de simulation des dépendances externes du code qui est testé. On va donc isoler notre code de la multitude de choses dont il dépend. La simulation peut prendre deux formes : des données factices ou des interactions factices

<mark style="background: #ADCCFFA6;">L'objectif</mark> est d'isoler le code testé en remplaçant les dépendances par des objets simulés dont le comportement est contrôlé

<mark style="background: #BBFABBA6;">Par exemple</mark> : [[MOCK sur une BDD]]

- Il est nécessaire de mocker quand le code détient des dépendances lentes. Par exemple, si une fonction dépend d'une API externe, on ne veut probablement pas faire un appel API à chaque fois que l'on exécute un test
- Il peut également être nécessaire de mocker quand un test est non déterministe. Par exemple, notre fonction dépend de l'heure actuelle ; Il faudrai probablement mocker pour que les tests soient cohérents
- On peut mocker quand les dépendances sont difficiles à configurer : si ma fonction dépend d'une service tiers, on ne veut probablement pas configurer ce service tiers juste pour tester une fonction
- Finalement, si les dépendances ne sont pas le focus du test, il peut être nécessaire de mocker. Par exemple, si je teste une fonction sur une BDD, et que l'on ne teste pas spécifiquement l'interaction avec la BDD, il est probable que l'on utiliser une MOCK