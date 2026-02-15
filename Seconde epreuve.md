# Correction du Sujet CAPES NSI - Seconde épreuve d'admissibilité

## Exercice I : Reconnaissance d'unités lexicales

### 1.1 Automates et base de données

**Question 1** - Automate pour les identificateurs Python

```
États : {entree, valide, invalide}
Alphabet : {lettres (a-z, A-Z), chiffres (0-9), underscore (_)}
Transitions :
- entree --[lettre ou _]--> valide
- valide --[lettre, chiffre ou _]--> valide
- entree --[chiffre]--> invalide
État initial : entree
États finaux : {valide}
```

**Question 2** - Instructions SQL pour la base de données

```sql
-- Insérer if et else comme mots-clefs
INSERT INTO mot (nom_mot, ismotclef) VALUES ('if', 1);
INSERT INTO mot (nom_mot, ismotclef) VALUES ('else', 1);

-- Associer les états de l'automate pour "identificateur de variable"
-- (Les requêtes exactes dépendraient de l'id_mot généré automatiquement)
```

**Question 3** - Réponses sur la structure de la base

1. **Peut-on représenter un automate sans transition ?** Oui, il suffit de ne pas avoir d'entrées dans la table `transition` pour un automate donné.
    
2. **Peut-on décrire plusieurs états avec le même nom dans des automates associés à des mots différents ?** Oui, car `id_etat` est la clé primaire unique, et `nom_etat` peut être identique pour différents automates.
    
3. **Peut-on représenter des états qui seraient à la fois des états d'entrée et de sortie ?** Oui, un état peut avoir `isentree = 1` et `issortie = 1` simultanément.
    
4. **Peut-on décrire deux états de même nom dans le même automate ?** Non, à cause de la contrainte `UNIQUE(nom_etat, id_mot)` dans la table `etat`.
    
5. **Peut-on représenter des automates indéterministes ?** Oui, il suffit d'avoir plusieurs transitions partant du même état avec la même étiquette.
    
6. **Peut-on représenter des automates avec plusieurs états de départ ?** Non, car `isentree` est un entier dans `{0,1}` avec la contrainte `CHECK (isentree in (0,1))`, donc un seul état d'entrée par automate.
    

**Question 4** - Validité des dépendances fonctionnelles

