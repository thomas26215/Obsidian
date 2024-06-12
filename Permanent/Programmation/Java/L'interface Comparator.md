---
MOOC: "[[Programmation]]"
Langage: Java
Type: Tri d'objets
tags:
---
>[!Warning]
>Impératif de savoir utiliser `Comparable`

Il se peut que l'utilisation de [[Interface Comparable]] ne suffise pas. En effet, cette interface ne trie que d'une seule manière, mais il se peut que l'on souhaite trier selon certains critères.
L'interface Comparator pemet de créer des objets *comparateur* `monComparateur` et les passer en arguments à certaines méthodes (`Collection.sort(maCollection, monComparateur);`) ou à certains constructeurs (`TreeSet<>(monComparateur);`)

![[Solution 1 pour implémenter le Comparator]]
![[Solution 2 pour implémenter le Comparator]]