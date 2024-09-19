---
MOOC: "[[Programmation]]"
Langage: C++
Type: Classes
tags:
---
Il faut créer un constructeur par recopie quand on souhaite "dupliquer" un objet, tout en pouvant modifier indépendemment les attributs. Il faut pour cela créer un constructeur par recopie de prototype `Classe (const Classe& autre);` :

```cpp
Classe::Classe(const Classe& autre) : m_intitule(autre.m_intitule){
	for(const auto& element : autre.m_liste){ //Parcourir tous les éléments de liste
		m_liste.push_back(new Element(*element)); //Ajouter l'élément courant
	}
}
```

>[!info] Quel objectif ?
>Le but ici est de prendre un object appelé `autre` de même type que l'objet actuel. Il faut maintenant prendre tous les éléments de `autre` pour les mettres dans l'objet actuel (que l'on peut aussi nommer `this`)



A partir de maintenant, je peux écrire le code suivant :
```Cpp
Groupe *groupeA = new Groupe("A");
groupeA->addElement("1");
groupeA->addElement("2");
groupeA->addElement("3");

Groupe *groupeB = new Groupe(*groupeA); //Constructeur par recopie
groupeB->setIntitule("B") //Je peux modifier sans que cela modifie pour groupeA
```

>[!warning] Attention pour =
>Si vous souhaitez faire `objet1 = objet2`, il est nécessaire de faire une [[Surcharge d'opérateurs]] sur = (`void operator=(ClassObjet autre)){m_intitule = autre.m_intitule;...}`