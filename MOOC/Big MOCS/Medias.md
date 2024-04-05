# Toutes catégories
```dataview
TABLE Type, Auteur, Categorie, FullName, Numero FROM "Permanent/Medias" SORT Type ASC, Auteur ASC, Type ASC, Numero ASC
```
# Vidéos

```dataview
TABLE Auteur, Categorie FROM "Permanent/Medias" WHERE Type="Video" SORT Auteur ASC, Categorie ASC
```
# Livre

# Podcast

# Article