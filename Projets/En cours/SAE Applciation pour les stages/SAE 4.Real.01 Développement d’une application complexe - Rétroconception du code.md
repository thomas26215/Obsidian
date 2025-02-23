



**Groupe 4**

*   VENOUIL Thomas
*   ARNAUD Sophie
*   BILS Brayan
*   JOANNICElouan
*   CELUZNIAK DE SOUZA Maria


<div style="text-align: center; margin-top: 300px; margin-bottom: 20px;">
    <img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4ZMW_BCVViAx7D_ZieOoXxe4LN-gK-smyG02vMs3hakMKz9QUb87FtANE72AyFNDQCiB9lrve3tS27a58cLIygIMt4IzFlID0Mr121F3WEhzBJDkgihUOZ3rSgKhdcI5fHImAlQ?key=bGQht-ukJAu38OyHPutoFyVF" style="width: 100%;" alt="Description de l'image" />
</div>

<div style="page-break-after: always;"></div>

**Table des matières :**
```table-of-contents

```

<div style="page-break-after: always;"></div>

# Introduction

Pour aider les étudiants pendant leur recherche de stage, la maîtrise d’ouvrage a mis à notre disposition le code d’une application de suivi de recherche de stage afin que nous l’améliorions. Cette application se sépare en deux parties, une partie serveur qui est utilisée par les professeurs et une partie client à destination des élèves.

L’architecture de l’application se présente sous la forme décrite dans la figure 1 et ses cas d’utilisations nous ont été résumés.

Lors de la première phase de ce projet, nous avions pour mission de procéder à une rétroconception du code qui nous a été fourni. Pour ce faire, nous avons tout d’abord affiné les diagrammes de classes et de cas d’utilisation. Nous avons ensuite procédé à une cartographie du code de chaque partie. Enfin, nous avons décrit la base de données à l'aide d’un diagramme adéquat.

<figure>
    <img src="Pasted image 20250220170526.png" width="400" alt="Description de l'image" />
    <figcaption>Architecture de la relation entre la partie client et serveur</figcaption>
</figure>



---

<figure> <img src="Pasted image 20250220170606.png" width="210" alt="Description de l'image" /> <figcaption>Figure 2 : Diagramme des cas d'utilisation</figcaption> </figure>


<div style="page-break-after: always;"></div>



# Partie serveur
## Description textuelle

### Partie Administrateur

#### Fonctionnalités Globales

L'application administrateur gère plusieurs aspects liés aux étudiants et aux offres, notamment :

*   Gestion administrative des candidatures => `CandidatureController`

---

*   Gestion des comptes étudiants => `CompteEtudiantController`
*   Gestion des étudiants => `EtudiantController`

---

*   Gestion des offres => `OffreController`
*   Gestion des offres consultées => `OffreConsulteeController`
*   Gestion des offres retenues => `OffreRetenueController`

---

*   Gestion des entreprises disponibles => `EntrepriseController`

---

*   Gestion du tableau de bord des candidatures des étudiants => `TableauDeBordController`

---

*   Gestion de l'état des candidatures => `EtatCandidatureController`
*   Gestion de l'état des offres => `EtatOffreController`
*   Gestion de l'état des recherches => `EtatRechercheController`

<div style="page-break-after: always;"></div>

#### Structure commune des contrôleurs

Chacun des contrôleurs présentés contiennent la structure et les méthodes suivantes :

*   **Namespace** : `App\Controller\Admin`
*   **Route de base** : `/{entité}` (sauf exceptions notées)

#### Structure commune des méthodes

Chacun des contrôleurs rassemblent un ensemble de méthodes. Chaque méthode est appelée par une route qui suit la même structure

**Méthodes :**

1.  `index()` : Liste tous les éléments
    *   Route : `GET /`
    *   Utilise le repository correspondant
    *   Rend la vue `Admin/{entité}/index.html.twig`
2.  `new()` : Crée un nouvel élément
    *   Route : `GET|POST /new`
    *   Crée et gère un formulaire
    *   Si valide : sauvegarde et redirige vers le controleur `CandidatureControlleur`
    *   Sinon : affiche le formulaire (Rend la vue `Admin/{entité}/new.html.twig`)
3.  `show()` : Affiche les détails d'un élément
    *   Route : `GET /{id}`
    *   Rend la vue `Admin/{entité}/show.html.twig`
4.  `edit()` : Modifie un élément existant
    *   Route : `GET|POST /{id}/edit`
    *   Crée et gère un formulaire pré-rempli
    *   Si valide : sauvegarde et redirige vers le controleur `CandidatureController`
    *   Sinon : affiche le formulaire (Rend la vue `Admin/{Entité}/edit.html.twig`)
5.  `delete()` : Supprime un élément
    *   Route : `POST /{id}`
    *   Vérifie le jeton CSRF
    *   Supprime si valide et redirige vers le contrôleur `CandidatureController`

<div style="page-break-after: always;"></div>

**Particularités :**

*   `CandidatureController` : Gère la date d'action
*   `CompteEtudiantController` :
    *   Utilise `UserPasswordHasherInterface` pour le hachage des mots de passe
    *   Gère les rôles des utilisateurs
*   `OffreConsulteeController` : Route de base `/offre_consultee`
*   `OffreRetenueController` : Route de base `/offre_retenue`

Tous les contrôleurs implémentent les opérations CRUD avec des routes et méthodes spécifiques pour chaque opération dans la section administrateur de l'application. Ils suivent une structure similaire, avec des différences mineures dans les noms des entités et des routes.



### Partie Etudiant

