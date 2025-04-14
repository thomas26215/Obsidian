1. Il y a une fonctionnalité d'authentification de l'utilisateur car :
    
    - Le fichier `LoginActivity.java` contient le code de la classe `LoginActivity` qui gère l'interface et la logique d'authentification de l'utilisateur.
        
    - Le fichier `activity_login.xml` décrit la structure de l'interface de connexion.
        
    - Le modèle `Auth` est utilisé pour l'authentification.
        
2. Il y a un affichage du tableau de bord principal car :
    
    - Le fichier `MainActivity.java` contient le code de la classe `MainActivity` qui gère l'affichage du tableau de bord principal de l'application, montrant un résumé des offres et des candidatures.
        
    - Le fichier `activity_main.xml` définit la structure de l'interface du tableau de bord.
        
    - Les modèles `CompteEtudiant`, `Offre`, et `Candidature` sont utilisés pour afficher le résumé des informations.
        
3. Il y a une liste des offres de stage car :
    
    - Le fichier `ListOffresActivity.java` contient le code de la classe `ListOffresActivity` qui gère l'affichage de la liste des offres de stage disponibles.
        
    - Le fichier `activity_list_offres.xml` décrit la structure de l'interface pour la liste des offres.
        
    - Le modèle `Offre` est utilisé pour afficher la liste des offres de stage.
        
4. Il y a un affichage détaillé d'une offre de stage car :
    
    - Le fichier `OffreActivity.java` contient le code de la classe `OffreActivity` qui gère l'affichage détaillé d'une offre de stage spécifique.
        
    - Le fichier `activity_offre.xml` définit la structure de l'interface pour les détails d'une offre.
        
    - Les modèles `Offre`, `Entreprise`, et `Candidature` sont utilisés pour afficher les détails d'une offre et gérer la candidature.
        
5. Il y a une liste des candidatures car :
    
    - Le fichier `ListCandidaturesActivity.java` contient le code de la classe `ListCandidaturesActivity` qui gère l'affichage de la liste des candidatures de l'étudiant.
        
    - Le fichier `activity_list_candidatures.xml` décrit la structure de l'interface pour la liste des candidatures.
        
    - Le modèle `Candidature` est utilisé pour afficher la liste des candidatures de l'étudiant.
        
6. Il y a un affichage détaillé d'une candidature car :
    
    - Le fichier `CandidatureActivity.java` contient le code de la classe `CandidatureActivity` qui gère l'affichage détaillé d'une candidature spécifique.
        
    - Le fichier `activity_candidature.xml` définit la structure de l'interface pour les détails d'une candidature.
        
    - Les modèles `Candidature` et `Offre` sont utilisés pour afficher les détails d'une candidature.
        
7. Il y a une fonctionnalité d'édition d'une candidature car :
    
    - Le fichier `CandidatureEditActivity.java` contient le code de la classe `CandidatureEditActivity` qui gère l'interface et la logique pour modifier une candidature existante.
        
    - Le fichier `activity_candidature_edit.xml` décrit la structure de l'interface d'édition de candidature.
        
    - Les modèles `Candidature` et `CandidatureRequest` sont utilisés pour l'édition d'une candidature.
        
8. Il y a une gestion des données partagées et de l'API car :
    
    - Le fichier `StageAppActivity.java` contient le code de la classe `StageAppActivity`, une classe de base pour les autres activités, qui gère les fonctionnalités communes comme l'accès à l'API et aux préférences partagées.
        
9. Il y a un adaptateur pour la liste des candidatures car :
    
    - Le fichier `CandidatureAdapter.java` contient le code de la classe `CandidatureAdapter` qui gère la façon dont les candidatures sont affichées dans une liste.
        
    - Le fichier `template_candidature.xml` définit la structure de chaque élément de la liste des candidatures.
        
    - Le modèle `Candidature` est utilisé pour gérer l'affichage des éléments dans la liste des candidatures.