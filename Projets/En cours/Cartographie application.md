### Partie Admin
#### Fonctionnalités Globale

L'application admin gère plusieurs aspects liés aux étudiants et aux offres, notamment :

- Gestion administrative des candidatures => `CandidatureController`
---
- Gestion des comptes étudiants => `CompteEtudiantController`
- Gestion des étudiants => `EtudiantController`
---
- Gestion des offres => `OffreController`
- Gestion des offres consultées => `OffreConsulteeController`
- Gestion des offres retenues => `OffreRetenueController`
---
- Gestion des entreprises disponibles => `EntrepriseController`
---
- Gestion du tableau de bord des candidatures des étudiants => `TableauDeBordController`
---
- Gestion de l'état des candidatures => `EtatCandidatureController`
-  Gestion de l'état des offres => `EtatOffreController`
- Gestion de l'état des recherches => `EtatRechercheController`

#### Structure commune des contrôleurs
Chacun des contrôleurs présentés contiennent la structure et les méthodes  suivantes :
- **Namespace** : `App\Controller\Admin`
- **Route de base** : `/{entité}` (sauf exceptions notées)

#### Structure commune des méthodes
Chacun des contrôleurs rassemblent un ensemble de méthodes. Chaque méthode est appelée par une route qui suit la même structure

**Méthodes :**
1. `index()` : Liste tous les éléments
   - Route : `GET /`
   - Utilise le repository correspondant
   - Rend la vue `Admin/{entité}/index.html.twig`

2. `new()` : Crée un nouvel élément
   - Route : `GET|POST /new`
   - Crée et gère un formulaire
   - Si valide : sauvegarde et redirige vers le controleur `CandidatureControlleur`
   - Sinon : affiche le formulaire (Rend la vue `Admin/{entité}/new.html.twig`)

3. `show()` : Affiche les détails d'un élément
   - Route : `GET /{id}`
   - Rend la vue `Admin/{entité}/show.html.twig`

4. `edit()` : Modifie un élément existant
   - Route : `GET|POST /{id}/edit`
   - Crée et gère un formulaire pré-rempli
   - Si valide : sauvegarde et redirige vers le controleur `CandidatureController`
   - Sinon : affiche le formulaire (Rend la vue `Admin/{Entité}/edit.html.twig`)

5. `delete()` : Supprime un élément
   - Route : `POST /{id}`
   - Vérifie le jeton CSRF
   - Supprime si valide et redirige vers le contrôleur `CandidatureController`

**Particularités** :
- `CandidatureController` : Gère la date d'action
- `CompteEtudiantController` : 
  - Utilise `UserPasswordHasherInterface` pour le hachage des mots de passe
  - Gère les rôles des utilisateurs
- `OffreConsulteeController` : Route de base `/offre_consultee`
- `OffreRetenueController` : Route de base `/offre_retenue`

Tous les contrôleurs implémentent les opérations CRUD avec des routes et méthodes spécifiques pour chaque opération dans la section admin de l'application. Ils suivent une structure similaire, avec des différences mineures dans les noms des entités et des routes.

### Partie Etudiant
Le contrôleur `DefaultControlleur`, qui est le contrôleur par défaut pour l'étudiant, a une méthode unique `index()̀` de route `/` et qui rend la vue `default/index.html.twig`. 

Le contrôleur `SecurityControlleur`, qui est le contrôleur d'authentification pour l'étudiant, a une méthode `/login` de route `/login` qui rend la vue `security/login.html.twig` et une méthode `/logout` de route `/logout` qui rend la vue `security/logout.html.twig`