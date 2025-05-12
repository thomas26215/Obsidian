# 📘 Documentation de la Hiérarchie NameMapping - Projet TestComplete


Ce fichier décrit l’organisation hiérarchique du `NameMapping` utilisé dans notre projet TestComplete, pour faciliter la compréhension, la maintenance et le respect des conventions.

---

## 🏠 Contexte global

- **`MainView`**  
  C’est le **point d’entrée principal** de l’application. Toutes les autres fenêtres ou pages sont accessibles à partir de cet objet parent.

---

## 💬 Gestion des fenêtres contextuelles

- **`PopUpWindow`**  
  Contient les objets relatifs aux **popups** affichés dans l’application (fenêtres modales, boîtes de dialogue, etc.).

- **`PopupHome`**  
  Représente une page de type popup spécifique utilisée pour certaines interactions.

---

## 🔐 Page de connexion

- **`Login`**  
  Englobe tous les éléments de la **page de login** (champ email, mot de passe, bouton de validation, etc.).

---

## 📄 Pages générales

- **`LayoutRoot`**  
  Élément structurel principal utilisé sur **toutes les pages**. Sert de point de référence pour charger les composants visibles dans chaque vue.

---

## 🧭 Page d’accueil (navigation)

- **`HomeView`**  
  C’est la **page d’accueil principale** après la connexion. Elle regroupe de nombreux **boutons de redirection** vers les différentes pages de fonctionnalités (gestion des plants, des utilisateurs, etc.).

---

## 🛠 Pages fonctionnelles

- **`GeneralPane`**  
  Utilisé comme conteneur de base pour toutes les **pages fonctionnelles** (ex. : `Plant`, `Workcenters`, `ProductionOrder`, etc.).


**Exemple de structure typique d’une page fonctionnelle :**

```text
MainView  
└── LayoutRoot  
    └── GeneralPane  
        ├── General_Pane_Plant
        │   └── Plant_Pane_SideBar
        │       ├── Liste d'éléments de la SideBar
        │       └── BottomBar  
        │           ├── Bouton Ajouter  
        │           ├── Bouton Supprimer  
        │           └── Bouton Reload  
        │   └── MainPane  
        │       ├── TopBar  
        │       │   ├── Boutons divers  
        │       │   └── TextBox, ComboBox, etc.  
        │       ├── NavBar  
        │       │   ├── Page 1  
        │       │   ├── Page 2  
        │       │   └── ...  
        │       └── Pages (une par élément de NavBar)  
        ├── General_Pane_Workcenters  
        │   └── même structure que ci-dessus  
        └── General_Pane_ProductionOrder  
            └── même structure que ci-dessus
```

![[Drawing 2025-05-12 09.58.32.excalidraw]]

![[Drawing 2025-05-12 10.04.22.excalidraw]]

---

## Les tableaux

![[Drawing 2025-05-12 09.50.04.excalidraw]]

> [!warning]
> Attention ! Quand on clique sur une cellule, ça ne référence pas automatiquement la ligne. Il faut ainsi jouer avec l'object browser pour pouvoir retrouver l'élément

> [!utile]
> Quand une ligne avec tous ces éléments ont été correctement référence, il suffit de copier coller le namemapping de la ligne et de changer **A compléter** pour que cela corresponde à la nouvelle ligne

> [!utile]
> Quand on clique sur un élément texte et non sur la cellule, ca va créer automatiquement un élément qui va être ajouté dans le namapping de la cellule



---

## 🔧 Propriétés à renseigner (DataContext, ToolTip, etc.)

### ✅ Quand rajouter des **propriétés d’identification** :

#### 🟢 `DataContext`

À ajouter ​**uniquement si nécessaire**​, dans les cas suivants :

* Pour différencier **plusieurs vues similaires dans un même conteneur** :
  Exemple : `General_Pane_Plant` vs `General_Pane_Islets`.
* Pour distinguer **plusieurs onglets d’un même panneau** :
  Exemple : onglets `Properties`, `Islet`, `Containers` dans `Plant`.

**À ne pas utiliser :**

* Sur un élément ​**unique**​, inutile (voire contre-productif).
* Sur des composants internes comme `NavBar`, `TextBox`, `ComboBox`, `ToogleButton`, car TestComplete sait les différencier automatiquement.

> ❗ Trop de `DataContext` nuit à la maintenance : copier/coller de Panes nécessite alors une redéfinition du contexte inutilement.

---

#### 🟡 `ToolTip`

À utiliser ​**en dernier recours**​, ​**seulement si TestComplete n'arrive pas à distinguer deux éléments proches**​, malgré les autres propriétés disponibles.

> Ne surtout pas abuser du `ToolTip`. Un mauvais usage rend la maintenance du mapping instable et difficile à relire.

---

### 📝 Exemple récapitulatif des règles

| Élément                         | DataContext requis ?        | ToolTip requis ?        |
| ----------------------------------- | ----------------------------- | ------------------------- |
| `General_Pane_Plant`          | ✅ Oui                      | 🚫 Non                  |
| `NavBar`dans un`Pane`     | 🚫 Non                      | 🚫 Non                  |
| `TextBox`dans un`TopBar`  | 🚫 Non                      | 🚫 Non                  |
| Deux boutons identiques           | 🚫 Non (si autres props OK) | ✅ Si non distinguables |
| Deux pages imbriquées similaires | ✅ Oui                      | 🚫 Non                  |

---

### 💡 Astuce de manipulation

Quand vous collez un nouveau `Pane`, TestComplete affiche une erreur car l'élément n’est pas encore trouvé. Cliquez sur ​**Edit identification properties**​, puis **Update les DataContext** pour le `Pane` et ses éléments parents.

> [!Note]
> Cela ne fonctionnera que si ​**les contextes de page sont compatibles**​.

---

## Convention de nommage
### Nommage général
Il faut toujours nommer ses éléments de cette manière : `parent_typeElement_enfant`. Exemple : `plant_button_addPlant`

### Nommage des boutons
Il faut toujours nommer ses éléments de la manière suivante : Ce que fait le bouton et sur quoi porte l'action de ce bouton.
Exemple : `refreshPlants`,  `addPlant`, `removeIslet`.

>[!warning]
>Toujours nommer le bouton en fonction du **toolTip**