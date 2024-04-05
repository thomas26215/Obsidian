---
MOOC: "[[Cours]]"
Ressource: "R1.05 : Introduction aux bases de données et SQL"
Cours: TD 3
Date: 2023-10-16
tags:
---
# Exercice 2
## Q1
![[Pasted image 20231016164036.png]]
## Q2
![[Pasted image 20231016165912.png]]

## Q3
### R0
`CLIENT(numClient, nomClient, prenom, mobile, mail)`
`PRODUIT(codeProduit, description, prix)`
`COMMANDE(IdCommande, Date)`

### R1
`CLIENT(numClient, nomClient, prenom, mobile, mail)`
`PRODUIT(codeProduit, description, prix)`
`COMMANDE(IdCommande, Date, # numClient)`

### R2 (0, n)
On rajoute `DETAILCOMMANDE(# IdCommande, # CodeProduit, quantité)`

## Q5
```SQL
SELECT count(*) AS nombre_commande
FROM COMMANDE
WHERE Date='17/10/2022'
```

```SQL
SELECT numClient, sum(prix*quantité) AS prix_total
FROM PRODUIT p, COMMANDE c, DETAILCOMMANDE d
WHERE D.IdCommande = C.IdCommande AND D.CodeProduit = P.CodeProduit AND Date = '17/10/2022';
GROUP BY numClient
```

```SQL

```