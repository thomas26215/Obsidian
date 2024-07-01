---
MOOC: "[[Programmation]]"
Langage: Kotlin
Type: Compilateur
tags:
---
Le [[Compilateur|compilateur]] qu'utilise Kotlin est appelé *Kotlin Compiler* (*kolinc* en abrégé). C'est celui qui est responsable de la transformation du code source Kotlin en bytecote Java ou en fichier exécutable
Le compilateur est écrit en Kotlin lui-même + distribué avec kit de développement Kotlin (***SDK***) qui est fournit par [[JetBrains]]. Les IDE associés sont IntelliJ IDEA, Android Studio, Eclipse ...
Ce compilateur permet différentes options de compilation, telles que la spécification du niveau de compatibilité avec [[Java]] (facilités de transfert de code Java - Kotlin + bibliothèques Java utilisable dans Kotlin et inversement), la génération de fichiers de débogage, l'optimisation du code ...
Cependant, Kotlin utilise aussi un [[Interpréteur|interpréteur]], mais le compilateur est le composant principale pour la production du code exécutable L'interpréteur est généralement utilisé pour faire des tests, pour naviguer plus facilement dans le code
> **Résumé** : Le langage Kotlin utilise son propre compilateur qui permet de traduire le code source Kotlin en [[Bytecode]] java


### Le lien avec la JVM
Il est important de noter que la JVM (Java Virtual Machin) permet de faire tourner du code Java mais aussi du code Kotlin. En effet, comme mentionné plus tôt, le compilateur va transformer le code source Kotlin en bytecode Java, tout comme le code Java traditionnel. Celui-ci va pouvoir être exécuté dans la machine virtuelle Java

Il est important de noter que Kotlin dispose tout de même de sa propre *runtime* ("Kotlin Runtime"), qui peut être utilisé sans dépendre de la JVM ; mais la JVM reste tt de même privilégié. La Kotlin Runtime est utilisé pour des cas spécifiques (plate-forme embarquées, générer du code natif)