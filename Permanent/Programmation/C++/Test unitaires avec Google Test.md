[[Les tests]]
[[Le principe des tests]]
[[Les bonnes pratiques des tests]]


Les assertions sont des macros
La plupart des assertions ont deux formes :
- `EXPECT_TRUE(une condition)` : teste si la condition est vraie et poursuit la cas de test courant même si elle ne l'est pas (non fatil failure)
- `ASSERT_TRUE(une condition)` : teste si la fonction est vraie et interrompt le cas de test courant si elle ne l'est pas (fatal failure)

On peut produire un message d'informations en cas d'échec : 
`EXPECT_TRUE(uneCondition) << "uneCondition n'est pas vraie mais devrait l'être`

- Assertions Booléennes
	- `EXPECT_TRUE(condition)`
	- `EXPECT_FALSE(condition)`
- Assertions Comparaisons binaires [[Définition - Notion de condition]]
	- `EXPECT_EQ(val1, val2)`
	- `EXPECT_NE(val1, val2)`
	- `EXPECT_LT(val1, val2)`
	- `EXPECT_LE(val1, val2)`
	- `EXPECT_GT(val1, val2)`
	- `EXPECT_GE(val1, val2)`
- Asssertions Exceptions
	- `EXPECT_THROW(inst, type_except)`
	- `ASSERT_THROW(inst, type_except)`
	- `EXPECT_ANY_THROWN(inst)`
	- `ASSERT_ANY_THROWN(inst)`
	- `EXPECT_NO_THROW(inst)`
	- `ASSERT_NO_THROW(inst)`

[[Configurer GTest pour VS Code]]
[[Structure du code d'un test JUnit5]]

