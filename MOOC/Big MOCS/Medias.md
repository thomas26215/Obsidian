# Toutes catégories
```dataview
TABLE Type, Auteur, Categorie, FullName as "Nom formation", Numero FROM "Permanent/Medias" SORT Type ASC, Categorie ASC, FullName ASC, Numero ASC
```
# Vidéos

```dataview
TABLE Auteur, Categorie FROM "Permanent/Medias" WHERE Type="Video" SORT Auteur ASC, Categorie ASC
```
# Livre

# Podcast

# Article