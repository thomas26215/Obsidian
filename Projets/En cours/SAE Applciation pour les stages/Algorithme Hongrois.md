```R
hungarian_algorithm <- function(cost_matrix) {
  n <- nrow(cost_matrix)
  m <- ncol(cost_matrix)
  
  # Étape 1: Réduction des lignes
  for (i in 1:n) {
    cost_matrix[i,] <- cost_matrix[i,] - min(cost_matrix[i,])
  }
  
  # Étape 2: Réduction des colonnes
  for (j in 1:m) {
    cost_matrix[,j] <- cost_matrix[,j] - min(cost_matrix[,j])
  }
  
  # Étapes 3-5: Recherche de l'affectation optimale
  # (Cette partie nécessite une implémentation plus complexe)
  
  return(cost_matrix)
}

# Exemple d'utilisation
cost_matrix <- matrix(c(2,3,3,4,1,5,3,3,2), nrow=3, ncol=3)
result <- hungarian_algorithm(cost_matrix)
print(result)
	
```

```R

isCarre <- function

cost_matrix <- matrix(c(2,3,3,4,1,5,3,3,2,1,2,4), nrow=4, ncol=4)
matrice <- matrix(1:12, nrow=3, ncol=4)


# Ajouter une colonne
nouvelle_colonne <- c(6, 7, 8)
cost_matrix_elargie <- cbind(cost_matrix, nouvelle_colonne)

# Ajouter une ligne
nouvelle_ligne <- c(9, 10, 11)
cost_matrix_elargie <- rbind(cost_matrix, nouvelle_ligne)
```

# Fonction minimum

**Fonction minimum pour les lignes :**
```R
# Fonction pour soustraire le minimum de chaque élément d'une ligne
soustraire_minimum <- function(ligne) {
  min_ligne <- min(ligne)
  return(ligne - min_ligne)
}

# Création d'une matrice exemple
matrice <- matrix(c(5,2,3,8,1,6,4,7,9), nrow=3, byrow=TRUE)

# Affichage de la matrice originale
print("Matrice originale:")
print(matrice)

# Application de la fonction à chaque ligne de la matrice
matrice_modifiee <- t(apply(matrice, 1, soustraire_minimum))

# Affichage de la matrice modifiée
print("Matrice après soustraction du minimum de chaque ligne:")
print(matrice_modifiee)

```

**Fonction minimum pour les colonnes :**
```R
# Fonction pour soustraire le minimum de chaque élément d'une colonne
soustraire_minimum_colonne <- function(colonne) {
  min_colonne <- min(colonne)
  return(colonne - min_colonne)
}

# Création d'une matrice exemple
matrice <- matrix(c(5,2,3,8,1,6,4,7,9), nrow=3, byrow=TRUE)

# Affichage de la matrice originale
print("Matrice originale:")
print(matrice)

# Application de la fonction à chaque colonne de la matrice
matrice_modifiee_colonnes <- apply(matrice, 2, soustraire_minimum_colonne)

# Affichage de la matrice modifiée
print("Matrice après soustraction du minimum de chaque colonne:")
print(matrice_modifiee_colonnes)

```

**Fonction pour les 2** :
```R
# Fonction pour soustraire le minimum de chaque élément d'une ligne
soustraire_minimum_ligne <- function(ligne) {
  min_ligne <- min(ligne)
  return(ligne - min_ligne)
}

# Fonction pour soustraire le minimum de chaque élément d'une colonne
soustraire_minimum_colonne <- function(colonne) {
  min_colonne <- min(colonne)
  return(colonne - min_colonne)
}

# Création d'une matrice exemple
matrice <- matrix(c(5,2,3,8,1,6,4,7,9), nrow=3, byrow=TRUE)

# Affichage de la matrice originale
print("Matrice originale:")
print(matrice)

# Application de la fonction à chaque ligne de la matrice
matrice_modifiee <- t(apply(matrice, 1, soustraire_minimum_ligne))

# Affichage de la matrice modifiée pour les lignes
print("Matrice après soustraction du minimum de chaque ligne:")
print(matrice_modifiee)

# Application de la fonction à chaque colonne de la matrice
matrice_modifiee <- apply(matrice_modifiee, 2, soustraire_minimum_colonne)

# Affichage de la matrice modifiée pour les colonnes
print("Matrice après soustraction du minimum de chaque colonne:")
print(matrice_modifiee)

```

# Run

