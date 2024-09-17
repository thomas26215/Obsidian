---
MOOC: "[[Programmation]]"
Langage: C++
Type: Classes
tags:
---
L'utilisation de la classe vis à vis de la mémoire est sûre si les différents éléments suivants sont codés

| Prototype                     | Fonctionnalité                               |
| ----------------------------- | -------------------------------------------- |
| **T::T()**                    | [[Le constructeur\|Constructeur par défaut]] |
| **T::T(const T&)**            | [[Constructeur par recopie]]                 |
| **T& T::operator=(const T&)** | Opérateur d'affectation                      |
| **T::~T()**                   | [[Le destructeur\|Destructeur]]              |
