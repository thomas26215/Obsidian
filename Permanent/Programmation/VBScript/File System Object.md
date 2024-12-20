---
MOOC: "[[Programmation]]"
Langage: VBScript
Type: FSO
tags:
---
L'objet **FileSystemObject (FSO)** est un composant de VBScript utilisé pour interagir avec le système de fichiers d'un ordinateur. Il permet de gérer les fichiers et les dossiers, facilitant ainsi des opérations comme la création, la lecture, la modification et la suppression.

## Création d'une instance

Pour utiliser le `FileSystemObject`, il est nécessaire de créer une instance de cet objet. Cela se fait avec la commande suivante :


```vb
Set fso = CreateObject("Scripting.FileSystemObject")`
```
Cette ligne initialise un objet FSO que vous pouvez ensuite utiliser pour manipuler des fichiers et des dossiers.

## Vérification de l'existence d'un fichier

Avant d'effectuer des opérations sur un fichier, il est important de vérifier s'il existe. Cela peut être fait avec la méthode `FileExists` :

text

```vb
If fso.FileExists("chemin_du_fichier") Then
	' Le fichier existe, procéder à l'opération
End If`
```

Cette vérification aide à éviter les erreurs lors de l'accès à un fichier inexistant.

## Création d'un fichier

Pour créer un nouveau fichier texte, utilisez la méthode `CreateTextFile` :

```vb
Set file = fso.CreateTextFile("C:\monfichier.txt", True)
```

Cette commande crée un fichier nommé "monfichier.txt" dans le chemin spécifié.

## Ouverture d'un fichier existant

Pour lire le contenu d'un fichier existant, utilisez la méthode `OpenTextFile` :

```vb
Set file = fso.OpenTextFile("C:\monfichier.txt", 1) ' 1 pour lecture
```
Cela permet d'accéder au contenu du fichier pour le lire ou le traiter.

## Écriture dans un fichier

Pour ajouter du contenu à un fichier ouvert, utilisez la méthode `WriteLine` :


```vb
file.WriteLine("Texte à écrire")
```

Cette ligne écrit "Texte à écrire" à la fin du fichier.

## Suppression d'un fichier

Pour supprimer un fichier, utilisez la méthode `DeleteFile` :

text

```vb
fso.DeleteFile("C:\monfichier.txt")
```

Cela efface définitivement le fichier spécifié du système.

## Gestion des dossiers

Pour créer un nouveau dossier, utilisez la méthode `CreateFolder` :

```vb
fso.CreateFolder("C:\NouveauDossier")
```

Cela crée un dossier nommé "NouveauDossier" dans le chemin spécifié.

## Vérification de l'existence d'un dossier

Avant de créer un dossier, il est utile de vérifier s'il existe déjà :

text

```vb
If Not fso.FolderExists("C:\NouveauDossier") Then
	fso.CreateFolder("C:\NouveauDossier")
End If
```

Cela évite les erreurs liées à la tentative de création d'un dossier déjà existant.

## Suppression d'un dossier

Pour supprimer un dossier, utilisez la méthode `DeleteFolder` :


```vb
fso.DeleteFolder("C:\NouveauDossier")
```

Cette commande efface le dossier spécifié et son contenu. Cette note présente une vue d'ensemble complète et cohérente sur l'objet `FileSystemObject`, tout en permettant à chaque section d'être comprise indépendamment.

## Lire ligne par ligne
```vb
If fso.FileExists("C:\monfichier.txt") Then
	Dim infoFichier
	Set infoFichier = fso.GetFile("C:\monfichier.txt")
	MsgBox "Taille : " & infoFichier.Size & " octets" & vbCrLf & _ "Date de création : " & infoFichier.DateCreated
End If
```