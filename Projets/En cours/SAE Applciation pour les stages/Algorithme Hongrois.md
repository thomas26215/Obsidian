



**Groupe 4**

*   VENOUIL Thomas
*   ARNAUD Sophie
*   BILS Brayan
*   JOANNICElouan
*   CELUZNIAK DE SOUZA Maria


<div style="text-align: center; margin-top: 300px; margin-bottom: 20px;">
    <img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4ZMW_BCVViAx7D_ZieOoXxe4LN-gK-smyG02vMs3hakMKz9QUb87FtANE72AyFNDQCiB9lrve3tS27a58cLIygIMt4IzFlID0Mr121F3WEhzBJDkgihUOZ3rSgKhdcI5fHImAlQ?key=bGQht-ukJAu38OyHPutoFyVF" style="width: 100%;" alt="Description de l'image" />
</div>

<div style="page-break-after: always;"></div>

**Table des matières :**
```table-of-contents

```

<div style="page-break-after: always;"></div>

Nous avons implémenté l'algorithme Hongrois en R. Cet algorithme permet de trouver la meilleure affectation possible avec une matrice quelconque
Pour chaque étape, nous avons écrits une ou plusieurs fonctions afin d'effectuer les étapes de l'algorithme Hongrois et pour arriver à un résultat cohérent.

# 1. Rendre la matrice carré si elle ne l'est pas

```R
make_square_matrix <- function(matrix) {
  cat("\n=== Step 1: Matrix Preparation ===\n")
  rows <- nrow(matrix)
  cols <- ncol(matrix)
  
  if (rows == cols) {
    cat("Matrix is already square (", rows, "x", cols, ")\n", sep = "")
    return(matrix)
  }
  
  size <- max(rows, cols)
  new_matrix <- matrix(Inf, nrow = size, ncol = size)
  new_matrix[1:rows, 1:cols] <- matrix
  cat("Converted to square matrix (", size, "x", size, ") with Inf padding\n", sep = "")
  return(new_matrix)
}
```

<div style="page-break-after: always;"></div>

# 2.  Réduire les lignes et les colonnes de leur minimum
## 2.1. Réduire les lignes

```r
subtract_row_mins <- function(matrix) {
  cat("\n=== Step 2: Row Reduction ===\n")
  row_mins <- apply(matrix, 1, min, na.rm = TRUE)
  cat("Row minima:", row_mins, "\n")
  result <- sweep(matrix, 1, row_mins)
  print(result)
  return(result)
}
```

## 2.2. Réduire les colonnes

```r
subtract_col_mins <- function(matrix) {
  cat("\n=== Step 3: Column Reduction ===\n")
  col_mins <- apply(matrix, 2, min, na.rm = TRUE)
  cat("Column minima:", col_mins, "\n")
  result <- sweep(matrix, 2, col_mins)
  print(result)
  return(result)
}
```


<div style="page-break-after: always;"></div>

# 3.  Encadrer et  Barrer les zéros

```R
find_max_matching <- function(matrix) {
  cat("\nFinding maximum matching in zero matrix...\n")
  n <- nrow(matrix)
  adj <- matrix == 0
  pair_u <- rep(NA, n)
  pair_v <- rep(NA, n)
  dist <- rep(0, n)
  
  bfs <- function() {
    queue <<- which(is.na(pair_u))
    dist <<- rep(Inf, n)
    dist[queue] <<- 0
    while (length(queue) > 0) {
      u <- queue[1]
      queue <<- queue[-1]
      for (v in which(adj[u, ])) {
        if (is.na(pair_v[v]) || dist[pair_v[v]] < Inf) {
          if (is.na(pair_v[v])) return(TRUE)
          dist[pair_v[v]] <<- dist[u] + 1
          queue <<- c(queue, pair_v[v])
        }
      }
    }
    FALSE
  }
  
  dfs <- function(u) {
    for (v in which(adj[u, ])) {
      if (is.na(pair_v[v]) || (dist[pair_v[v]] == dist[u] + 1 && dfs(pair_v[v]))) {
        pair_u[u] <<- v
        pair_v[v] <<- u
        return(TRUE)
      }
    }
    dist[u] <<- Inf
    FALSE
  }
  
  while (bfs()) {
    for (u in 1:n) if (is.na(pair_u[u])) dfs(u)
  }
  list(pair_u = pair_u, pair_v = pair_v)
}

find_min_line_cover <- function(matrix) {
  cat("\nFinding minimum line cover...\n")
  n <- nrow(matrix)
  matching <- find_max_matching(matrix)
  
  # Konig's theorem implementation
  mark_u <- rep(FALSE, n)
  mark_v <- rep(FALSE, n)
  mark_u[is.na(matching$pair_u)] <- TRUE
  
  repeat {
    changed <- FALSE
    for (u in which(mark_u)) {
      vs <- which(matrix[u, ] == 0)
      for (v in vs) {
        if (!mark_v[v]) {
          mark_v[v] <- TRUE
          changed <- TRUE
        }
      }
    }
    
    for (v in which(mark_v)) {
      u <- matching$pair_v[v]
      if (!is.na(u) && !mark_u[u]) {
        mark_u[u] <- TRUE
        changed <- TRUE
      }
    }
    if (!changed) break
  }
  
  covered_lines <- list(rows = !mark_u, cols = mark_v)
  cat("Covered rows:", which(covered_lines$rows), "\n")
  cat("Covered columns:", which(covered_lines$cols), "\n")
  return(covered_lines)
}
```

