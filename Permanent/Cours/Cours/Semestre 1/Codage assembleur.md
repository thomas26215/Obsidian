---
MOOC: "[[Cours]]"
Ressource: "R1.03 : Architecture des ordinateurs (données et instructions)"
Cours: "Cours 4 : Codage assembleur"
Date: 2023-12-04
tags: 
Complete: false
Learned: false
---
# Généralités d'un ordinateur et de l'assembleur
Dans un ordinateur, la RAM (Random Access Memory) est une composante importante qui stocke différents programmes, ainsi que leurs données et leurs instructions. Quand au processeur, il est doté de plusieurs éléments clés tels que l'UAL (unité arithmétique et logique) et les registres. 

L'UAL est responsable de l'exécution des opérations arithmétiques et logiques, tandis que les registres sont de petites unités de mémoire intégrées dans le processeur. Le processeur passe son temps à exécuter des instructions enregistrées dans la mémoire centrale, puis à récupérer les données nécessaires pour effectuer les calculs.

Il est important de mentionner la mémoire cache qui agit comme tampon entre le processeur et la RAM. La mémoire cache permet au processeur de trouver rapidement les données et les instructions nécessaires à son fonctionnement.

Dans le contexte du processeur 68000, il existe plusieurs types de registres. Tout d'abord, il y a 8 registres de données (D0 à D7) qui ont une capacité de stockage de 32 bits. Ensuite, on trouve 8 autres registres appelés registres d'adresse (A0 à A7). En plus de cela, il existe des registres d'état (S) qui contiennent les indicateurs suivants: Z (Extension de signe), N (Résultat nul), V (débordement) et C (retenue).

Le programme counter (PC) est un registre spécial de 32 bits qui contient l'adresse de la prochaine instruction à exécuter. Il est initialement configuré avec l'adresse de la première instruction du programme et évolue à chaque instant, soit en pointant vers l'instruction suivante en mémoire centrale (en fonction de la longueur du codage actuel), soit en indiquant une adresse de saut lorsqu'un branchement ou un appel de sous-programme est effectué.

**Exemple de codage :**
`SUB.W D3, Var A` ⇒ `Var A(.W) = Var A(.W)-D3.W`
cf page 20.Mot d'instruction + développement des mots d'extension

