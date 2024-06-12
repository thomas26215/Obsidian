```java
public class Main{
	public void main(String[] args){
		//Scanner
		private Scanner scanner = new Scanner(System.in);
		int i = scanner.nextInt();
		scanner.nextLine();

		String s = scanner.nextLine();

		
	}

"----------------"

    // Nombre entier aléatoire jusqu'à x (inclus)
    public static int randomIntUntil(int x) {
        Random random = new Random();
        return random.nextInt(x + 1);
    }

    // Nombre entier aléatoire entre x (inclus) et y (inclus)
    public static int randomIntBetween(int x, int y) {
        Random random = new Random();
        return x + random.nextInt(y - x + 1);
    }

    // Nombre à virgule flottante aléatoire jusqu'à x (exclus)
    public static double randomDoubleUntil(double x) {
        Random random = new Random();
        return random.nextDouble() * x;
    }

    // Nombre à virgule flottante aléatoire entre x (exclus) et y (exclus)
    public static double randomDoubleBetween(double x, double y) {
        Random random = new Random();
        return x + (y - x) * random.nextDouble();
    }

"---------------------------"

    // Fonction pour capitaliser la première lettre d'un mot
    public static String capitalizeFirstLetter(String word) {
        if (word == null || word.isEmpty()) {
            return word; // Retourner le mot tel quel s'il est null ou vide
        }

        // Convertir la première lettre en majuscule et les autres en minuscules
        return word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
    }
}

"-----------------------------"

public void askIntMin(int min){
	Scanner scanner = new Scanner(System.in);
	int number = min-1;
	do{
		System.out.println("Donnez un nombre supérieur à " + min);
		number = Scanner.nextInt();
		scanner.nextLine();
		if(number<min){
			System.out.println("Erreur : Vous devez donner un nombre supérieur à " + max + " !");
		}
	}while(number < min);
}



public void askIntMin(int max){
	Scanner scanner = new Scanner(System.in);
	int number = max+1;
	do{
		System.out.println("Donnez un nombre inférieur à " + max);
		number = Scanner.nextInt();
		scanner.nextLine();
		if(number>min){
			System.out.println("Erreur : Vous devez donner un nombre inférieur à " + min + " !");
		}
	}while(number > min);
}
```