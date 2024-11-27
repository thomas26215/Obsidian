---
MOOC: "[[Cours]]"
Ressource: "R3.05 : Processus"
Cours: "TP01 : Processus - création, terminaison"
Date: 
tags: 
Complete: false
Learned: false
---
# 1 - Observations
## 1.1. Arbre des processus
**Question 1**
```bash
venouilt@iut2-dg037-d09:~/R3.05/tp01$ pstree -uphT 149790  
bash(149790,venouilt)───pstree(152052)
```
> Le PID du processus `shell`est **149790**
> Son père est **konsole** de PID **135280**
> Bash possède un **fils** qui est **pstree** de **PID** **153900**

**Question 2**
> Après avoir ouvert Firefox par le shell et exécuté `pstree -uphT`, Les fils du shell sont `cat`, `chrome`

**Question 3**
> Il est intéressant qu'un shell crée un processus fils pour exécuter une commande plutôt que de l'exécuter lui-même, car cela permet au shell de rester disponible et fonctionnel après l'exécution. En isolant les commandes dans des processus fils, le shell protège son propre fonctionnement en cas d'erreur ou de plantage de la commande. De plus, cette approche permet au shell de gérer plusieurs commandes simultanément, offrant ainsi flexibilité et contrôle, comme la possibilité d'attendre la fin d'un processus ou de l'interrompre. En somme, cela garantit une utilisation plus stable et efficace du shell.

**Question 4**
> Un navigateur web crée d'autres processus principalement pour améliorer la stabilité, les performances et la sécurité. En isolant chaque onglet, extension ou tâche dans un processus distinct, il évite qu'un problème dans un onglet n'affecte l'ensemble du navigateur. Cette approche multi-processus permet de répartir la charge de travail sur plusieurs cœurs du processeur, d'améliorer la gestion des ressources et de limiter les risques de propagation des failles de sécurité. Ainsi, le navigateur peut exécuter des tâches en arrière-plan, comme des téléchargements, sans compromettre l'expérience de navigation principale.

## 1.2. Ordonnancement
**Question 1** :
```shell
venouilt@iut2-dg037-d09:~/R3.05/tp01$ time ./bin-gcc/exploration 1  
  
OUEST Explorateur 0 : position finale = 20299  
  
real    0m3,806s  
user    0m3,798s  
sys     0m0,002s
```

**Question 2** :
```shell
venouilt@iut2-dg037-d09:~/R3.05/tp01$ time ./bin-gcc/exploration 10  
  
                                                  EST Explorateur 5 : position finale = -10795  
OUEST Explorateur 8 : position finale = 25293  
                                                  EST Explorateur 9 : position finale = 2079  
OUEST Explorateur 4 : position finale = -5686  
                                                  EST Explorateur 1 : position finale = -29745  
OUEST Explorateur 6 : position finale = 19284  
                                                  EST Explorateur 7 : position finale = -14304  
OUEST Explorateur 2 : position finale = -16031  
                                                  EST Explorateur 3 : position finale = -2419  
OUEST Explorateur 0 : position finale = 14945  
  
real    0m6,933s  
user    0m38,290s  
sys     0m0,032s
```

> Depuis htop, on voit :
> - **Nombre de coeurs** : 6
> - **Priorité de processus** :


**Question 3** :
> La durée totale d'exécution est environ six fois moins élevée que la durée d'exécution sur le CPU en raison du parallélisme, et non d'un ordonnancement Round-Robin (RR). Cette différence s'explique par l'utilisation simultanée de plusieurs cœurs du processeur


### Questions sur l'ordonnancement mêlant RR et priorités
**Question 1** :
> L'entremêlement des affichages West et East est une conséquence directe de l'ordonnancement Round-Robin (RR), qui attribue à chaque processus une tranche de temps fixe (quantum) et les fait progresser de manière cyclique. En donnant à chaque processus une part égale du temps processeur et en basculant rapidement entre eux avant qu'un processus ait terminé son exécution, le RR crée l'illusion d'une exécution simultanée. Chaque processus est préempté et replacé dans la file d'attente avant d'avoir terminé, ce qui provoque l'alternance rapide des affichages et donne l'impression que tous les processus s'exécutent et s'affichent en même temps.

**Question 2** :



### Programmation système
