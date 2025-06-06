# 📘 Fonctionnement de l’Action Based Image dans TestComplete

## 🔍 Qu’est-ce que l’Action Based Image ?

L'**Action Based Image** est une fonctionnalité de **TestComplete** permettant de créer des tests automatisés à partir de **captures d’éléments visuels**. Plutôt que d'utiliser des objets identifiés via le NameMapping, les actions (clics, entrées, validations...) sont déclenchées par reconnaissance d'images.

Cela s’avère utile dans les cas où **les éléments de l’interface ne sont pas détectables via l’inspecteur d’objets**, ou quand on travaille avec des environnements complexes

---

## ⚙️ Fonctionnement technique

- Chaque élément UI est capturé sous forme d’**image**.
- Les actions sont liées à ces images (clic, survol, etc.).
- TestComplete recherche ensuite cette image à l’écran, en comparant les pixels à ceux de la capture.
- On peut ajuster la reconnaissance avec des **paramètres de tolérance de couleur** et **de pixels**.
- Certaines actions, comme la **saisie de texte**, nécessitent du code (`Sys.Keys("Mon texte")`).

---

## ✅ Avantages

- **Utile quand le NameMapping échoue** ou que les éléments ne sont pas accessibles via l’arbre d’objets.
- Permet de tester des interfaces non standardisées ou visuellement complexes.
- Possibilité d’ajuster les critères de reconnaissance (tolérances) pour plus de flexibilité.
- Peut être plus simple au niveau des merges que le NameMapping ?

---

## ❌ Inconvénients / limitations

### 💻 Dépendance à la résolution d’écran

- Les tests **ne fonctionnent pas si la résolution d’écran diffère** de celle utilisée lors de la capture.
- L’image doit correspondre **exactement** en dimensions et en affichage.

### 🎨 Sensibilité à l’état visuel de l’élément

- Un même élément doit être capturé **plusieurs fois** selon ses états :
  - Bouton activé/désactivé
  - Champ vide/rempli
  - Sélectionné/non sélectionné
- Exemple : pour une liste, un élément peut nécessiter jusqu’à **3 images** (sélectionné, désélectionné gris, désélectionné blanc).

### 🔠 Entrée de texte non intuitive

- Nécessite d’écrire du code pour simuler la saisie : `Sys.Keys("Mon texte")`.
- Impossible d’entrer du texte par simple interaction image + clavier.

### 🔁 Re-mapping fréquent

- Une légère différence visuelle (contour, surbrillance, focus...) rend l’image non reconnue.
- Oblige à **capturer plusieurs variantes d’un même élément**, ce qui alourdit la maintenance.
- D’un test à l’autre, une action peut **cesser de fonctionner** sans raison apparente → **besoin de re-screener régulièrement**.

### 📦 Tests volumineux

- Chaque élément visuel stocke **plusieurs images**, ce qui **alourdit le projet**.
- Par exemple, pour **2 lignes dans un tableau de 5 colonnes**, on peut arriver à **jusqu’à 30 images** à capturer (2×5×3 états).

### 🧩 Cas pratiques problématiques

- **ComboBox** : pas encore exploitable avec l'Action Based Image.
- **StorageLocation** :
  - Si le texte de description passe de la ligne 1 à la ligne 2, l’image n’est plus reconnue.
  - Difficile de différencier deux éléments ayant **le même texte** dans une liste (risque de confusion).

### Le merge
Le nouveau NameMapping ne pose plus aucun problème. Chacun travaille dans son espace, et prévient quand il fait du changement dans le namamapping concernant la page pour que les autres personnes ne créent pas de conflit inutile

### Et si l'écran change ?


---

## ⚠️ Attention sur la tolérance de couleur et de pixels

- Les options **Color Tolerance** et **Pixel Tolerance** permettent d’élargir la reconnaissance (pour tolérer de légères variations visuelles).
- Mais si elles sont trop élevées :
  - Le moteur de reconnaissance peut **confondre deux éléments visuellement proches**.
  - Cela peut déclencher des actions sur **le mauvais élément**.
  - Si ces éléments sont utilisés dans **plusieurs tests**, **un changement de tolérance dans un test peut casser un autre test** qui utilisait la même image.

### ➤ Recommandation :

> Utiliser la tolérance avec prudence, **documenter les ajustements**, et éviter le partage d’images "tolérantes" entre plusieurs tests si les contextes sont différents.

---

## 📝 Conclusion

L’Action Based Image est un outil **pratique dans des cas spécifiques**, notamment quand les objets ne sont pas détectables par le NameMapping. Cependant, il nécessite **beaucoup de rigueur** :

- Multiplier les captures pour chaque état d’un même élément,
- S’assurer que la résolution ne change pas,
- Bien gérer les tolérances pour ne pas créer d’erreurs cachées,
- Accepter une **maintenance importante** sur le long terme.

Il est donc préférable de l’utiliser comme **complément ciblé**, plutôt qu’en remplacement complet des méthodes de tests classiques.