1. `id_etat → nom_mot, ismotclef` : **FAUX** (un état appartient à un automate, mais plusieurs automates peuvent exister)
2. `id_depart, id_arrivee → etiquette` : **FAUX** (plusieurs transitions peuvent relier les mêmes états avec différentes étiquettes)
3. `id_depart → etiquette` : **FAUX** (un état de départ peut avoir plusieurs transitions sortantes)
4. `id_depart, etiquette → id_arrivee` : **FAUX** (dans un automate non déterministe)
5. `nom_etat → isentree` : **FAUX** (le même nom d'état peut être utilisé différemment dans différents automates)

**Question 5** - Requêtes SQL

1. **Nombre de mots décrits dans la base** :

```sql
SELECT COUNT(*) FROM mot;
```

2. **Nombre de mots-clef de la base** :

```sql
SELECT COUNT(*) FROM mot WHERE ismotclef = 1;
```

3. **Nombre d'états dans l'automate du mot "entier"** :

```sql
SELECT COUNT(*) 
FROM etat 
WHERE id_mot = (SELECT id_mot FROM mot WHERE nom_mot = 'entier');
```

4. **Nombre d'états dans l'automate de chaque mot de la base** :

```sql
SELECT nom_mot, COUNT(id_etat) as nb_etats
FROM mot 
LEFT JOIN etat ON mot.id_mot = etat.id_mot
GROUP BY nom_mot;
```

5. **Nombre d'états dans l'automate de chaque mot ayant au moins 5 lettres** :

```sql
SELECT nom_mot, COUNT(id_etat) as nb_etats
FROM mot 
LEFT JOIN etat ON mot.id_mot = etat.id_mot
WHERE LENGTH(nom_mot) >= 5
GROUP BY nom_mot;
```

6. **Nombre d'états des automates qui ont autant d'états que le nombre de lettres du mot correspondant** :

```sql
SELECT nom_mot, COUNT(id_etat) as nb_etats
FROM mot 
LEFT JOIN etat ON mot.id_mot = etat.id_mot
GROUP BY nom_mot
HAVING COUNT(id_etat) = LENGTH(nom_mot);
```

**Question 6** - Incohérence dans le schéma

Le schéma ne garantit pas la cohérence entre les automates et les transitions : une transition pourrait référencer des états appartenant à des automates différents.

**Solution** : Ajouter une colonne `id_mot` dans la table `transition` et une contrainte vérifiant que `id_depart` et `id_arrivee` appartiennent bien au même automate (même `id_mot`). Utiliser des triggers ou des contraintes de clé étrangère composées.

---

### 1.2 Programmation en Python

**Question 7** - Requêtes SQL pour les méthodes de la classe DAO

```python
class DAO:
    def get_mots(self):
        return "SELECT nom_mot FROM mot"
    
    def get_motsclef(self):
        return "SELECT nom_mot FROM mot WHERE ismotclef = 1"
    
    def get_etats(self, mot):
        return """SELECT nom_etat 
                  FROM etat 
                  WHERE id_mot = (SELECT id_mot FROM mot WHERE nom_mot = ?)"""
    
    def get_entree(self, mot):
        return """SELECT nom_etat 
                  FROM etat 
                  WHERE id_mot = (SELECT id_mot FROM mot WHERE nom_mot = ?)
                  AND isentree = 1"""
    
    def get_sortie(self, mot):
        return """SELECT nom_etat 
                  FROM etat 
                  WHERE id_mot = (SELECT id_mot FROM mot WHERE nom_mot = ?)
                  AND issortie = 1"""
    
    def get_transitions(self, mot, etat):
        return """SELECT id_etat, etiquette 
                  FROM transition t
                  JOIN etat e1 ON t.id_depart = e1.id_etat
                  WHERE e1.nom_etat = ?
                  AND e1.id_mot = (SELECT id_mot FROM mot WHERE nom_mot = ?)"""
```

**Question 8** - Code de BaseReconnaissance

```python
class BaseReconnaissance:
    def __init__(self, nom_base):
        self.dao = DAO(nom_base)
        self.li_mots_clef = self.dao.get_motsclef()
        self.base = self.dao.get_automates()
    
    def is_mot_clef(self, ch):
        return ch in [mot[0] for mot in self.li_mots_clef]
    
    def reconnaitre(self, ch):
        for mot_info in self.base:
            automate = self.dao.get_automate(mot_info)
            if automate.reconnaitre(ch):
                return mot_info
        return None
```

---

### 1.3 Conception et programmation orientée objet

**Question 9** - Cardinalités du diagramme de classes

- Sommet - Arc (départ) : 1 - *
- Sommet - Arc (arrivée) : 1 - *
- Arc - Graphe : * - 1
- Sommet - Graphe : * - 1
- Sommet - Automate (entrée) : 1..* - 1
- Sommet - Automate (sorties) : 1..* - 1
- Automate - Graphe : 1 - 1

**Question 10** - Code des classes Sommet, Arc et Graphe

```python
class Sommet:
    def __init__(self, num):
        self.num = num

class Arc:
    def __init__(self, depart, arrivee, car):
        self.depart = depart  # Sommet
        self.arrivee = arrivee  # Sommet
        self.car = car  # caractère (étiquette)

class Graphe:
    def __init__(self):
        self.arcs = []
    
    def add_arc(self, s1, s2, etiquette):
        arc = Arc(s1, s2, etiquette)
        self.arcs.append(arc)
    
    def get_sommets_source(self):
        """Retourne les sommets sources (sans arc entrant)"""
        sommets_depart = set(arc.depart for arc in self.arcs)
        sommets_arrivee = set(arc.arrivee for arc in self.arcs)
        return list(sommets_depart - sommets_arrivee) if self.arcs else []
    
    def get_all_sommets(self):
        """Retourne tous les sommets du graphe"""
        if not self.arcs:
            return []
        sommets = set()
        for arc in self.arcs:
            sommets.add(arc.depart)
            sommets.add(arc.arrivee)
        return list(sommets)
    
    def get_sommet_arrivee(self, s1, car, categ):
        """Trouve le sommet d'arrivée depuis s1 avec étiquette car et catégorie categ"""
        for arc in self.arcs:
            if arc.depart == s1 and arc.car == car:
                # Vérifier la catégorie si nécessaire
                return arc.arrivee
        return None
    
    def is_vide(self):
        return len(self.arcs) == 0
    
    def is_etat_source(self, s):
        for arc in self.arcs:
            if arc.arrivee == s:
                return False
        return True
    
    def is_arc(self, s1, etiquette):
        for arc in self.arcs:
            if arc.depart == s1 and arc.car == etiquette:
                return True
        return False
    
    def au_moins_un_arc(self):
        return len(self.arcs) > 0
```

**Question 11** - Nouveau diagramme avec arcs étiquetés

Le nouveau diagramme devrait inclure :

- Une classe `EtiquetteChiffre` héritant d'une classe abstraite `Etiquette`
- Une classe `EtiquetteLettre` héritant d'`Etiquette`
- La classe `Arc` aurait une association avec `Etiquette` au lieu d'un simple caractère

---

## Exercice II : Interpréteur pour un assembleur

### 2.1 Architecture et assembleur du processeur BUB25

**Question 12** - Schéma de l'architecture

```
[Mémoire 2000 octets] <---> [BUB25 64 bits]
                              |
                              +-- Registres R0-R7
                              +-- SP (Stack Pointer)
                              +-- PC (Program Counter)
                              +-- LR (Link Register)
                              +-- IOC (I/O Character)
                              |
                              +-- ALU
                              +-- Drapeaux (z, n)
                              |
                         [Périphériques I/O]
```

**Question 13** - Taille maximale de la mémoire adressable

Avec des instructions sur 64 bits, la taille maximale adressable dépend du nombre de bits dédiés à l'adresse dans le format d'instruction. Sans format précis, théoriquement 2^64 octets, mais en pratique limité par le format d'instruction.

**Question 14** - Mécanisme pour les comparaisons

Les comparaisons (CMP) soustraient deux valeurs et mettent à jour les drapeaux :

- `z = 1` si le résultat est 0 (égalité)
- `n = 1` si le résultat est négatif (premier opérande < deuxième)

Cela permet de tester : `=`, `≠`, `<`, `≤`, `>`, `≥`

**Question 15** - Explication du programme non documenté

Le programme calcule la somme des nombres pairs de 0 à 9:

```assembly
s = 0
for i in range(10):
    s += i
    if s % 2 == 0:
        print(s)
print(s)
```

**Question 16** - Programme assembleur équivalent

```assembly
    STO #0, R0       ; s = 0
    STO #0, R1       ; i = 0
boucle:
    CMP R1, #10      ; comparer i avec 10
    BGE fin          ; si i >= 10, sortir
    ADD R0, R1       ; s += i
    CPY R0, R2       ; copier s dans R2
    SHL R2           ; multiplier R2 par 2 (décalage gauche)
    CMP R2, R0       ; comparer 2*s avec s
    BEQ pair         ; si s % 2 == 0
    JMP suite
pair:
    CPY R0, IOC      ; afficher s
suite:
    ADD R1, #1       ; i++
    JMP boucle
fin:
    CPY R0, IOC      ; afficher s final
    HLT
```

---

### 2.2 Interpréteur en Java

**Question 17** - Implémentation de l'association instructions

L'association `instructions` est implémentée comme une **composition** : le Programme contient une liste d'Instructions qui lui appartiennent exclusivement.

**Question 18** - Compléter le diagramme

Il manque **les étiquettes** dans le diagramme. Il faudrait ajouter une classe ou un attribut pour gérer les labels (comme "addition", "traitement1", etc.).

**Question 19** - Représentation des opérandes

Les opérandes devraient être représentés par une **interface `Operande`** avec plusieurs implémentations :

- `OperandeRegistre` (ex: R0, R1)
- `OperandeImmediat` (ex: #5, #10)
- `OperandeAdresse` (ex: #addr)

Justification : polymorphisme, extensibilité, et respect du principe ouvert/fermé.

**Question 20** - Variables d'instance de Machine

```python
class Machine:
    def __init__(self):
        self.registres = [0] * 8  # R0 à R7
        self.sp = 0
        self.pc = 0
        self.lr = 0
        self.ioc = 0
        self.z = False  # drapeau zéro
        self.n = False  # drapeau négatif
        self.memoire = [0] * 2000
```

---

### 2.3 Interpréteur en Python

**Question 21** - Méthode parser

```python
def parser(self, fichier):
    """Parse un fichier assembleur BUB25"""
    programme = []
    etiquettes = {}
    
    with open(fichier, 'r') as f:
        lignes = f.readlines()
    
    # Premier passage : identifier les étiquettes
    adresse = 0
    for ligne in lignes:
        ligne = ligne.strip()
        if ':' in ligne:  # c'est une étiquette
            etiquette = ligne.replace(':', '')
            etiquettes[etiquette] = adresse
        elif ligne and not ligne.startswith(';'):  # instruction
            adresse += 1
    
    # Deuxième passage : parser les instructions
    for ligne in lignes:
        ligne = ligne.strip()
        if ligne and not ligne.startswith(';') and ':' not in ligne:
            # Parser l'instruction
            parties = ligne.split()
            operation = parties[0]
            operandes = [p.strip(',') for p in parties[1:]]
            
            # Remplacer les étiquettes par des adresses
            operandes_resolus = []
            for op in operandes:
                if op in etiquettes:
                    operandes_resolus.append(f"#{etiquettes[op]}")
                else:
                    operandes_resolus.append(op)
            
            instruction = Instruction(operation, operandes_resolus)
            programme.append(instruction)
    
    return programme
```

**Question 22** - Types d'erreurs détectées

La méthode `parser` peut détecter :

- Erreurs de syntaxe (instructions mal formées)
- Étiquettes non définies
- Nombre incorrect d'opérandes
- Opérandes invalides (registres inexistants)
- Instructions inconnues

**Question 23** - Diagramme de classes Python

```
Programme
└── instructions: List[Instruction]

Instruction
├── operateur: str
└── operandes: List[Operande]

Operande (interface/classe abstraite)
├── OperandeRegistre(num: int)
├── OperandeImmediat(valeur: int)
└── OperandeAdresse(adresse: int)

Machine
├── registres: List[int]
├── memoire: List[int]
├── pc, sp, lr, ioc: int
├── z, n: bool
└── executer(programme: Programme)
```

**Question 24** - Code des méthodes

```python
class Instruction:
    def __init__(self, operateur, operandes):
        self.operateur = operateur
        self.operandes = operandes

class Machine:
    def executer_HLT(self):
        self.running = False
    
    def executer_JSR(self, adresse):
        self.lr = self.pc  # sauvegarder l'adresse de retour
        self.pc = adresse
    
    def executer_ADD(self, reg1, operande2):
        """reg1 = reg1 + operande2"""
        valeur = self.get_valeur_operande(operande2)
        self.registres[reg1] = self.registres[reg1] + valeur
    
    def get_valeur_operande(self, operande):
        if operande.startswith('#'):
            return int(operande[1:])  # valeur immédiate
        elif operande.startswith('R'):
            return self.registres[int(operande[1])]  # registre
        else:
            return self.memoire[int(operande)]  # adresse mémoire
```

---

### 2.4 Système multi-tâches

**Question 25** - Durée d'exécution en cycles

La durée d'exécution d'une instruction est évaluée en nombre de cycles. Les paramètres influents :

- Accès mémoire (lent)
- Opérations ALU (rapide)
- Branchements (peuvent vider le pipeline)

Instruction "brève" : `ADD R1, R2` (2-3 cycles) Instruction "longue" : `LOD #addr(R1), R2` (5-10 cycles)

**Question 26** - Ajouts au diagramme pour multi-tâches

Il faudrait ajouter :

- Classe `Processus` avec :
    - `pid`: identifiant
    - `etat`: (prêt, en cours, bloqué)
    - `contexte`: sauvegarde des registres
    - `quantum`: temps alloué
- Classe `Ordonnanceur` pour gérer la file de processus

**Question 27** - Instructions pour suspension anticipée

Instructions pouvant causer une suspension :

- `LOD` (attente mémoire)
- `STO` (attente mémoire)
- `JSR` (appel de sous-programme)
- Instructions I/O

**Question 28** - Mécanismes d'isolation

Pour éviter qu'un processus interfère avec un autre :

- **Mémoire virtuelle** : chaque processus a son propre espace d'adressage
- **Protection mémoire** : zones mémoire protégées
- **Mode privilégié** : certaines instructions réservées au système
- **Sauvegarde/restauration du contexte** : registres sauvegardés à chaque changement
