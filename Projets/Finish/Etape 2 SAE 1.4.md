VENOUIL Thomas
ROGER Joshua
A2

1. Dans PORT :
	- PortName et Country proviennent de l'application de la règle **R0** à l'entité PORT PortId est clé primaire parce qu'il représente l'identifiant de cette entité
2. Dans PASSENGER
	- Name, Sex, Age et Survived proviennent de l'application de la règle **R0** à l'entité PASSENGER et PassengerID est clé primaire parce qu'il représente l'identifiant de cette entité
	- PClass et PortID proviennent de l'application de la règle **R1**
	- PClass est hérité par Class car c'est un identifiant seul dans l'entité
	- PortID est clé étrangère en tant qu'identifienté de PORT
3. OCCUPATION
	- PassengerID et CabinCode proviennent de l'application de la règle **R3** aux entités CABIN et PASSENGER
	- PassengerID est clé primaire et clé étrangère en tant qu'identifienté de PASSENGER
	- CabinCode est clé primaire et clé étrangère en tant qu'identifienté de CABIN
4. SERVICE
	- PassengerId_Dom, PassengerId_Emp et rôle proviennent de l'application de la règle **R2** à l'entité PASSENGER (Les deux branches pointent vers cette même entité)
	- Passenger_Dom est clé primaire et clé étrangère en tant qu'identifienté à la clé primaire PassengerId de l'entité PASSENGER
	- Passenger_Emp est clé étrangère en tant qu'identifié à la clé primaire PassengerId de l'entité PASSENGER
5. CATEGORY
	- Structure et Places proviennent de l'application de la règle **R0** à l'entité CATEGORY et  LifeBoatCat est clé primaire  parce qu'il représente l'identifiant de cette entité
6. LIFEBOAT
	- Side, Position et Location proviennent de l'application de la règle **R0** à l'entité LIFEBOAT et LifeBoatId est clé primaire parce qu'il présente l'identifiant de cette entité
	- LifeBoatCat et Time proviennent de l'application de la règle **R1**
	- Time est hérité par OBSERVED_TIME car c'est un identifiant seul dans la l'entité
	- LifeBoatCat est clé étrangère en tant qu'identifié de CATEGORY
7. RECOVERY
	- LifeBoatId et RecoveryTime proviennent de l'application de la règle **R2**
	- LifeBoatId est clé primaire et clé étrangère en tant qu'identifié de CATEGORY
	- RecoveryTime est hérité par Time de l'entité OBSERVED_TIME car c'est un identifiant seul de l'entité
8. RESCUE
	- PassengerId et LifeBoatId proviennent de l'application de la règle **R2**
	- PassengerId est clé primaire et étrangère en tant qu'identifiant de PASSENGER
	- LideBoatId est clé étrangère en tant qu'identifiant de LIFEBOAT