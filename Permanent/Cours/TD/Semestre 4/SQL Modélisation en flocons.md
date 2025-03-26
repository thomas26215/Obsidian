# Exercice 1
Il existe les DF suivants :
- `trancheAge -> ageMin, ageMax`
- `nomDiplome -> niveauEtudes`
- `Mois -> semestre`

```mermaid
classDiagram
	class Entrainement {
		idEntraineur
		idTemps
		idTerrain
		idCoureur
		idCategorie
		distance
		chrono
		obstacle
	}
	class Entraineur {
		idEntraineur
		nom
		prenom
		domaine
		idDiplome
	}
	class Terrain {
		idTerrain
		surface
		adresse
	}
	class Temps {
		idTemps
		jour
		idSemestreDannee
		idMoisDannee
	}
	class Coureur {
		idCoureur
		nom
		prenom
		dateNaissance
	}
	class Diplome {
		idDiplome
		nomDiplome
		niveauEtudes
	}
	class MoisDannee {
		idMoisDannee
		libelleMois
		idSemestreDAnnee
	}
	class SemestreDannee {
		idSemestreDannee
		semestre
		annee
	}
	class SemaineDannee {
		idSemaine
		numeroSemaine
		isAnnee
	}
	class Annee {
		annee
	}
	class ResultatCourse {
		idCoureur
		idTemps
		idCategorie
		classement
		chrono
	}
	class Categorie {
		idCategorie
		niveau
		idTrancheAge
	}
	class TrancheAge {
		idTranche
		libelle
		ageMin
		ageMax
	}
	
	Entraineur-->Diplome
	Entrainement-->Entraineur
	Entrainement-->Terrain
	Entrainement-->Temps
	Entrainement-->Categorie
	MoisDannee-->SemestreDannee
	SemestreDannee-->Annee
	Temps-->MoisDannee
	Temps-->SemaineDannee
	SemaineDannee-->Annee
	ResultatCourse-->Temps
	ResultatCourse-->Coureur
	ResultatCourse-->Categorie
	Categorie-->TrancheAge
```

# Exercice 2
**Question 1**

|                                  | Bac d'origine | Age | Mineur | Groupe | Semestre | Annee | Horaire | UE  | Type épreuve |
| -------------------------------- | ------------- | --- | ------ | ------ | -------- | ----- | ------- | --- | ------------ |
| Pourcentage d'absent             | X             | X   | X      |        |          |       |         |     |              |
| Nombre étudiant absents          |               |     |        | X      | X        | X     |         |     |              |
| Nombre absents                   |               |     |        |        |          |       | X       |     |              |
| Pourcentage absents              |               |     |        |        |          |       |         | X   | X            |
| Note moyenne / Mediane / Min max |               |     |        | X      | X        | X     |         | X   |              |
