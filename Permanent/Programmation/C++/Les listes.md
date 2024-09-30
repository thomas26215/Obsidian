Pour déclarer une liste, il faut faire `std::vector<T> contenu;`
>[!wraning] Liste d'objets ?
>Si je souhaite déclarer une iiste d'objets (Ex : de personnes), il faut que je fasse `std::vector<Personne*> personnes;`


Pour parcours tous les élements de la liste, je peux faire :
```cpp
std::vector<int> contenu;
contenu.push_back(4);
contenu.push_back(7);


int variable = 7;

std::vector<int*> contenu2;
contenu2.push_back(&variable);
contenu2.push_back(&variable);
```

Pour supprimer un élement de la liste, il faut que je fasse `delete element`

# Cas pratiques
## 1 - Ajouter x élément de la liste
```cpp
for(const auto& element : liste){
	liste.push_back(variable);
}
```

## 2 - Supprimer tous les éléments d'une liste
```cpp
for(auto& element : liste){
	delete element;
}
```