Le contrôleur `DefaultControlleur`, qui est le contrôleur par défaut pour l'étudiant, a une méthode unique `index()̀` de route `/` et qui rend la vue `default/index.html.twig`.

Le contrôleur `SecurityControlleur`, qui est le contrôleur d'authentification pour l'étudiant, a une méthode `/login` de route `/login` qui rend la vue `security/login.html.twig` et une méthode `/logout` de route `/logout` qui rend la vue `security/logout.html.twig`






## Diagramme

<figure>
    <img src="DiagrammeServeurSimple.png" alt="Diagramme de serveur simple" />
    <figcaption>Figure 3 : Diagramme de serveur</figcaption>
</figure>


<div style="page-break-after: always;"></div>

# Partie client
## Description textuelle

1.  Il y a une fonctionnalité d'**authentification** de l'utilisateur car :

    *   Le fichier `LoginActivity.java` contient le code de la classe `LoginActivity` qui gère l'interface et la logique d'authentification de l'utilisateur.
    *   Le fichier `activity_login.xml` **décrit la structure** de l'interface de connexion.
    *   Le modèle `Auth` est utilisé pour l'authentification.

---

2.  Il y a un affichage du **tableau de bord principal** car :

    *   Le fichier `MainActivity.java` contient le code de la classe `MainActivity` qui gère l'affichage du tableau de bord principal de l'application, **montrant un résumé des offres et des candidatures**.
    *   Le fichier `activity_main.xml` définit la structure de l'interface du tableau de bord.
    *   Les modèles `CompteEtudiant`, `Offre`, et `Candidature` sont utilisés pour afficher le résumé des informations.

---

3.  Il y a une **liste des offres** de stage car :

    *   Le fichier `ListOffresActivity.java` contient le code de la classe `ListOffresActivity` qui gère l'affichage de la liste des offres de stage disponibles.
    *   Le fichier `activity_list_offres.xml` décrit la structure de l'interface pour la liste des offres.
    *   Le modèle `Offre` est utilisé pour afficher la liste des offres de stage.

---

4.  Il y a un **affichage détaillé d'une offre de stage** car :

    *   Le fichier `OffreActivity.java` contient le code de la classe `OffreActivity` qui gère l'affichage détaillé d'une offre de stage spécifique.
    *   Le fichier `activity_offre.xml` définit la structure de l'interface pour les détails d'une offre.
    *   Les modèles `Offre`, `Entreprise`, et `Candidature` sont utilisés pour afficher les détails d'une offre et gérer la candidature.

---

5.  Il y a une **liste des candidatures** car :

    *   Le fichier `ListCandidaturesActivity.java` contient le code de la classe `ListCandidaturesActivity` qui gère l'affichage de la liste des candidatures de l'étudiant.
    *   Le fichier `activity_list_candidatures.xml` décrit la structure de l'interface pour la liste des candidatures.
    *   Le modèle `Candidature` est utilisé pour afficher la liste des candidatures de l'étudiant.

---

6.  Il y a un **affichage détaillé d'une candidature** car :

    *   Le fichier `CandidatureActivity.java` contient le code de la classe `CandidatureActivity` qui gère l'affichage détaillé d'une candidature spécifique.
    *   Le fichier `activity_candidature.xml` définit la structure de l'interface pour les détails d'une candidature.
    *   Les modèles `Candidature` et `Offre` sont utilisés pour afficher les détails d'une candidature.

---

7.  Il y a une **fonctionnalité d'édition d'une candidature** car :

    *   Le fichier `CandidatureEditActivity.java` contient le code de la classe `CandidatureEditActivity` qui gère l'interface et la logique pour modifier une candidature existante.
    *   Le fichier `activity_candidature_edit.xml` décrit la structure de l'interface d'édition de candidature.
    *   Les modèles `Candidature` et `CandidatureRequest` sont utilisés pour l'édition d'une candidature.

---

8.  Il y a une **gestion des données partagées et de l'API** car :

    *   Le fichier `StageAppActivity.java` contient le code de la classe `StageAppActivity`, une classe de base pour les autres activités, qui gère les fonctionnalités communes comme l'accès à l'API et aux préférences partagées.

---

9.  Il y a un **adaptateur pour la liste des candidatures** car :

    *   Le fichier `CandidatureAdapter.java` contient le code de la classe `CandidatureAdapter` qui gère la façon dont les candidatures sont affichées dans une liste.
    *   Le fichier `template_candidature.xml` définit la structure de chaque élément de la liste des candidatures.
    *   Le modèle `Candidature` est utilisé pour gérer l'affichage des éléments dans la liste des candidatures.

<div style="page-break-after: always;"></div>

## Diagrammes de classe
<figure> <img src="Pasted image 20250220195448.png" alt="Diagramme de classe" /> <figcaption>Figure 4 : Diagramme de classe de la partie client (1/2)</figcaption> </figure>

---

<figure> <img src="Pasted image 20250220195455.png" alt="Diagramme de classe" /> <figcaption>Figure 5 : Diagramme de classe de la partie client (2/2)</figcaption> </figure>



<div style="page-break-after: always;"></div>

 
# Schéma de la base de données

<figure> <img src="Pasted image 20250220203308.png" alt="Diagramme de la base de données" /> <figcaption>Figure 6 : Diagramme de la base de données</figcaption> </figure>

# Conclusion

Suite à cette phase de rétroconception, nous avons pu prendre en main le code de l’application que nous allons devoir améliorer, à l’aide de différents diagrammes et une cartographie précise des deux parties de l’application.
