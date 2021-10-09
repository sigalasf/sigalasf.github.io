# Les lambdas

Plusieurs exemples d'utilisation des lambdas :

## Quelques exemples d'utilisation

### Pour parcourir des listes

!!! example "Exemple"
	=== "Before Lambdas"
		```java linenums="1"
			for(Something s : list) {
				System.out.println(s.doSomething());
			}
		```
	===	"After Lambdas"
		```java linenums="1"
			list.forEach(Something::doSomething);
			// or
			list.forEach(element -> element.doSomething());
		```
	=== "Commentaire"
		La méthode forEach() dans l'interface Iterable attend en paramètre une interface fonctionnelle de type Consumer

### Pour les listeners

!!! example "Exemple"
	=== "Before Lambdas"
		```java linenums="1"
			button.addActionListener(new ActionListener() {
  				public void actionPerformed(ActionEvent event) {
    				doSomething(event);
  				}
			});
		```
	===	"After Lambdas"
		```java linenums="1"
			button.addActionListener(event -> doSomething(event));
		```
	=== "Commentaire"
		L'expression lambda  permet de définir une implémentation d'une interface fonctionnelle. Le type du paramètre n'est pas obligatoire : le compilateur va tenter de réaliser une inférence du type pour le déterminer selon le contexte.


### Pour les threads

!!! example "Exemple"
	=== "Before Lambdas"
		```java linenums="1"
			Thread thread = new Thread(new Runnable() {
  				@Override
  				public void run() {
    				doSomething();
  				}
			});
			thread.start();
		```
	===	"After Lambdas"
		```java linenums="1"
			Thread thread = new Thread(() -> { doSomething(); });
			thread.start();
		```
	=== "Commentaire"
		L'utilisation d'une expression lambda évite d'avoir à écrire le code nécessaire à la déclaration de la classe anonyme de type Runnable et de la méthode.

## Les interfaces fonctionnelles

Une interfacce fonctionnelle est une interface :

- Qui doit n'avoir qu'une seule méthode déclarée abstraite (les méthodes définies dans la classe Object ne sont pas prises en compte comme étant des méthodes abstraites)
- Dont toutes les méthodes doivent être public
- Qui peut avoir des méthodes par défaut et static

Certaines interfaces (avant Java 8) respèctent ses règles et sont donc des interfaces fonctionnelles, comme `Comparator<T>`, `Callable<T>`, `Runnable`, `ActionListener` ...
On peut donc utiliser une expression lambda au lieu d'une classe anonyme.

!!! example "Quelques exemples"
	```java linenums="1"
		// Le type du paramètre peut être précisé entre parenthèses
		Consumer<String> display = (String message) -> System.out.println(message);
		// Il est possible d'annoter les paramètres des expressions lambdas si le type est précisé
		Comparator<String> comparator = (@NotNull String chaine1, @NotNull String chaine2) -> Integer.compare(chaine1.length(),chaine2.length());
		// Si aucun paramètre n'est nécessaire, on utilise des parenthèses vides
		Runnable process = () -> System.out.println("processing");
		Function<Integer, Boolean> isEven = number -> { return (number%2 == 0); };
		BiFunction<Integer, Integer, Long> add = (x, y) -> (long) x + y;
		IntFunction intFunction  = x -> x * 2;
	```

Voici un exemple de définition d'une inteface fonctionnelle :

!!! example "Quelques exemples"
	=== "Operation.java"
		```java linenums="1"
			@FunctionalInterface
			public interface Operation {
				int calcul(int a, int b);
			}
		```
	=== "Main.java"
		```java linenums="1"
			public class Main {
				public static void main(String[] args) {
					System.out.println(execute(20, 10, (a,b) -> a + b)); // 30
					System.out.println(execute(20, 10, (a,b) -> a - b)); // 10
				}
				
				private static int execute(int a, int b, Operation operation) {
					return operation.calcul(a, b);
				}
			}
		```