<div style="page-break-after: always;"></div>

# 4. Marquer les lignes et les colonnes et on retranche aux cases non barrés leur minimum et on ajoute cette valeur on cases barrées deux fois

```r
adjust_matrix <- function(matrix, cover) {
  cat("\nAdjusting matrix...\n")
  min_val <- min(matrix[!cover$rows, !cover$cols])
  cat("Minimum uncovered value:", min_val, "\n")
  
  matrix[!cover$rows, ] <- matrix[!cover$rows, ] - min_val
  matrix[, cover$cols] <- matrix[, cover$cols] + min_val
  
  cat("New matrix after adjustment:\n")
  print(matrix)
  return(matrix)
}
```

<div style="page-break-after: always;"></div>

# 5. La fonction principale pour faire tourner l'algorithme

```r
hungarian_algorithm <- function(matrix) {
  original <- matrix
  cat("=== Initial Matrix ===\n")
  print(matrix)
  
  # Step 1: Prepare matrix
  matrix <- make_square_matrix(matrix)
  
  # Step 2-3: Initial reduction
  matrix <- subtract_row_mins(matrix)
  matrix <- subtract_col_mins(matrix)
  
  iteration <- 1
  while (TRUE) {
    cat("\n=== Iteration", iteration, "===\n")
    
    # Step 4: Find line cover
    line_cover <- find_min_line_cover(matrix)
    num_lines <- sum(line_cover$rows) + sum(line_cover$cols)
    cat("Total lines:", num_lines, "/", nrow(matrix), "\n")
    
    if (num_lines == nrow(matrix)) {
      cat("\n*** Optimal solution found! ***\n")
      break
    }
    
    # Step 5: Adjust matrix
    matrix <- adjust_matrix(matrix, line_cover)
    iteration <- iteration + 1
  }
  
  # Final matching
  matching <- find_max_matching(matrix)
  assignment <- matching$pair_u
  total_cost <- sum(original[cbind(1:nrow(original), assignment)])
  
  # Results formatting
  cat("\n=== Final Assignment ===\n")
  result_df <- data.frame(
    Task = 1:nrow(original),
    Agent = assignment,
    Cost = original[cbind(1:nrow(original), assignment)]
  )
  print(result_df)
  
  list(
    assignment = assignment,
    total_cost = total_cost,
    final_matrix = matrix,
    iteration_count = iteration
  )
}
```


<div style="page-break-after: always;"></div>

# Exemple d'utilisation de la fonction

Nous pouvons donc utiliser ce code par exemple pour la matrice :
$$\begin{pmatrix}1&2&3&4&5\\1&4&2&5&3\\3&2&1&5&4\\1&2&3&5&4\\2&1&4&3&5\end{pmatrix}$$

Pour cette matrice, nous utilisons donc le code de cette manière :

```r
cost_matrix <- matrix(c(
  1,2,3,4,5,
  1,4,2,5,3,
  3,2,1,5,4,
  1,2,3,5,4,
  2,1,4,3,5
), nrow = 5, byrow = TRUE)

result <- hungarian_algorithm(cost_matrix)
```



Et voici nos résultats :
$$\begin{pmatrix}0&0&1&0&1\\1&3&1&2&0\\3&1&0&2&1\\0&0&1&1&0\\2&0&3&0&2\end{pmatrix}$$
Ainsi, 1 est affecté à 1, 2 est affecté à 5, 3 est affecté à 3, 4 est affecté à 2 et 5 est affecté à 4