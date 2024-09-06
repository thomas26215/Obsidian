---
MOOC: "[[Cours]]"
Ressource: "R3.16 : C"
Cours: Cours 2
Date: 
tags: 
Complete: false
Learned: false
---
2 types de gestion de la mémoire :
- statique
- dynamique
cf [[Pile]] assembleur

# Notion d'adresses
[[Les pointeurs - C]]

```C
void fonction(int* x){
	*x = *x + *x
}
```

`int* x` = Un pointeur vers int
Dans le passage de fonction, c'est une lecture, dans la fonction, c'est une écriture

# Allocation dynamique
- Mémoire * la demande
- Quantité variable d'exec ou d'exe

Allocation dynamique sont dans le tas

<mark style="background: #FF5582A6;">Demander de la mémoire :</mark> `void *malloc(size_t size);`
Nombres d'octets demandés et pointeur vers inconnu

<mark style="background: #FF5582A6;">Rendre la mémoire :</mark> : `void free(void* pt);`

>[!Warning] `Free`
>- Que une fois par pointeur
>- 1 pointeur donné par malloc


```C
int main(void){
	int *ptr;
	ptr = (int*) malloc(16);
	free ptr(ptr);
}
```