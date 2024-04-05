Il est possible de créer un lien d'une page vers une autre en HTML. Pour ceci, il faut utiliser la baliser `<a>` (Cette balise signifie *anchor*). Dans cette balise, il faut rajouter l'attribut `href=""` qui nous permettra de rajouter le lien vers la nouvelle page.
Voici un exemple :
```HTML
<a href="Nouvelle page.html">Lien vers la nouvelle page</a>
```

![[Lien hypertext.png]]

Il est possible de créer un lien vers une page interne mais également vers una page externe. Pour cela, il suffit de remplace le nom de notre fichier par le lien du site Internet

Si le lien interne vers la nouvelle page ne se trouve pas dans le dossier de la page parent, il est possible de se référer au fichier [[Vocabulaire de base pour les systèmes de fichiers]]

**Exemple** :
```HTML
<a href="../../Dossier1/Dossier2/Nouvelle page.html"></a>
```
