La fonction principale est `int main(void)` ou bien `int main(int args, char *args[])` (pour la gestion d'arguments)

Une fonction se fait de la manière : `void procédure([..])`
Le passage en paramètres est dit par copie :
```C
void maFonction(int nombre){
	...
}
int main(void){
	int nombre = 1;
	maFonction(nombre);
}
```
Cela fait que la modification de `nombre` dans la fonction ne modifiera pas la variable `nombre` dans la boucle principale

On peut modifier cela avec les adressages et les [[Les pointeurs - C]]