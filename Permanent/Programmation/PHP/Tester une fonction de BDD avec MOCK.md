```php
public function testAddUserSuccess(){
	$userData = [ 'pseudo' => 'testuser', 'email' => 'test@example.com', 'mot_de_passe' => 'password123' ];
	$stmtMock = $this->createMock(PDOStatement::class);
	$stmtMock->expects($this->once()) // Simulation des requêtes
		->method('execute')
		->with($userData)
		->willReturn(true);
	$this->dbMock->expects($this->once()) // Configurer les attentes
		->method('prepare')
		->with("INSERT INTO utilisateurs (pseudo, email, mot_de_passe) VALUES(:pseudo, :email, :mot_de_passe)")
		->willReturn($stmtMock);
	$result = $this->userBase->addUser($userData); // Exécution du code à tester
	$this->assertTrue($result); // Vérifications
}
```

Une fois que j'ai configuré le [[Mise en place d'un MOCK pour BDD|MOCK sur ma BDD]], il faut que je fasse le teste sur ma BDD :
1. Configurer les attentes
	- Pour chaque test, on configure le comportement attendu du mock PDO
	- On définit quelles méthodes seront appelées (comme `prepare`), avec quels arguments (en utilisant `with`) et avec ce qu'elles doivent retourner (`willReturn`)
2. Simulation des requêtes
	- Des mocks de PDOStatement sont crées pour simuler des requêtes préparées
	- Il faut configurer ces mocks pour qu'ils répondent de manière spécifique (succès, échec, lancement d'exéption) lors de l'exécution
3. Exécution du code à tester
	- On appelle les méthodes qu'on veut tester (`addUser`, `addProfil` ...)
	- Grâce à la méthode [[Mise en place d'un MOCK pour BDD#^important|setPrivateProperty]], nous savons que les méthodes interagissent avec un mock au lieu d'une vraie BDD
4. Vérifications
	- Il faut maintenant vérifier que les méthodes retournent les résultats attendus (bon nombre de fois, avec les bons arguments)


Le principe étant que les attentes que l'on définit, comme par exemple `expect($sthis->once())` sont vérifiées uniquement durant l'exécution du test. Quand le test est terminé, les attentes ne persistent pas et ne sont pas conservées par d'autres tests.
A la fin de l'exécution du test, PHPUnit vérifie si les attentes ont été satisfaites à la fin de l'exécution du test. Si la méthode simulée a été appelée le bon nombre de fois, le test réussit, sinon non

---
```php
$this->dbMock->expects($this->once()) ->method('prepare') ->with("INSERT INTO utilisateurs (pseudo, email, mot_de_passe) VALUES(:pseudo, :email, :mot_de_passe)");
```

