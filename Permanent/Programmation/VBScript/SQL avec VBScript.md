Pour se connecter à une base de données SQL, vous devez créer une chaîne de connexion et utiliser l'objet `ADODB.Connection`.

## Exemple de connexion à une base de données SQL Server

text

`Dim conn, connectionString Set conn = CreateObject("ADODB.Connection") ' Chaîne de connexion connectionString = "Provider=SQLOLEDB;Data Source=NomDuServeur;Initial Catalog=NomDeLaBaseDeDonnées;User ID=VotreUtilisateur;Password=VotreMotDePasse;" ' Ouvrir la connexion conn.Open connectionString If conn.State = 1 Then     MsgBox "Connexion réussie!" Else     MsgBox "Échec de la connexion." End If`

## 2. Exécution de requêtes SQL

## a. Exécution d'une requête SELECT

Pour récupérer des données, utilisez une requête SELECT et un objet `Recordset`.

text

`Dim rs, sqlQuery sqlQuery = "SELECT * FROM NomDeLaTable" Set rs = conn.Execute(sqlQuery) Do While Not rs.EOF     MsgBox "Nom : " & rs("NomColonne")    rs.MoveNext Loop rs.Close`

## b. Exécution d'une requête INSERT, UPDATE ou DELETE

Pour modifier des données, utilisez la méthode `Execute` sans un recordset.

text

`Dim insertQuery insertQuery = "INSERT INTO NomDeLaTable (Colonne1, Colonne2) VALUES ('Valeur1', 'Valeur2')" conn.Execute insertQuery`

## 3. Gestion des erreurs

Il est important de gérer les erreurs lors de l'exécution des requêtes.

## Exemple de gestion des erreurs :

text

`On Error Resume Next conn.Execute insertQuery If Err.Number <> 0 Then     MsgBox "Erreur : " & Err.Description    Err.Clear ' Réinitialiser l'erreur End If On Error GoTo 0 ' Réinitialiser la gestion des erreurs`

## 4. Fermeture de la connexion

N'oubliez pas de fermer la connexion après avoir terminé vos opérations.

text

`conn.Close Set conn = Nothing ' Libérer l'objet`

## 5. Utilisation de fichiers SQL pour les tests

Vous pouvez exécuter des scripts SQL stockés dans des fichiers `.sql`.

## Exemple d'exécution d'un fichier SQL :

text

`Dim fso, sqlFile, sqlCommand Set fso = CreateObject("Scripting.FileSystemObject") Set sqlFile = fso.OpenTextFile("C:\chemin\vers\script.sql", 1) ' 1 pour lecture Do While Not sqlFile.AtEndOfStream     sqlCommand = sqlFile.ReadLine()         ' Exécuter la commande si elle n'est pas vide    If Trim(sqlCommand) <> "" Then        conn.Execute sqlCommand    End If Loop sqlFile.Close`

## 6. Tests unitaires et validation des résultats

Pour effectuer des tests sur les résultats retournés par vos requêtes, comparez les résultats attendus avec ceux obtenus.

## Exemple :

text

`Dim expectedValue, actualValue expectedValue = "ValeurAttendue" actualValue = rs("Colonne") If actualValue = expectedValue Then     MsgBox "Test réussi!" Else     MsgBox "Test échoué! Attendu : " & expectedValue & ", Obtenu : " & actualValue End If`

Cette note résume les étapes essentielles pour interagir avec des bases de données SQL en utilisant VBScript et ADO. En suivant ces exemples et bonnes pratiques, vous pourrez manipuler efficacement vos données et automatiser vos tests. Si vous avez besoin d'informations supplémentaires ou d'exemples spécifiques, n'hésitez pas à demander !