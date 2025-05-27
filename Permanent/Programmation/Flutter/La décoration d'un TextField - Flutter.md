En flutter, il est possible de personnaliser l'apparence d'un `TextField` en utilisant la propriété `Decoration`. Ce dernier accepte l'objet `InputDecoration` permettant de modifier de nombreux aspects visuels du champs texte :
- `labeltext` : Affiche un label flottant
- `icon` : Ajoute une icône à gauche du champs
- `hintText` : Affiche un texte grisé à l'intérieur du champs qui disparaîtra dès que l'utilisateur commencera à rentrer du texte
- `hintStyle` : Permet de modifier le style du `hintText`
- `border` : Détermine la bordure par défaut du champs
    - `UnderlineInputBorder` : Bordure en ligne
    - `OutlineInputBorder` : Bordure en rectangle
- `enabledBorder` : Spécifie la bordure du champs quand il est actif mais pas sélectionné
- `focusedBorder` : Spécifie la bordure du champs quand il est actif et sélectionné

> [!Example]
> ```dart
> TextField(
> 	decoration: InputDecoration(
> 		labelText: "Nom",
> 		icon: Icon(Icons.person),
> 		hintText: "Entrez un nom",
> 	),
> ),
> ```

[!Example] Example avancé avec style personnalisé
```dart
import 'package:flutter/material.dart';
import 'package:unicons/unicons.dart';

class Header extends StatelessWidget {
    const Header({Key? key}) : super(key: key);

    final String trainingName;
    final ValueChanged<String> onChanged;


    @override
    Widget build(BuildContext context) {
        return Row(
            children: [
                GestureDetector(
                    onTap:() {
                        Navigator.pop(context);
                    },
                    child: const Icon(
                        UniconsLine.angle_left,
                        color: Colors.white,
                        size: 40,
                    ),
                ),
                Expanded(
                    child: TextField(
                        child: TextField(
                            style: Theme.of(context).textTheme.displayLarge?.copyWith(
                                color: Colors.white,
                                fontSize: 20,
                            ),
                            decoration: InputDecoration(
                                hintText: "Rechercher un entraînement",
                                hintStyle: Theme.of(context).textTheme.displayLarge?.copyWith(Colors.white54),
                                border: const UnderlineInputBorder(
                                    borderSide: BorderSide(color: Colors.white),
                                ),
                                border: const UnderlineInputBorder(
                                    borderSide: BorderSide(color: Colors.white),
                                ),
