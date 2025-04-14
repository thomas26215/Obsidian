


# Versionnage
Nous travaillons sur 3 versions :
- La version de production qui est la version la plus ancienne, celle où on est sûre qu'elle marche
- La version de tests qui est la une version supérieure par rapport à la version de test
- La version de dév qui est un version supérieure par rapport à la version de test

>[!Example]
> - **Version de production** : `2.65`
> - **Version de test** : `2.66`
> - **Version de développement web** : `2.67`


Quand La version de test est totalement testée et qu'on décide de la passer en production, chaque version prend une version supérieure :
- **Version de production** <- Version de test
- **Version de test** <- Version de développement
- **Version de développement** <- `dev_version += 1`
> [!Example]
> En se référant à l'exemple :
> - **Version de production** : `2.66`
> - **Version de test** : `2.67`
> - **Version de développement web** : `2.68`





# Organisation physique de l'usine
```mermaid
flowchart LR
P(Plant) --> I1(Ilot 1)
P-->I2(Ilot 2)
P-->I...(...)
P-->In(Ilot n)

I1-->WC1(WorkCenter 1111)
I1-->WC2(WorkCenter 1112)
I1-->WC...(WorkCenter ...)
I1-->WCn(WorkCenter n)

WC1-->WS1(Workstation 1)
WC1-->WS2(Workstation 2)
WC1-->WS...(...)
WC1-->WSn(Workstation n)
```

![[Exemple d'une Plant.excalidraw]]