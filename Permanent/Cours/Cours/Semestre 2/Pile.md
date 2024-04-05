---
MOOC: "[[Cours]]"
Ressource: R2.04a  :Fonctionnement bas niveau
Cours: "Cours 2 : Piles"
Date: 2024-02-07
tags: 
Complete: false
Learned: false
---
Une pile est délimitée par deux adresses en mémoire désignant :
- **La base de la pile** : `0x0000 0000`
- **Le sommet de la pile** : `%sp`(adresse)
	- Valeur au sommet de la pile : ***`(%sp)`***
Au début du programme, ce registre a pour valeur l'adresse de la base de la pile. Valeur fixée par les lignes suivantes :
```SEGA MEGA DRIVE
ORG 0x0000
DC.L 0x8000 ; Le pointeur de pile est fixé à 0x8000 soit A7:=0x0800
DC.L DEBUT
```

Une pile est une zone de la mémoire. Elle est principalement utilisée pour l'appel de sous-programmes par empilement :
1. Valeur des paramètres d'un appel de sous-programme
2. Variables locales
3. Adresse de retour du sous-programme

> [!tip] Utilisation de la pile
> - **En écriture :** Placer une donnée au sommet de la pile (`MOVE.W ..., -(%SP)`)
> - **En lecture :** Dépiler une valeur du sommet (`MOVE.W (%SP)+, ...`)

# Récap des étapes
**Programme appelé**
1. Sauvegarder le contexte → Empiler les registres
2. Réserver l'espace pour les variables → SUBA.L
3. Récupérer la valeur des arguments d(%sp) (Par copie dans la pile ou par référence)
4. Remettre à jour la valeur du paramètre en sorte → %d0
5. Libérer l'espace pour les variables → ADDA.L
6. Restaurer des registres → Depiler
7. RTS

**Programme appelant**
- Empiler les valeurs de paramètres : `MOVE ..., -(%sp)`
- `JSR`
- Traiter la valeur en sortie (`%D0`)
- Remettre la pile dans son état initial : `ADDA.L .., %sp`
# Appel de sous programme
## Fonctionnement
Un sous programme fait office de fonction. Elle nous permet d'appeler un sous-programme qui se traduit par un branchement vers le sous-programme.

## Appel de sous-programme
Pour appeler un sous programme, on utilise l'instruction `JSR`. Fonctionne en deux étapes :
1. Empile l'adresse de retour (`PEA 4(%PC)`)
2. `%PC` = adresse de sous programme
Pour marquer la fin du sous-programme, il faut utiliser l'instruction `RTS` qui va modifier la pile
1. Lecture de l'adresse au sommet de la pile qui est dépilée
2. `%PC` = Adresse lue

## Paramètres en entrée et en sorte
La pile nous permet aussi de passer des paramètres à noter fonction. Ainsi, il faut régulièrement penser à remettre la pile à l'état initiale dût à la mémoire utilisée pour les paramètres en entrée. On va pour cela utiliser l'instruction `ADDA.L(9)`. La valeur de retour est stockée dans le registre `%D0` si la valeur est stockée sur 4 octets. Sinon, la valeur est stocée dans une zone mémoire indiquée par le registre `%A0`

# Sauvegarde du contexte
> [!tip] SAUVEGARDE DE CONTEXTE
> # Règles de programmation
> 1. **Dès les premières instructions** : sauvegarder en pile la valeur des registres modifiés par le sous programme
> 2. **Restaurer la valeur** le contexte = la valeur initiale des registres modifiés

⇒ En fait, à l'intérieur de la fonction, il faut ajouter les valeurs des registres utilisés dans la pile et à la sortie de la fonction, il faut dépiler pour récupérer la valeur du registre
**Exemple :**
```ASSEMBLEUR
FCT_SOMME:
	MOVE.W %D1, -(%SP) | Sauvegarde du contexte
	MOVE.W 6(%SP), %D1
	ADD.L 8(%SP), %D1
	MOVE.W %D1, %D0
	MOVE.W (%SP)+, %D1 | Restauration du contexte
	RTS
| => Pour garde la valeur de %D1
```
# Variables locales
1. Réserver l'espace pour les variables locales en pile = décaler le sommet de pile → `SUBA.L`
2. Access aux variables par adressage indirect d(%sp)
3. Libérer l'espace → décaler le sommet → ADDA.L

# Exemples de fonctions
## Fonction max
```ASSEMBLEUR
MAX :
	MOVE.W D1, -(%SP) | 1
	MOVE.L %A1, -(%SP)

	MOVE.L 10(%SP), %A1
	MOVE.W 14(%SP), %D0

	CMP.W (%A1), %D1
	BGE .else

	MOVE.W 16(%SP), %D1
	ADD.W #2, %D1
	BRA .endif
.else :
	MOVE.W 16(%SP), %D1
	SUB.W #4, %D1
.endif:
	MOVE.W %D1, %D0 | 4

	MOVE.L (%SP)+, %A1 | 5
	MOVE.W (%SP)+, %D0

	RTS | 6



| Appel de la fonction max

MOVE.W #8, -(%SP)
MOVE.W b, -(%SP)
PEA a
JSR MAX
MOVE.W %D0, somme
ADDA.L #
	
```

## Fonction somme
```LOGIQUE
entier.w FCT_SOMME(entier.W x, entier.W y){
	D1.w = x;
	D1.w = D1.w + y;
	return D1.w
}
void Debut(){
	D1.W = 1234;
	somme = FCT_SOMME(5,10);
	somme = somme + D1.W
}
```

```ASSEMBLEUR
FCT_SOMME:
	MOVE.W %D1, -(%SP)
	MOVE.W 6(%SP)
	ADD.W 8(%SP), %D1
	MOVE.W %D1, %D0
	MOVE.W (%SP)+, %D1
	RTS
```

## Fonction somme 2
```LOGIQUE
entier.W FCT_SOMME(entier x, entier y){
	entier.W z = 23;
	z = 2*x+y+z;
	return z;
}
debut(){
	somme = 0;
	FCT_SOMME(a, b);
}
```

```ASSEMBLEUR
FCT_SOMME:
	MOVE.W %D1, -(%SP)
	SUBA.L #2, %SP
	MOVE.W #23, -(%SP)
	MOVE.W 8(%SP), %D1
	ADD.W %D1, %D1
	ADD.W 10(%SP), %D1


MOVE.W #0, somme
MOVE.W b, -(%SP)
MOVE.W a, -(%SP)
JSR FCT_SOMME
```

