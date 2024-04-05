During the week, we realized a project in order to classificate automatically a lot of dispaches (A dispach is a journalistic information ; For instance : Reign of the Queen, the Queen is dead, Queen Elizabeth II died on September 8, 2022, at the age of 96 and was succeeded by her eldest son under the name Charles III.). Then, we have make a program where the goal is to assign the dispaches in one of the following categories :
- ENVIRONNEMENT-SCIENCES
- CULTURE
- ECONOMY
- POLITIQUE
- SPORTS
To do that, we worked in stages :
→ First, we made lexiques, who are programs who save in memorie a lot of words for a particular categorie. Moreover, all these words has a weight attached, who goes from 1 to 3. For instance, in the SPORT category, we can have following words and weights : ***sport : 3, cup : 3, player : 2, domicile : 1***. 
→ Then, we had to create a program which compute the score of each dispach : For each article, the program calculates a score for each of the five categories by adding the weights of the words in the category's lexicon. The category assigned to the article is the one with the highest score. In case of a tie, a category is chosen arbitrarily among the best. In summary, the program classifies articles based on the category whose lexicon best matches the words used in the article
→ We have in disposition 2 files : `depeches.txt` who give us a lot of dispaches and `text.txt` to test our program.
→ Finally, we must generate a response file which will contain the number of the dispatches, their associated category as well as the percentage of correct

# 1 - The differents classes
## a) Categorie
The class `Categorie` have 2 attributes : `nom` which contains a name of a categorie and `lexique` who which contains words and wigth attached to this categorie.

## b) Classification
This class contains the main functions of our program and the function `main`. It will contains functions for the lexique, for the score and for the normal running of the program

## Depeche
This function will be useful for us to differentiate between the different parts of a dispatch. There will be several attributes: id, date, category, content and words. We will have a function in this class which will allow us to automatically retrieve each of the different elements of a dispatch from the depeches.txt file and will assign them to the different attributes, so respectively id, date, category, content and all the words that go be contained in the ArrayList word

## PaireChaineEntier
The class `PaireChaineEntier` is used to stock to store a chain and a linked digit. We'll mainly use this function when we'll want to stock somewhere ***A compléter***


# Functions we have created
All functions have been commented in the code. For the second part, if you want more informations, you can look directly in the code
## FirstPart
### initLexique
This function is found in the class `Category`. We recall that this function that this class has the attributs `name` and `lexique`. This function aims to read a file in this form :

```Categorie1.txt
word1:weigth1
word2:weigth2
word3:weigth3
word4:weigth4
...
```
Each element of the ArrayList `lexique` must be a word-weight pair. To achieve this, we must call the class `PaireChaineEntier`, which will be the elements of this ArrayList, elements which will represent the word-weight pairs. The variable `chaine` will store the word and the variable `entier` will store the weight.

### Score      
This method will return us the score of a dispatch. The score of a dispatch is calculated by the score of each word, a score that can be retrieved using the attribute `lexique` initialized by the function `initLexique` 
To do this, it takes a dispatch from the class `Depeche`  as parameters. We will therefore have access to the information in the dispatch, previously stored in the corresponding variables thanks to the function `lectureDepeche`  of the class `Classification` . To do this, we proceeded in stages:
1. **Browse through the list of words in the dispatch**. We will therefore go through all the words present in the ArrayList `Words` of the object `d` which is the dispatch given in parameters. This ArrayList contains all the words of the dispatch
   ⇒ `for (int i = 0; i < d.getMots().size(); i++) {`
2. **Adding the score** We will add the current score with the score of the current word. To retrieve the score of the word, you must retrieve the score of the current word, function `integerForString`, specifying as parameters the lexicon (attribute `lexique`) as well as the current word
   ⇒ `score += UtilityPairStringInteger.integerForString(lexicon, d.getWord().get(i))`
   3. **Return the score**
      ⇒ `return score`
### chaineMax
The function `chaineMax` present in the class `UtilitairePaireChaineEntier`  retrieves the string associated with the pair having the largest integer among all the pairs in the list `listePaireEntiers` . Each element in this  is a pair composed of a string and an integer, represented by the attributes of the class ``PaireChaineEntier`` .

### indicePourChaine
This function takes as parameters an ArrayList `ListePaires` and a character string `chaine`. For each element of `listPaires` which are elements of the class `PaireIntegerString`, we will compare the name (`listPaires.get(j).getString()`) with `chaine` (. If it is the same, we return the index. Otherwise we return 0



### Moyenne
This function will allow us to average the integers stored in the ArrayList `ListePaires` passed as parameters.



### ClassementDepeches
This function will return a file in this format:
```Resultat.txt
001:ENVIRONNEMENT-SCIENCE
002:ENVIRONNEMENT-SCIENCE
003:ECONOMIE ...
500:SPORTS 
NVIRONNEMENT-SCIENCES:
89% CULTURE:
93% ECONOMIE:
68% POLITIQUE:
80% SPORTS: 76%
MOYENNE : 81.2%
```
Something that was successfully achieved, in accordance with our code

## Second part
For the second part, we did the same thing but we had to initialise automatically the lexics. We had to rewrite some functions and to create new to meet expectations.
All the functions were created and work with success

# Results
In terms of results, we can observe many things:
1. In terms of execution time
	1. We can observe execution times with or without sorting. For the manual version, we observe that without sorting, the execution time is 162 ms and is 308 ms with the sorted version. Also, we observe that for the training version, we have an execution time of 500 ms for the unsorted version unlike an execution time of 770 ms for the sorted version
	⇒ **The sorted version is therefore more efficient**
	2. We can also observe the execution time between the training version and the one without. Without learning, we have respectively 162ms and 308ms for the sorted and unsorted version compared to execution times of 500ms and 770ms for the training version
	⇒ **The learning version takes longer, which seems undeniable**
2. For the learning version, we obtain 52% success, unlike a result of 67% for the learning version, which leads us to believe that this version is more precise than when we do it by hand
3. By adding depth to the learning algorithm, we observe a better success rate. If we call the algorithm 5 times so that it learns more, we go from a success rate of 67% to 76% success




# Complexity
**Function calculScore :**
⇒ no sorted and no automatic
- CUTURE : 11324 comparaisons
- ECONOMIE : 13376
- ENVIRONNEMENT-SCIENCE : 13190 comparaisons
- POLITIQUE : 13490 comparaisons
- SPORTS : 12348 comparaisons

no sorted v2 and automatic
- CULTURE : 5647
- ECONOMIE : 6674
- ENVIRONNEMENT-SCIENCE : 6580
- POLITIQUE : 6745
- SPORT : 6158

sorted v2 and automatic
- ECONOMIE : 12401
- POLITIQUE : 12441
- CULTURE : 11255
- ENVIRONNEMENT-SCIENCE : 12212
- SPORT : 11854

# Conclusion about ameliorations
One of many solutions can be to add a deeper training for the IA. It can help to improve the precision of the results. One of solutions for the rapidity is to delete the `PaireChaineEntier` class and implement a Map-Array structure.