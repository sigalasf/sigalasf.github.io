# Les variables et fonctions

## Les types primitifs

|  Type primitif     | Taille en mémoire (en bits)   | Intervalle  | Valeur par défaut  |
| ------------       |        -------------          | ------------|       ------------|
| char | 16 |  $[Unicode~{0} ; Unicode~2^{16} - 1]$            | '\u0000'|
| byte | 8   |  $[-127 ; 127]$             | $0$|
| short | 16 |  $[-2^{15} ; 2^{15} - 1]$             | $0$|
| int | 32 |  $[-2^{31} ; 2^{31} -1]$             | $0$ |
| long | 64  |  $[-2^{63} ; 2^{63} - 1]$             | $0L$ |
| float | 32 |  $32~bits~IEEE~754~floating~point~numbers$             |$0.0f$ |
| double | 64  |  $64~bits~IEEE~754~floating~point~numbers$            | $0.0d$|
| boolean | 1 | $\{true;false\}$            | $false$ |

Les **valeurs par défaut ne s'appliquent qu'aux attributs d'une classe**, pas aux variables locales.

### Déclaration des types primitifs

!!! example "Exemple"
	=== "Code"
		```java linenums="1"
			int i;
		```
	=== "Commentaire"
		A l'éxecution, un espace mémoire de 32 bits est reservé par la JVM permettant de stocker un entier.

	Cela peut être représenté par le schéma suivant en mémoire (Le losange indique un nom de variable, le rectangle violet désigne une case mémoire) :

	```mermaid
		flowchart LR
	    ?:::ppl <--> I{i}
	    classDef ppl fill:purple;
	```

### Affectation des types primitifs

L'affectation des types primitifs fonctionne par **valeur**.

!!! example "Exemple"
	=== "Code"
		```java linenums="1"
			int i = 1;
			int j = i;
			i = 2;
			System.out.println(i); // Affiche '2'
			System.out.println(j); // Affiche '1'
		```
	=== "Commentaire"
		Après l'exécution de ce code, **il n'y a plus aucun lien entre i et j**.

	Cela peut être représenté par le schéma suivant en mémoire :

	```mermaid
		flowchart LR
	    2:::ppl <--> I{i}
	    1:::ppl <--> J{j}
	    classDef ppl fill:purple;
	```

	!!! warning "Attention"
	    En Java, les tableaux sont des objets, que ce soit des tableaux de type primitifs ou d'objets.
	    Ainsi, le code suivant :
	    ```java linenums="1"
	    	int arr[] = {1,2,3};
	    ```
	    Est simplement un raccourci pour :
	    ```java linenums="1"
	    	int arr[] = new int[3];
	    	arr[0] = 1;
	    	arr[1] = 2;
	    	arr[2] = 3;
	    ```
	    On reviendra donc sur les tableaux dans la partie dédiée aux objets.