# Expressions Régulières et Automates à États Finis

## 1. Expressions Régulières (Regex)

Les expressions régulières sont des motifs de recherche puissants utilisés pour décrire et manipuler des chaînes de caractères.

## 1.1 Syntaxe de Base

- **Caractères littéraux** : Correspondent à eux-mêmes. Ex : "abc" correspond à "abc".
    
- **Métacaractères** : Ont une signification spéciale.
    - `.` : N'importe quel caractère sauf nouvelle ligne
    - `*` : 0 ou plusieurs occurrences
        
    - `+` : 1 ou plusieurs occurrences
        
    - `?` : 0 ou 1 occurrence
        
    - `^` : Début de ligne
        
    - `$` : Fin de ligne
        
    - `[]` : Classe de caractères
        
    - `()` : Groupement
        
    - `|` : Alternative

### Classes de caractères
- `a+b+c+d` <=> `a|b|c|d` <=> `[abcd]` <=> `[a-d]`
- `0+1+2+3+4+5+6+7+8+9` <=> `1|2|3|4|5|6|7|8|9` <=>  `[123456789]` <=> `[1-9]`
- `[:alpha:]` = caractères alphanumériques
- `[:digit:]` = classe des chiffres aussi notée `\d`
- `[:alnum:]` = union de la classe `[:alpha:]` avec la classe `[:digit:]`
- `[:word:]` = classe `[:alnum:]` plus le souligné `_`. Autrement noté `\w`
- `[1-9A-F]` = Un nombre de 0 à 9 ou une lettre de A à F

## 1.2 Exemples

## 1.2.1 Adresse e-mail

text

`\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b`

Cette regex correspond à la plupart des adresses e-mail.

## 1.2.2 Numéro de téléphone français

text

`^(?:(?:\+|00)33|0)\s*[1-9](?:[\s.-]*\d{2}){4}$`

Correspond aux formats comme +33 1 23 45 67 89 ou 01.23.45.67.89.

## 1.2.3 Date (format JJ/MM/AAAA)

text

`^(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[012])/(19|20)\d\d$`

Valide les dates comme 01/01/2025.

## 1.3 Utilisation en PHP

PHP offre plusieurs fonctions pour travailler avec les regex:

php

`$texte = "Mon email est exemple@email.com"; $pattern = "/\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b/"; if (preg_match($pattern, $texte, $matches)) {     echo "Email trouvé : " . $matches[0]; }`

## 2. Automates à États Finis

Un automate à états finis est un modèle mathématique utilisé pour représenter des systèmes avec un nombre fini d'états.

## 2.1 Composants Principaux

1. **États** : Représentés par des cercles ou rectangles arrondis.
    
2. **Transitions** : Flèches reliant les états.
    
3. **État initial** : Marqué par une flèche entrante.
    
4. **États finaux** : Représentés par un double cercle.
    

## 2.2 Exemple : Distributeur Automatique

text

     `Pièces insérées    ┌───────────────┐    │               │    ▼               │ [En attente] ──────▶ [Encaissement]     │                    │    │ Article            │ Montant suffisant    │ sélectionné        │    ▼                    ▼ [Test d'article] ──────▶ [Distribution]`

Dans cet exemple:

- L'état initial est "En attente".
    
- L'insertion de pièces fait passer à l'état "Encaissement".
    
- La sélection d'un article mène à "Test d'article".
    
- Si le montant est suffisant, on passe à "Distribution".
    

## 2.3 Implémentation en PHP

php

`class DistributeurAutomatique {     private $etat = 'En attente';    private $montant = 0;     public function insererPieces($somme) {        $this->montant += $somme;        $this->etat = 'Encaissement';    }     public function selectionnerArticle($prix) {        if ($this->etat == 'Encaissement') {            $this->etat = 'Test d\'article';            if ($this->montant >= $prix) {                $this->etat = 'Distribution';                echo "Article distribué";            } else {                echo "Montant insuffisant";            }        }    } }`


## 3. Les sous masques



Un sous-masque est une partie d'une expression régulière entourée de parenthèses (). Ces parenthèses créent des groupes de capture, permettant d'extraire des parties spécifiques du texte correspondant au motif global.

### Exemple avec une date

Prenons l'expression régulière pour une date au format jj/mm/20aa :

php

`/(\b(0[1-9]|[12][0-9]|3[01])\/(0?[1-9]|1[0-2])\/20(\d{2})\b)/`

Dans cette expression, nous avons plusieurs sous-masques :

1. Le premier groupe (tout le motif) capture la date entière.
    
2. `(0[1-9]|[0-9]|3)` capture le jour.
    
3. `(0?[1-9]|1[0-2])` capture le mois.
    
4. `(\d{2})` capture les deux derniers chiffres de l'année.
    

### Comment utiliser les sous-masques en PHP

En PHP, lorsque vous utilisez `preg_match()`, les sous-masques sont stockés dans le tableau `$matches` :

```php
$text = "La date est 15/03/2024";
$pattern = '/(\b(0[1-9]|[12][0-9]|3[01])\/(0?[1-9]|1[0-2])\/20(\d{2})\b)/';
if (preg_match($pattern, $text, $matches)) {     
	print_r($matches); 
}
```

Le résultat serait :



```php
Array (
	[0] => 15/03/2024 // Match complet   
	[1] => 15/03/2024  // Premier groupe (toute la date)   
	[2] => 15          // Deuxième groupe (jour)    *
	[3] => 03          // Troisième groupe (mois)    
	[4] => 24          // Quatrième groupe (année)
)
```

### Exemple pratique

Voici comment vous pourriez utiliser ces sous-masques pour extraire les composants d'une date :

```php
function dateFromString(string $text): array {     
	$pattern = '/\b(0[1-9]|[12][0-9]|3[01])\/(0?[1-9]|1[0-2])\/20(\d{2})\b/';
	if (preg_match($pattern, $text, $matches)) {        
		return [            
			'jour' => $matches[1],            
			'mois' => $matches[2],            
			'annee' => '20' . $matches[3]        
		];    
	}    
	return []; 
} 

$str = "Nous sommes le 15/3/2024";
$date = dateFromString($str); 
if (!empty($date)) {     
	echo "Jour: {$date['jour']},
	Mois: {$date['mois']}, Année: 
	{$date['annee']}";
}
```

Cette fonction extrait le jour, le mois et l'année séparément, grâce aux sous-masques de l'expression régulière.

Les sous-masques sont donc un outil puissant pour extraire des informations structurées à partir de textes correspondant à des motifs spécifiques.

---

## Conclusion

Les expressions régulières et les automates à états finis sont des outils puissants pour la manipulation de texte et la modélisation de systèmes. Leur maîtrise est essentielle pour de nombreuses tâches en programmation, du traitement de données à la conception de systèmes complexes.

---

Réponse de Perplexity: pplx.ai/share