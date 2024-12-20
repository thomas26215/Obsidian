---
MOOC: "[[Programmation]]"
Langage: VBScript
Type: MsgBox
tags:
---
## `vbInformation`

`vbInformation` est une constante utilisée dans la fonction `MsgBox` pour afficher une boîte de message qui contient une icône d'information. Cela indique à l'utilisateur que le message est informatif. Par exemple :


```vb
MsgBox "Bonjour, " & userName & " !", vbInformation, "Message de bienvenue"
```

Dans cet exemple, lorsque l'utilisateur saisit son nom, un message de bienvenue s'affiche avec une icône d'information

## `vbExclamation`

`vbExclamation` est une autre constante utilisée dans la fonction `MsgBox`, mais elle affiche une icône d'exclamation. Cela signale généralement un avertissement ou une attention requise. Par exemple :

```vb
MsgBox "Aucun nom saisi.", vbExclamation, "Erreur"
```

Ici, si l'utilisateur n'a pas saisi de nom, un message d'erreur s'affiche avec une icône d'exclamation pour attirer l'attention sur le problème