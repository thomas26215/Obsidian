## Tables principales
```SQL
Compte_Etudiant {
  etudiant_id integer [primary key]
  login varchar(180) [unique]
}

Ref: Compte_Etudiant.etudiant_id > Etudiant.id
Ref: Compte_Etudiant.login > Login.login

Login {
  login varchar(180) [primary key]
  password varchar(255)
  parcours varchar(1)
  roles json
  derniere_connexion timestamp
  etat_recherche_id integer
}

Ref: Login.etat_recherche_id > Etat_Recherche.id

Etat_Recherche {
  etat varchar(255) [primary key]
  descriptif text
}

Etudiant {
  numero_ine varchar(11) [primary key]
  nom varchar(255)
  prenom varchar(255)
  email varchar(255)
}

Entreprise {
  raison_sociale varchar(255) [primary key]
  ville varchar(255)
}

Ref: Entreprise.ville > Ville.nom

Ville {
  nom varchar(255) [primary key]
  pays varchar(255)
}

Offre {
  intitule varchar(255)
  date_depot date
  entreprise_raison_sociale varchar(255)
  etat_offre_id integer
  descriptif text
  parcours varchar(1)
  mots_cles varchar(255)
  url_piece_jointe varchar(2000)
  [primary key: intitule, date_depot, entreprise_raison_sociale]
}

Ref: Offre.entreprise_raison_sociale > Entreprise.raison_sociale
Ref: Offre.etat_offre_id > Etat_Offre.id

Etat_Offre {
  etat varchar(255) [primary key]
  descriptif text
}
```
## Tables de liaison
```SQL
Candidature {
  compte_etudiant_id integer
  offre_intitule varchar(255)
  offre_date_depot date
  offre_entreprise varchar(255)
  etat_candidature_id integer
  type_action varchar(255)
  date_action timestamp
  [primary key: compte_etudiant_id, offre_intitule, offre_date_depot, offre_entreprise]
}

Ref: Candidature.etat_candidature_id > Etat_Candidature.id

Etat_Candidature {
  id integer [primary key]
  etat varchar(255)
  descriptif text
}

Offre_Consultee {
  compte_etudiant_id integer
  offre_intitule varchar(255)
  offre_date_depot date
  offre_entreprise varchar(255)
  [primary key: compte_etudiant_id, offre_intitule, offre_date_depot, offre_entreprise]
}

Offre_Retenue {
  compte_etudiant_id integer
  offre_intitule varchar(255)
  offre_date_depot date
  offre_entreprise varchar(255)
  [primary key: compte_etudiant_id, offre_intitule, offre_date_depot, offre_entreprise]
}
```
## Autres tables techniques

```SQL
Doctrine_Migration_Versions {
  version varchar(191) [primary key]
  executed_at timestamp
  execution_time integer
}

Messenger_Messages {
  id bigint [primary key]
  body text
  headers text
  queue_name varchar(190)
  created_at timestamp
  available_at timestamp
  delivered_at timestamp
}
```