```R

# Fonction pour vérifier si une matrice est carrée
isSquare <- function(matrice) {
  return(nrow(matrice) == ncol(matrice))
}

# Fonction pour rendre une matrice carrée
makeSquare <- function(matrice) {
  n <- max(nrow(matrice), ncol(matrice))
  new_matrice <- matrix(Inf, nrow = n, ncol = n)
  new_matrice[1:nrow(matrice), 1:ncol(matrice)] <- matrice
  return(new_matrice)
}

# Fonction pour soustraire le minimum de chaque élément d'une ligne
soustraire_minimum_ligne <- function(ligne) {
  min_ligne <- min(ligne)
  return(ligne - min_ligne)
}

# Fonction pour soustraire le minimum de chaque élément d'une colonne
soustraire_minimum_colonne <- function(colonne) {
  min_colonne <- min(colonne)
  return(colonne - min_colonne)
}

# Fonction pour soustraire le minimum des lignes et des colonnes
soustraireMinLignesColonnes <- function(matrice) {
  # Application de la fonction à chaque ligne de la matrice
  matrice <- t(apply(matrice, 1, soustraire_minimum_ligne))
  
  # Application de la fonction à chaque colonne de la matrice
  matrice <- apply(matrice, 2, soustraire_minimum_colonne)
  
  return(matrice)
}

# Fonction pour créer la matrice des zéros encadrés et barrés
toSurroundCross <- function(matrice) {
  matriceSurroundCross <- matrix(0, nrow = nrow(matrice), ncol = ncol(matrice))
  for (i in 1:nrow(matrice)) {
    for (j in 1:ncol(matrice)) {
      if (matrice[i, j] == 0) {
        matriceSurroundCross[i, j] <- sample(c(1, -1), 1)
      }
    }
  }
  return(matriceSurroundCross)
}

# Fonction pour vérifier si l'algorithme est terminé
isFinish <- function(matriceSurroundCross) {
  return(all(rowSums(matriceSurroundCross == 1) == 1) && all(colSums(matriceSurroundCross == 1) == 1))
}

# Fonction pour trouver la ligne avec le minimum de zéros
checkLigneMinZero <- function(matrice) {
  zeros_per_row <- apply(matrice, 1, function(x) sum(x == 0))
  if (all(zeros_per_row == 0)) return(NULL)
  return(which.min(ifelse(zeros_per_row > 0, zeros_per_row, Inf)))
}

# Fonction pour marquer
mark <- function(matriceMarkt, ligne_min_zero) {
  if (!is.null(ligne_min_zero)) {
    matriceMarkt[ligne_min_zero, ] <- 1
  }
  return(matriceMarkt)
}

# Fonction pour barrer lignes et colonnes
crossRowColumn <- function(matriceCross, matriceMarkt) {
  for (i in 1:nrow(matriceMarkt)) {
    if (sum(matriceMarkt[i, ]) > 0) {
      matriceCross[i, ] <- 1
    }
  }
  for (j in 1:ncol(matriceMarkt)) {
    if (sum(matriceMarkt[, j]) > 0) {
      matriceCross[, j] <- 1
    }
  }
  return(matriceCross)
}

# Fonction pour obtenir les éléments non barrés
getNotCross <- function(matriceCross) {
  return(which(matriceCross == 0, arr.ind = TRUE))
}

# Fonction pour soustraire et ajouter à la matrice
substractAddMatrice <- function(matrice, matriceCross, min_value) {
  matrice[matriceCross == 0] <- matrice[matriceCross == 0] - min_value
  matrice[matriceCross == 1] <- matrice[matriceCross == 1] + min_value
  return(matrice)
}

# Fonction pour réinitialiser une matrice
reinitialiserMatrice <- function(matrice) {
  return(matrix(0, nrow = nrow(matrice), ncol = ncol(matrice)))
}

# Création de la matrice
matrice <- matrix(c(8,2,4,7,2,1,5,2,6), nrow=3, byrow=TRUE)

print("Matrice originale:")
print(matrice)

# Vérifier si la matrice est carrée et la rendre carrée si nécessaire
if (!isSquare(matrice)) {
  matrice <- makeSquare(matrice)
}

# Soustraction du minimum de chaque ligne et colonne
matrice <- soustraireMinLignesColonnes(matrice)

print("Après soustraction du minimum des lignes et colonnes:")
print(matrice)

# Initialisation des matrices auxiliaires
matriceSurroundCross <- matrix(0, nrow=nrow(matrice), ncol=ncol(matrice))
matriceMarkt <- matrix(0, nrow=nrow(matrice), ncol=ncol(matrice))
matriceCross <- matrix(0, nrow=nrow(matrice), ncol=ncol(matrice))

# Boucle principale de l'algorithme
finished <- FALSE
max_iterations <- 1000
iteration <- 0

while (!finished && iteration < max_iterations) {
  matriceSurroundCross <- toSurroundCross(matrice)
  finished <- isFinish(matriceSurroundCross)
  
  if (!finished) {
    ligne_min_zero <- checkLigneMinZero(matrice)
    matriceMarkt <- mark(matriceMarkt, ligne_min_zero)
    matriceCross <- crossRowColumn(matriceCross, matriceMarkt)
    not_crossed <- getNotCross(matriceCross)
    
    if (length(not_crossed) > 0) {
      min_value <- min(matrice[not_crossed])
      matrice <- substractAddMatrice(matrice, matriceCross, min_value)
    }
    
    # Réinitialisation des matrices auxiliaires
    matriceMarkt <- reinitialiserMatrice(matriceMarkt)
    matriceCross <- reinitialiserMatrice(matriceCross)
  }
  
  iteration <- iteration + 1
}

if (iteration == max_iterations) {
  print("L'algorithme n'a pas convergé après le nombre maximum d'itérations.")
} else {
  print("Matrice finale:")
  print(matrice)
  print("Matrice des zéros entourés et barrés: (Si encadré : 1, Si barré -1n sinon 0)")
  print(matriceSurroundCross)
}



```