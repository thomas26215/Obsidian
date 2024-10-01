En C++, il existe différentes les classes héritages. Voici comment les créer :
```cpp
class classe2 : public class1{

};
```

Les classes peuvent étendre de 3 types :
- `public`
- `private`
- `protected`
Il est également possible de faire de l'héritage multiple :
```cpp
class class3 : public class1, public class2{

};
```

## Constructeur et destructeur
Il faut redéfinir chacun de constructeur et destructeur dans les classes filles. Ils peuvent cependant appeler des constructeurs de la classe de base :

```cpp
class Mere{
public:
	Mere(Trajet& trajet, Tarif& tarif);
private:
	const Trajet& m_trajet;
	const Tarif& m_tarif;
}

class Fille : public mere{
public:
	Fille(Trajet& trajet, Tarif& tarif, Promotion& promotion);
private:
	Promotion& promotion;
}

Fille::Fille(Trajet& trajet, Tarif& tarif, Promotion& promotion):
Mere(trajet, tarif), m_promotion(promotion){}
```

## Fonctions virtuelles
Une fonction virtuelle (`virtual`) est une fonction que l'on veut voir apparaître dans toutes les classes filles.
Par exemple, si je j'ai les classes addition, soustraction, multiplication qui hérite de calcul, et que je veu que chaque fille de la classe calcul est une fonction `calculer(int a, int b);`, il faut que je le définisse en virtual dans la classe mère :
```cpp
class Calcul{
public:
	virtual int calculer(int a, int b) = 0; //Fonction virtuelle
};

class Addition : public Calcul{
public:
	int calculer(int a, int b) override; //Je redéfinis la méthode de la classe Calcul
}

class Soustraction : public Calcul{
public:
	int calculer(int a, int b) override;
}

class Multiplication : public Calcul{
public:
	int calculer(int a, int b) override;
}

int Addition::calculer(int a, int b){
	return a+b;
}

//Pareil pour la classe Soustraction et Multiplication

```

>[!Warning] Quelques spécificités
>- Si je veux définir une fonction purement virtuelle, il faut que je fasse `virtual type fonction() = 0;` je ne pourrai pas la définir dans la classe mère
>- Si je veux une fonction virtuelle mais que je puisse quand même l'utiliser dans la classe mère elle-même, il faut que je fasse : `virtual type fonction();` Je peux ainsi faire `Mere::type fonction(){...};`

## Redéfinition de fonction
Il est possible de redéfinir une fonction de la classe mère avec le mot-clé `@override`. Voici comment faire :
```cpp
class Mere{
public:
	public void afficher(int x);
};
class Fille: public Mere{
public:
	public void afficher(int x) override;
}
```