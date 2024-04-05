---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: 
tags:
---
Les liens symboliques sont des entrées spéciales qui permettent d'accéder à un fichier ou à un répertoire en utilisant un chemin différent de celui d'origine. Ils sont reconnaissables par la lettre `l` à gauche de leur nom ou par une flèche dans la sortie de la commande `ls`, indiquant la destination ou la cible du lien symbolique.

Les liens symboliques ont plusieurs caractéristiques :

- Ils permettent d'accéder à une entrée sans créer de copie.
- Ils peuvent pointer vers un fichier, un répertoire ou un autre lien symbolique.
- Ils peuvent être absolus (chemin complet) ou relatifs (chemin relatif par rapport à la position du lien).
- Les liens symboliques en rouge indiquent des liens brisés.
- Ils sont créés à l'aide de la commande `ln -s`.
  ⇒ `ln -s ENTREE_EXISTANTE REPERTOIRE_Où_CREER_LE_LIEN`
  **Exemple :** `ln -s ../idea-IC-212-5080.55/bin/idea.sh idea`
			⇒ Créer un lien s'appelant `idea` 

Les liens symboliques sont utiles pour créer des raccourcis ou des raccourcis vers des fichiers ou des répertoires.