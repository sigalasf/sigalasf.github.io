# Les références


## Exemple de classe pour la suite

!!! example "User.java"
	```java linenums="1"
		public class User {
			private int age;
			private int id;

			public User() {
				super();
				// age & id = 0 by default
			}

			public User(int age, int id) {
				super();
				this.age = age;
				this.id = id;
			}

			// getters and setters
		}
	```

Supposons maintenant ces extraits de code : 

!!! example "Exemple 1"
	=== "Code"
		```java linenums="1"
			User user;
		```
	=== "Commentaire"
		Aucune instance de la classe User est créée ici, et l'espace mémoire nécessaire à stocker un User n'est pas resérvé. En réalité, la variable `user` est une référence. Ce code va donc allouer la mémoire nécessaire pour stocker une référence.

	Cela peut être représenté par le schéma suivant en mémoire (Le losange indique un nom de variable, le rectangle violet désigne une case mémoire):

	```mermaid
		flowchart LR
	    ?:::ppl <--> User{user}
	    classDef ppl fill:purple;
	```

!!! example "Exemple 2"
	=== "Code"
		```java linenums="1"
			new User();
		```
	=== "Commentaire"
		Cette fois, un espace mémoire est alloué permettant de stocker un objet User.

	On a donc quelque chose qui ressemble à ça :

	```mermaid
		flowchart LR
	    OBJ(age=0\n id=0):::grn
	    classDef grn fill:green;
	```

!!! example "Exemple 3"
	=== "Code"
		```java linenums="1"
			User user = new User();
		```
	=== "Commentaire"
		Ici, on déclare d'abord la référence avec `User user` puis on créé ensuite l'objet grâce à l'opérateur `new User()`. Vient ensuite l'**affectation** grâce au `=` : La référence stockée dans l'espace mémoire reservé lors de la déclaration de `user` prend la valeur de l'address mémoire de l'objet créé.

	Cela peut être représenté par le schéma suivant en mémoire:

	```mermaid
		flowchart LR
		MEM[ ]:::ppl <--> User{user}
		OBJ(age=0\n id=0):::grn --- MEM
	    classDef ppl fill:purple;
	    classDef grn fill:green;
	```

!!! example "Exemple 4"
	=== "Code"
		```java linenums="1"
			User user1 = new User(20,1000);
			User user2 = user1;
		```
	=== "Commentaire"
		Ici, on créé une instance de User avec `User user1 = new User(20,1000)`, référencé par la variable `user1`. Comme vu précédemment, l'instruction `User user2` va déclarer une variable `user2` : Aucun utilisateur n'est créé, on reserve juste un espace mémoire pour une référence. Lors de `user2 = user1`, la **valeur** de la référence de `user1` est recopiée dans l'espace mémoire correspondant à `user2` : `user2` référence donc l'objet qui était référencé par `user1`.

	Cela peut être représenté par le schéma suivant en mémoire:

	```mermaid
		flowchart LR
		MEM1[ ]:::ppl <--> User{user1}
		MEM2[ ]:::ppl <--> User2{user2}
		OBJ(age=20\n id=1000):::grn --- MEM1
		OBJ:::grn --- MEM2
	    classDef ppl fill:purple;
	    classDef grn fill:green;
	```

!!! example "Exemple 5"
	=== "Code"
		```java linenums="1"
			User user1 = new User(20,1000);
			User user2 = new User();
			user2 = user1;
		```
	=== "Commentaire"
		Ici, aux lignes 1 et 2, on créé deux objets référencés par les variables `user1` et `user2`. A la ligne 3, on recopie l’adresse de l’objet référtencé par `user1` dans l’espace mémoire aloué à `user2`, ce qui revient à dire que `user2` référence maintenant le même objet que `user1` :


	Cela peut être représenté par le schéma suivant en mémoire:

	```mermaid
		flowchart LR
		MEM1[ ]:::ppl <--> User{user1}
		MEM2[ ]:::ppl <--> User2{user2}
		OBJ1(age=20\n id=1000):::grn --- MEM1
		OBJ2(age=0\n id=0):::grn
		OBJ1:::grn --- MEM2
	    classDef ppl fill:purple;
	    classDef grn fill:green;
	```

	Plus aucune variable ne désigne le second objet en mémoire. Il occupe donc une place inutile en mémoire. Il sera détruit par le garbage collector dont le but est justement de supprimer en mémoire les objets qui ne sont plus référencés.