SUB `-<3>dix

| 1001           | 011             | 101           | 111  | 000        |
| -------------- | --------------- | ------------- | ---- | ---------- |
| Code opération | Numéro registre | Code longueur | Mode | Suite mode | 
En 16 bits

Counter. Compteur ordonal
SUB.W D3, adresse en .W ($0600.W) ⇒ Prochaine adresse à exécuter
`<$9778 0600>`
⇒ 68000 L'adresse de la première instuction du programme (Reset)
⇒ Suivante en MC (et dépend  de la longueur du codage de l'instruction courante)
Soit adresse d'un brachement (et si branchement prix ou si appel dans sous programme)


# Qu'est ce qu'une instruction ?
1. Indication à fournir au processeur ?
  ⇒ Opérations (Ex Move, Add). <mark style="background: #FFB8EBA6;">(Dépend du jeu d'instructions)</mark>
  ⇒ Avec quelles opérandes ? <mark style="background: #FFB8EBA6;">SUB.B D3, var A (source et destination)</mark>
  ⇒ Sur quelle longueur ? <mark style="background: #FFB8EBA6;">B, W, L</mark>
  ⇒ Où ranger les résultats ? <mark style="background: #FFB8EBA6;">SUB.B D3, Var A, D5 Le résultat est stocké dans D5. Pour 68000, résultat dans destination si aucun spécifié</mark>
  ⇒ Quoi faire après ? (Quelle instruction exécuter après) <mark style="background: #FFB8EBA6;">Passer à l'instruction suivante, dans mémoire centrale, ou autre si enbranchement ... Mise à jour de PC</mark> 
2. Catégories d'instructions.
   ⇒ Mouvement de données. MOVE (LOAD, STORE). NZVC = * * 0 0
   ⇒ Opérations arithmétiques. ADD, SUB. NZVC = * * * *
   ⇒ Logiques. UAL, OR, AND, XOR. NZVC = * * 0 0
   ⇒ Branchements conditionnels (et appels de sous programmes). B(cond)
   BCS ou BCC adresse_où_aller → branchement si carry (Ne modifie pas les indicateurs NZVC) 
   Sous programme → JSR nom_sous_programme
   Autres NOP no_operation
	        SWAP.L .W et .W ou .B et .B
3. Les modes de dressage
   ⇒ MOVE.W D7, Var A Immédiat : # D4F3 / %0110.. / -24
   ⇒ MOVE.W # 28, D5 Register D0...D7
   ⇒ MOVE.W 28, D5 Absolu (Direct mémoire) (MC) accès (RAM) .N .L → cf TD

Codage / décodage instructions
`<$9B38 0502 1C3C 3C7B 6B02...>68000` ⇒ PC

1er octet ⇒ `<9B38>` = `%1001 1011       0011   1000`. Mot d'instruction
										SUB  Num registre  Mode  Suite Mode
Photo
La fin ca fait 111 000 ce qui correspond a absolu.W

SUB.B D5, Abs.W   MC[$...].B ← MC[$...] B - D5.B
Pour le ABS.W, elle se trouve juste après
donc SUB.B D5, $0502

PC ← PC+2octets+2

`$1C3C` ⇒ MOVE.B # $7B, D6


**Branchement :**
Tant que A >= 0      → Détecter ruptures de séquence
          ou B = 0
Faire .
        .
        .
        .
Fin tant que


tant que MOVE.N A, D0
										, aller à faire
	BPL faire					pour N = 0
ou MOVE.W B, D0        , aller à fin tant que
	BNE  fin tant que    pour Z=0

Faire .
		 .
		 .
		 .
		 BRA tq
Fin tant que

# Coder en assembleur 68000
## Codage et décodage d'une instruction
![[Pasted image 20231214162842.png|475]]
A partir de la feuille ci-dessus, décoder l'instruction suivante :
`<D644 123C 00FF 9404 9438>proc.68000`
Pour pouvoir décoder cela, il faut savoir que l'assembleur octet par octet.
Certaines indications :
- Valeur absolue : les x prochains octets représentent la valeur du nombre, et ce n'est non plus une instruction

1. `$D644` = `%1101 0110 0100 0100`
   D'une manière plus visuelle pour le décodage, on a `%1101 011 001 000 100`
   Les quatre premiers bits nous indiquent que c'est une instruction `ADD`. Il faut donc regarder le deuxième tableau.
   On a donc `1101` = MOVE. `001` nous indique que c'est un `.W` et cela se représente comme cela : `<AE>, Dn`
   On a donc finalement
	   `1101` = Move
	   `011` = Registre D3
	   `001` = `.W` en nous indiquant que c'est `<AE>, Dn`
	   `000 100` = Registre D4
	 ⇒ Donc l'instruction est `MOVE.W D4, D3`
Faire de même pour les autres

## Passer d'un algorithme au code assembleur
### Sans CMP
Si [(A>=0)

	ou (B<0)]
et (C=0)
alors
... + Instruction direction <mark style="background: #FF5582A6;">Finsi</mark>
Sinon
...
<mark style="background: #FF5582A6;">Finsi</mark>


Pour une condition, on n'enfait jamais une pour aller à l'instruction suivante, car c'est ce que fait le processeur à la base. On utilise pour aller vers une auture instruction, où le processeur ne serait pas allé par lui-même

```Assembly
A, B, C : .W en cpt2
S1 MOVE.B A,D0 Mise à jour de N,Z
	BLP et(3)  Aller à et(3) pour N=0

ou(2) MOVE.N B,D0 Mise à jour N,Z
	BLP sinon Aller à sinon pour N=0

et(3) MOVE.W C,D0 maj N,Z
		BNE sinon Aller à sinon pour Z=0

alors
	BRA finsi

sinon
	finsi
```


### CMP et CMPI
CMP(ou CMPI), j'indique sur quelle longueur je travaille (B, W, L). Source, destination
→ Entraîne le positionnement des indicateurs (N, Z, V, C) en fontion de destination - source
Mais le résultat n'est pas stocké

Destination ? Source

|     | Base 2 | Cpt2 |
| --- | ------ | ---- |
| >=  | BCC    | BGE  |
| <   | BCS    | BLT  |
| >   | BKI    | BGT  |
| <=  | BLS    | BLC  |
MC[$] (Absolu)
CMPI B/W/L # ...,  Var A (ou Dj)


---
**Questions :**
1. Qu'est ce que la RAM ? Qu'y a til dedans ?
2. De quoi est doté le processeur ?
3. Qu'est-ce que l'UAL ?
4. Que sont les registres ?
5. Que fait le processeur ?
6. Qu'est ce que la mémoire cache ?
7. Qu'y a t-il dans le contexte du 68000 ?
8. Qu'est ce qu'une instruction ? Donner les différentes parties. Pour chaque partie, les différentes étapes


###
```assembly
S1 MOVE.W a, D0
	CMP.W C, D0 ; D0(=a) ? c
	BGE où(3) pour a >= c
et(2) MOVE.W d, D0
	CMP.W ,b D0 ; D0(=d) ? b
	BLT alors(4) ; aller à alors(4) pour d < b
ou(3) MOVE.W b, d6
	CMP.W c, D0 ; D0(=b) ? c
	BGE sinon(5) ; aller à sinon(5) pour b >= c
```

### Codage des Bxx
Bxx (xx = condition) étiquette (où aller)
Mot d'instruction `%0110 condition 8bits`
⇒ 16 conditions (BGE, BRA ...)