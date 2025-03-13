[Créer un jeu vidéo en 2D avec Unity](https://www.youtube.com/watch?v=Y3-iYIs16TI&list=PLUWxWDlz8PYKnrd27LTqOxL2lr3KhEVRT)

# Vidéo 1
## Le LevelDesign

Pour le système de levelDesign, nous pouvons utiliser le TileMap

> Un **tilemap** est une grille composée de petites images carrés appelée tuiles (tiles) qui sont placées côte à côte pour créer des environnements ou des niveaux dans les jeux vidéos, plus particulièrement en 2D, chaque case correspondant à une tuile spécifique
>
> On utilise les tilemaps pour leur efficacité, leur optimisation et leur flexibilité

> Un **tileset** est un ensemble d'images / tuiles utilisées pour créer un tilemap. Il contient toutes les tuiles nécessaires pour construire un niveau (les sols, murs ou tout autre objet décoratif)

---

Pour pouvoir faire une Tilemap, la première étape est d'importer un fichier **TileSheet** dans le dossier `Assets` de Unity
> [!Information]
>Il est conseillé classer tous ses fichiers dans des dossiers. Ainsi, créer un dossier `imports` dans le dossier `Assets` qui servira à stocker tous les fichiers importés.  Ainsi, ranger la tilesheet dans ce fichier




---
# Créer un bouton personnalisé



## 1. Préparation des Ressources Graphiques

*   **Image de fond du bouton :**
    *   Créez une image rectangulaire avec un fond jaune et une bordure (comme dans l'image).
    *   Utilisez un *9-Slice Sprite* pour que le bouton puisse s'étendre sans déformer les bords.
*   **Icône de ressource (pièce) :**
    *   Importez une image de pièce dorée ou une autre icône représentant la ressource nécessaire.
*   **Police de caractères :**
    *   Choisissez une police lisible et adaptée au style de votre jeu.  TextMeshPro offre plus de flexibilité et une meilleure qualité.

## 2. Création du Bouton dans Unity
Absolument ! Voici un guide complet sans blocs de Markdown pour créer un bouton d'invocation dynamique dans Unity, similaire à l'image fournie, qui se désactive lorsque le joueur n'a pas assez de ressources et dont le prix augmente à chaque utilisation. Nous utiliserons TextMeshPro pour une qualité de texte supérieure.

# Créer un Bouton d'Invocation Dynamique dans Unity (Guide Complet)

Ce guide explique en détail comment créer un bouton d'invocation dans Unity qui se désactive lorsque le joueur n'a pas assez de ressources et dont le prix augmente à chaque utilisation.

## 1. Préparation des Ressources Graphiques

- **Image de fond du bouton :**
    
    - Créez une image rectangulaire avec un fond jaune et une bordure (comme dans l'image).
        
    - Utilisez un _9-Slice Sprite_ pour que le bouton puisse s'étendre sans déformer les bords.
        
- **Icône de ressource (pièce) :**
    
    - Importez une image de pièce dorée ou une autre icône représentant la ressource nécessaire.
        
- **Police de caractères :**
    
    - Choisissez une police lisible et adaptée au style de votre jeu. TextMeshPro offre plus de flexibilité et une meilleure qualité.
        

## 2. Création du Bouton dans Unity

1. **Créer un Canvas:**
    
    - GameObject -> UI -> Canvas
        
    - Assurez-vous que le Canvas est en mode "Screen Space - Overlay" ou "Screen Space - Camera" dans l'Inspecteur.
        
2. **Créer le Bouton:**
    
    - GameObject -> UI -> Button - TextMeshPro
        
    - Cela crée un bouton avec un fond (`Image`) et un texte (`TextMeshPro - Text`).
        
3. **Remplacer le fond:**
    
    - Dans l'Inspecteur du bouton, remplacez la `Source Image` du composant `Image` par votre image de fond.
        
    - Si vous utilisez un 9-Slice Sprite, ajustez les paramètres "Border" dans l'Inspecteur de l'Image.
        
4. **Redimensionner le Bouton:**
    
    - Utilisez l'outil Rectangle (T) dans la vue Scene pour ajuster la taille.
        
5. **Modifier le texte "Summon":**
    
    - Sélectionnez l'objet enfant "Text (TMP)".
        
    - Dans l'Inspecteur, changez le champ "Text" à "Summon".
        
    - Ajustez `Font Asset`, `Font Size`, `Color`, et `Alignment` pour correspondre au style.
        
6. **Ajouter l'Icône de Ressource:**
    
    - GameObject -> UI -> Image
        
    - Faites-en un enfant du bouton.
        
    - Dans l'Inspecteur, assignez l'image de l'icône à `Source Image`.
        
    - Ajustez la position et la taille avec l'outil Move (W) et l'outil Scale (R).
        
7. **Ajouter le Texte du Prix:**
    
    - GameObject -> UI -> Text - TextMeshPro
        
    - Faites-en un enfant du bouton.
        
    - Dans l'Inspecteur, changez le champ "Text" à "190" (ou le prix initial).
        
    - Ajustez `Font Asset`, `Font Size`, `Color`, et `Alignment`.
        
    - Positionnez-le à côté de l'icône de ressource.
        

## 3. Script `SummonButton.cs` (Complet)


```Csharp
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class SummonButton : MonoBehaviour
{
    [Header("Configuration")]
    public int initialSummonCost = 190; // Prix initial
    public float priceIncreaseFactor = 1.1f; // Facteur d'augmentation du prix

    [Header("Références UI")]
    public TextMeshProUGUI priceText;  // Référence au TextMeshPro affichant le prix
    public Button button;              // Référence au composant Button

    [Header("Dépendances")]
    public ResourceManager resourceManager; // Exemple: un gestionnaire de ressources

    private int currentSummonCost;     // Prix actuel (modifiable)

    void Start()
    {
        InitializeButton();
    }

    void InitializeButton()
    {
        // Initialisation du prix actuel
        currentSummonCost = initialSummonCost;

        // Vérification des références
        if (priceText == null)
        {
            Debug.LogError("priceText n'est pas assigné !");
            enabled = false;
            return;
        }

        if (button == null)
        {
            button = GetComponent<Button>();
            if (button == null)
            {
                Debug.LogError("Button n'est pas assigné et n'a pas pu être trouvé!");
                enabled = false;
                return;
            }
        }

        // Initialisation de l'UI
        UpdatePriceText();
        UpdateInteractableState();
    }

    public void OnClick()
    {
        TrySummon();
    }

    void TrySummon()
    {
        if (resourceManager.HasEnoughResources(currentSummonCost))
        {
            PerformSummon();
        }
        else
        {
            HandleInsufficientResources();
        }
    }

    void PerformSummon()
    {
        resourceManager.DeductResources(currentSummonCost);
        SummonUnit(); // Action d'invocation
        IncreasePrice();  // Augmenter le prix
        UpdateUI();
    }

    void HandleInsufficientResources()
    {
        Debug.Log("Pas assez de ressources !");
        // TODO: Ajouter un feedback visuel (par exemple, un message à l'écran)
    }

    void IncreasePrice()
    {
        currentSummonCost = Mathf.RoundToInt(currentSummonCost * priceIncreaseFactor);
    }

    void UpdateUI()
    {
        UpdatePriceText();
        UpdateInteractableState();
    }

    void UpdatePriceText()
    {
        priceText.text = currentSummonCost.ToString();
    }

    void UpdateInteractableState()
    {
        button.interactable = resourceManager.HasEnoughResources(currentSummonCost);
    }

    void SummonUnit()
    {
        // TODO: Remplacer avec la logique réelle de votre jeu pour invoquer l'unité.
        Debug.Log("Unité invoquée !");
    }
}

```

## 4. Explications du Script

- `[Header("...")]` : Ces attributs divisent l'Inspecteur en sections pour une meilleure organisation.
    
- **Variables :**
    
    - `initialSummonCost` : Le prix de base de l'invocation.
        
    - `priceIncreaseFactor` : Multiplicateur pour augmenter le prix à chaque invocation.
        
    - `priceText` : Référence à l'objet TextMeshPro affichant le prix. _Important :_ Assignez cette référence dans l'Inspecteur.
        
    - `button` : Référence au composant Button. Le script tente de l'obtenir automatiquement si non assigné.
        
    - `resourceManager` : Référence à votre script de gestion des ressources. _Important :_ Assignez cette référence dans l'Inspecteur.
        
    - `currentSummonCost` : Le prix actuel de l'invocation (modifié dynamiquement).
        
- **`Start()` :**
    
    - Appelle `InitializeButton()` au démarrage.
        
- **`InitializeButton()`:**
    
    - Initialise `currentSummonCost`.
        
    - Vérifie si `priceText` et `button` sont assignés et affiche des erreurs si ce n'est pas le cas. Désactive le script si des références sont manquantes pour éviter des erreurs d'exécution.
        
    - Initialise l'état du bouton et affiche le prix initial.
        
- **`OnClick()` :**
    
    - Appelle `TrySummon()` quand le bouton est cliqué.
        
- **`TrySummon()`:**
    
    - Vérifie si le joueur a assez de ressources avec `resourceManager.HasEnoughResources()`.
        
    - Si oui, appelle `PerformSummon()`.
        
    - Sinon, appelle `HandleInsufficientResources()`.
        
- **`PerformSummon()`:**
    
    - Déduit les ressources avec `resourceManager.DeductResources()`.
        
    - Invoque l'unité avec `SummonUnit()`.
        
    - Augmente le prix avec `IncreasePrice()`.
        
    - Met à jour l'UI avec `UpdateUI()`.
        
- **`HandleInsufficientResources()`:**
    
    - Affiche un message (à améliorer avec un feedback visuel).
        
- **`IncreasePrice()` :**
    
    - Multiplie le prix actuel par le facteur d'augmentation.
        
- **`UpdateUI()`:**
    
    - Met à jour le texte du prix et l'état du bouton.
        
- **`UpdatePriceText()` :**
    
    - Met à jour l'affichage du prix.
        
- **`UpdateInteractableState()` :**
    
    - Active ou désactive le bouton (`button.interactable`) en fonction des ressources du joueur.
        
- **`SummonUnit()` :**
    
    - _À remplacer avec votre logique d'invocation_.
        

## 5. Implémentation de la logique de gestion des ressources

Vous devez avoir un script (par exemple, `ResourceManager.cs`) qui gère les ressources du joueur. Ce script doit avoir au moins les fonctions suivantes :

```Csharp
public class ResourceManager : MonoBehaviour
{
    public int currentResources = 1000; // Exemple: Ressources initiales

    public bool HasEnoughResources(int cost)
    {
        return currentResources >= cost;
    }

    public void DeductResources(int cost)
    {
        currentResources -= cost;
        Debug.Log("Ressources déduites. Ressources restantes: " + currentResources);
        // TODO: Mettre à jour l'UI pour afficher les ressources restantes.
    }

    // ... autres fonctions de gestion des ressources ...
}

```

## 6. Liaison des éléments dans l'Inspecteur Unity

1. Sélectionnez le GameObject du bouton.
    
2. Dans l'Inspecteur du composant `SummonButton` :
    
    - Faites glisser l'objet TextMeshPro du prix vers le champ `Price Text`.
        
    - Faites glisser le GameObject du bouton vers le champ `Button` (si ce n'est pas déjà assigné).
        
    - Faites glisser le GameObject contenant le script `ResourceManager` vers le champ `Resource Manager`.
        
3. Assurez-vous d'ajuster les valeurs de `Initial Summon Cost` et `Price Increase Factor` selon vos besoins.
    

## 7. Désactivation du Bouton

Le bouton est désactivé en définissant `button.interactable = false;`. Le script le fait automatiquement en fonction des ressources du joueur. Vous pouvez aussi changer la `Transition` du bouton (dans le composant `Button`) pour un feedback visuel plus clair. Les options sont "Color Tint", "Sprite Swap", et "Animation".

## 8. Améliorations Supplémentaires

- **Animation :** Ajoutez une animation subtile au clic.
    
- **Feedback visuel :** Affichez un message clair si le joueur n'a pas assez de ressources.
    
- **Internationalisation :** Utilisez un système de localisation pour le texte "Summon".
    
- **Sons :** Ajoutez des effets sonores au clic et à l'invocation.
    

## 9. Dépannage

- **Erreurs de référence :** Vérifiez que toutes les références dans l'Inspecteur sont correctement assignées.
    
- **Le prix n'augmente pas :** Vérifiez que `Price Increase Factor` est supérieur à 1.
    
- **Le bouton ne se désactive pas :** Assurez-vous que `ResourceManager.HasEnoughResources()` retourne la bonne valeur et que `UpdateInteractableState()` est appelée après chaque invocation et changement de ressources.
    
- **Le texte du prix ne se met pas à jour :** Vérifiez que `UpdatePriceText()` est appelée et que le champ `priceText` est correctement lié.
    

En suivant ce guide, vous devriez avoir un bouton d'invocation dynamique fonctionnel dans votre jeu Unity. N'hésitez pas à poser d'autres questions si vous rencontrez des problèmes !

### Citations:

1. [https://pplx-res.cloudinary.com/image/upload/v1741883571/user_uploads/EpfXTpNgUPKAyUf/image.jpg](https://pplx-res.cloudinary.com/image/upload/v1741883571/user_uploads/EpfXTpNgUPKAyUf/image.jpg)

---

Réponse de Perplexity: pplx.ai/share

