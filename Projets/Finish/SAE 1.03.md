**Exercice binaire**
1. The word #$0010 is moved to d0. d0 now contains 0000 0000
2. Nous donnes la valeur de `d0` au bit `$00000040`
3. The word from d0 is moved to d1. 0010 is copied. d1 now contains 0000 0000 (plutot 0000 0010)
4. A word from d1 is added to itself. d1 now contains 0000 0020
5. A word from d0 is added to d1. d1 now contains 0000 0030
6. A word from offset 0000 0040 is loaded and is substracted fro md1. (0030-0010). d1 now contains 0000 0020
7. d1 is swapped. d1 now contains 0020 0000
8. A word from d0 is moved to d1, now contains 00200010
9. #$0000 0040 is moved to a4. a4 now contains 0020 0010
10. a4 is add to d1. d1 nwo contains 0020 0020
12. The long in d1 and d0 are exchanged. d0 now contains 0020 0020 and d1 now contains 0000 0010.
13. ...