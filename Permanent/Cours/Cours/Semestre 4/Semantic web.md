# **Cours : Le Web Sémantique**

## **Introduction**  
Le Web sémantique est une extension du Web classique, conçu pour permettre aux machines de comprendre et d’interpréter les données. Contrairement au Web classique, où les données sont destinées aux humains, le Web sémantique repose sur des métadonnées et des structures spécifiques, rendant les informations exploitables automatiquement.

---

## **1. Web Classique vs Web Sémantique**

### **1.1 Le Web Classique**  
Le **World Wide Web (WWW)** est un système de documents hypertextes liés et accessibles via Internet.  
**Caractéristiques :**  
- Basé sur le modèle **client/serveur**.  
- Utilise des standards comme HTTP, HTML et URI.  
- Conçu pour afficher des informations destinées à des humains.  

**Limites :**  
Le Web classique ne permet pas aux machines d’interpréter la signification des données.

---

### **1.2 Le Web Sémantique**  
Le Web sémantique ajoute des descriptions structurées et un contexte aux données pour permettre aux machines de les traiter.  
**Objectifs :**  
1. Améliorer la récupération d’informations.  
2. Faciliter l’exploration et la gestion des relations entre données.  
3. Automatiser les processus, comme la génération de documents ou l’analyse des relations.  
4. Créer des bases de connaissances exploitables.  

---

## **2. Les Briques Fondamentales du Web Sémantique**

### **2.1 XML (eXtensible Markup Language)**  
XML est utilisé pour structurer et transporter des données. Contrairement à HTML, XML ne gère pas l’affichage, mais l’organisation des données.

### **2.2 RDF (Resource Description Framework)**  
RDF est un modèle de données structuré sous forme de triplets :  
- **Sujet :** La ressource identifiée.  
- **Prédicat :** La propriété ou relation.  
- **Objet :** La valeur ou une autre ressource.

### **2.3 OWL (Web Ontology Language)**  
OWL est un langage permettant de modéliser des relations complexes et de raisonner sur les données.

---

## **3. XML (eXtensible Markup Language)**

### **3.1 Structure d’un Document XML**  
Un document XML contient :  
- **Prologue :** Spécifie la version XML et l’encodage.  
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  ```
- **Éléments :** Les balises encapsulent les données.  
  ```xml
  <livre>
      <titre>Harry Potter</titre>
      <auteur>J.K. Rowling</auteur>
  </livre>
  ```
- **Attributs :** Fournissent des informations supplémentaires.  
  ```xml
  <livre genre="fantastique">
      <titre>Harry Potter</titre>
  </livre>
  ```

---

### **3.2 Validation XML avec DTD et XML Schema**

#### **a) DTD (Document Type Definition)**  
DTD spécifie la structure autorisée d’un document XML.  
Exemple :  
```xml
<!DOCTYPE livre SYSTEM "livre.dtd">
<!ELEMENT livre (titre, auteur)>
<!ELEMENT titre (#PCDATA)>
<!ELEMENT auteur (#PCDATA)>
```

#### **b) XML Schema**  
XML Schema est plus puissant que DTD.  
Exemple :  
```xml
<xs:element name="livre">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="titre" type="xs:string"/>
            <xs:element name="auteur" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

---

### **3.3 Différences entre DTD et XML Schema**

| **Critères**            | **DTD**                         | **XML Schema**                   |
|-------------------------|----------------------------------|-----------------------------------|
| Syntaxe                 | Propre à DTD                   | Basée sur XML                    |
| Types de données        | Texte uniquement               | Supporte nombres, dates, etc.    |
| Support                 | Plus ancien                    | Plus moderne et robuste          |

---

## **4. XPath : Sélection de Nœuds dans XML**

### **4.1 Terminologie**  
- **Nœud racine :** Point de départ.  
- **Élément :** Balise XML.  
- **Attribut :** Propriété d’un élément.  
- **Texte :** Contenu d’un élément.  

### **4.2 Exemples de Sélection avec XPath**

Exemple de document :  
```xml
<bookstore>
    <book>
        <title lang="en">Harry Potter</title>
        <price>29.99</price>
    </book>
    <book>:%y+

        <title lang="fr">Le Petit Prince</title>
        <price>25.50</price>
    </book>
</bookstore>
```

| **Expression XPath**            | **Résultat**                                         |
|---------------------------------|-----------------------------------------------------|
| `/bookstore`                    | Sélectionne l’élément `<bookstore>`.               |
| `/bookstore/book`               | Sélectionne tous les `<book>` enfants directs.     |
| `//title`                       | Sélectionne tous les `<title>`.                    |
| `//book[price>28.00]`           | Sélectionne les `<book>` où le prix > 28.00.       |
| `/bookstore/book[last()]`       | Sélectionne le dernier `<book>` sous `<bookstore>`.|
| `/bookstore/book[1]`            | Sélectionne le 1er `<book>` sous `<bookstore>`.    |
| `/bookstore/book[1]`            | Sélectionne le 1er `<book>` sous `<bookstore>`.    |
| `//@lang`                       | Sélectionne tous les attributs `lang`.             |

---

## **5. XQuery : Requêtes XML**

XQuery permet de manipuler les données XML avec plus de flexibilité qu’XPath.

### **5.1 Syntaxe et Exemples**  
Sélectionner les titres des livres :  
```xquery
for $livre in doc("bookstore.xml")/bookstore/book
return <titre>{$livre/title/text()}</titre>
```

FLWOR (For, Let, Where, Order by, Return) :  
```xquery
for $i in //Member let $j := doc("MemberAges.xml")//Member[@id eq $i/@id]/Age where number($i/@id) <=  order by $i/Name/text() return 
```

```xquery
for $dvd in /dvds/dvd
order by number($dvd/price) ascending
return $dvd/title/text()
```

```xquery
/dvds/dvd[director = 'Cameron']/title/text()
```


## **6. RDF (Resource Description Framework)**

### **6.1 Modèle RDF**  
Les données sont représentées sous forme de triplets :  
- **Sujet :** URI de la ressource.  
- **Prédicat :** Propriété ou relation.  
- **Objet :** Valeur ou URI cible.

Exemple en syntaxe RDF/XML :  
```xml
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
    <rdf:Description rdf:about="http://example.org/book1">
        <title>Harry Potter</title>
        <author>J.K. Rowling</author>
    </rdf:Description>
</rdf:RDF>
```

---

## **7. OWL (Web Ontology Language)**

OWL permet de modéliser des relations complexes, comme des hiérarchies ou des concepts imbriqués.  

Exemple : Définir une relation entre "Étudiant" et "Université".

---

## **8. SPARQL : Requêtes pour RDF**

SPARQL est utilisé pour interroger des bases RDF.  

Exemple :  
```sparql
SELECT ?titre ?auteur
WHERE {
    ?livre rdf:type ex:Livre .
    ?livre ex:titre ?titre .
    ?livre ex:auteur ?auteur .
}
```

---

## **9. Comparaison des Technologies**

| **Technologie** | **Utilisation**                     |
|------------------|-------------------------------------|
| XML              | Structurer et transporter des données. |
| RDF              | Représenter des relations en triplets. |
| OWL              | Modéliser des concepts complexes.  |
| SPARQL           | Requêter des données RDF.          |

---
