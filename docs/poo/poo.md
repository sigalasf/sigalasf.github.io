# Les principes de la POO

## Les classes

Comme dit dans l'introduction, la programmation orientée objet consiste à créer des briques logicielles appelées *objets*.

Un objet est matérialisé par une ou plusieurs classes, qui peuvent être facilement réutilisées et modifiables. En fait, on dit qu'*un objet est une instance d'une classe*.

Une classe est constituée à minima :

- De variables, appelées **attributs** qui décrivent comment est modélisé l'objet.
- De fonctions, appelées **méthodes** qui permettent d'effectuer des actions sur l'objet.

Une classe peut également posséder :

- Des **mutateurs** (**getters** et **setters**) qui permettent de récupérer ou modifier les valeurs des attributs.
- Une ou plusieurs fonctions particulières, appelées **constructeurs**, qui permettent d'instancier (créer) un objet en lui allouant la mémoire nécessaire et en y initialisant ses attributs.

Exemple :

=== "Java"

	=== "Utilisateur.java"
	    ``` java
	    public class Utilisateur {
	    	// Attributs
	    	private int id;
	    	private int age;
	    	private String name;
	    	private String emailAddress;

	    	// Constructeur par défaut
	    	public Utilisateur() {

	    	}

	    	// Constructeur avec paramètres
	    	public Utilisateur(int id, int age, String name, String emailAddress){
	    		this.id = id;
	    		this.age = age;
	    		this.name = name;
	    		this.emailAddress = emailAddress;
	    	}

	    	// Setters
	    	public void setIdentifiant(int identifiant){
	    		this.identifiant = identifiant;
	    	}

	    	public void setAge(int age){
	    		this.age = age;
	    	}

	    	public void setName(String name){
	    		this.name = name;
	    	}

	    	public void setEmailAddress(String emailAddress){
	    		this.emailAddress = emailAddress;
	    	}

	    	// Getters
	    	public int getIdentifiant(){
	    		return this.identifiant;
	    	}

	    	public int getAge(){
	    		return this.age;
	    	}

	    	public String getName(){
	    		return this.name;
	    	}

	    	public String getEmailAddress(){
	    		return this.emailAddress;
	    	}

	    	// Exemple d'une méthode
	    	public boolean isAdult() {
	    		return (this.age >= 18);
	    	}
	    }
	    ```
	=== "Main.java"
		``` java
		public class Main {

			public static void main(String[] args) {
				// Création d'une instance d'un utilisateur
				Utilisateur utilisateur = new Utilisateur(0, 17, "Marc", "marc.email@domain.com");
				utilisateur.isAdult(); // Renvoie false
			}
		}
		```

=== "C++"

	=== "Utilisateur.h"
		``` c++
		#ifndef UTILISATEUR_H
		#define UTILISATEUR_H

		#include <string.h>
		using namespace std;

		class Utilisateur {
			private:
				// Attributs
				int identifiant;
				int age;
				string name;
				string emailAddress;
			public :
				// Constructeur par défaut
				Utilisateur();
				// Constructeur avec paramètres
				Utilisateur(int identifiant, int age, string name, string emailAddress);

				// Setters
				void setIdentifiant(int identifiant);
				void setAge(int age);
				void setName(string name);
				void setEmailAddress(string emailAddress);

				// Getters
				int getIdentifiant();
				int getAge();
				string getName();
				string getEmailAddress;

				// Example d'une méthode
				bool isAdult();

		};
	    #endif
	    ```


	=== "Utilisateur.cpp"
	    
	    ``` c++
	    #include "Utilisateur.h"
	    #include <string>
	    using namespace std;

	    // Implémentation du constructeur par défaut
	    Utilisateur::Utilisateur() : {

	    }

	    // Implémentation du constructeur avec paramètres
	    Utilisateur::Utilisateur(int identifiant, int age, string name, string emailAddress) : {
	    	this->identifiant = identifiant;
	    	this->age = age;
	    	this->name = name;
	    	this.emailAddress = emailAddress;
	    }

	    // Implémentation des setters
	    void Utilisateur::setIdentifiant(int identifiant){
	    	this->identifiant = identifiant;
	    }

	    void Utilisateur:setAge(int age){
	    	this->age = age;
	    }

	    void Utilisateur::setName(string name){
	    	this->name = name;
	    }

	    void Utilisateur::setEmailAddress(string emailAddress){
	    	this->emailAddress=emailAddress;
	    }

	    // Implémentation des getters
	    int Utilisateur::getIdentifiant(){
	    	return this->identifiant;
	    }

	    int Utilisateur::getAge(){
	    	return this->age;
	    }

	    string Utilisateur::getName(){
	    	return this->name;
	    }

	    string Utilisateur::getEmailAddress(){
	    	return this->emailAddress;
	    }

	    // Implémentation des méthodes
	    bool Utilisateur::isAdult(){
	    	return (this->age >= 18);
	    }
	    ```


	=== "Main.cpp"
		``` c++
			#include <string> 
			using namespace std;
			#include "Utilisateur.h"

			int main() 
			{ 
			    Utilisateur *utilisateur = new Utilisateur(0, 17, "Marc", "marc.email@domain.com");
			    utilisateur->isAdult() // Renvoie false
			    delete utilisateur;
			    return 0;
			}
		```

L'exemple ci-dessus représente un utilisateur qui possède comme **attributs** :

- Un identifiant (nombre entier)
- Un âge (nombre entier)
- Un nom (chaîne de caractères)
- Une addresse email (chaîne de caractères)

Pour instancier un utilisateur, on utilise l'un des deux **constructeurs** :

- Par défaut (Ici, le constructeur par défaut n'initialise pas les valeurs. En Java, le compiler va initialiser par défaut les int à 0 et les String à null. Même chose en C++).
- Avec paramètres : Le mot clé `this` permet de faire référence à l'objet en cours pour initialiser ses valeurs.

Notre classe Utilisateur possède également une **méthode** *isAdult* qui retourne un booléen.

Que ce soit en C++ ou en Java, vous l'aurez remarqué, la présence de mots clés comme *public* ou *private* : Cela nous mène donc à un autre concept important d'un langage orienté objet : **L'encapsulation des données**

## L'encapsulation des données

L'encapsulation est un mécanisme consistant à rassembler les attributs et les méthodes au sein d'une structure en limitant par défaut le champ d'action de ces attributs et méthodes à l'objet lui-même et non à tout autre objet.

L'encapsulation permet de définir des niveaux de visibilité des éléments de la classe. Ces niveaux de visibilité définissent les droits d'accès aux données selon que l'on y accède par une méthode de la classe elle-même, d'une classe héritère, ou bien d'une classe quelconque.

Il existe trois niveaux de visibilité :

- **Publique** : Un membre (attribut, méthode ...) publique sera accessible de n'importe où dans le programme. La classe a donc accès à ce membre, mais aussi n'importe quelle autre classe.

- **Privé** : Seul la classe ayant définit le membre privé pourra y accéder.

- **Protégé** : Un membre protégé peut être manipulé :
	- Dans la classe qui définit ce membre
	- Dans les classes qui [héritent](#heritage) de la classe considérée
	- Particularité pour Java : Dans les classes et les types définies dans le même package que celle qui définit le membre protégé (On ne retrouve pas cette notion en C++ avec la notion de namespaces)

## Héritage

L'héritage est un autre principe de la programmation orientée objet, permettant de créer une nouvelle classe à partir d'une classe existante. La classe héritée a alors accès aux membres publiques et protégés de sa superclasse (classe dont elle dérive).

L'héritage peut être traduit en français par "*est une sorte de*".

Par exemple, on peut dire qu'une voiture est une sorte de véhicule. On peut donc imaginer une classe Véhicule, et une classe Voiture qui hérite de la classe Véhicule :

=== "Java"

	=== "Vehicule.java"
	    ``` java
	    public class Vehicule {
	    	// Attributs
	    	private float vitesse;
	    	private int nombreDePlaces;

	    	// Constructeur par défaut
	    	public Vehicule() {
	    		super();
	    	}

	    	// Constructeur avec paramètres
	    	public Vehicule(float vitesse, int nombreDePlace){
	    		this.vitesse = vitesse;
	    		this.nombreDePlace = nombreDePlace;
	    	}

	    	// Setters
	    	public void setVitesse(float vitesse){
	    		this.vitesse = vitesse;
	    	}

	    	public void setNombreDePlace(int nombreDePlace){
	    		this.nombreDePlace = nombreDePlace;
	    	}

	    	// Getters
	    	public float getVitesse(){
	    		return this.vitesse;
	    	}

	    	public int getNombreDePlace(){
	    		return this.nombreDePlace;
	    	}

	    	// Méthodes
	    	protected boolean nombreDePlaceEstPair(){
	    		return (this.nombreDePlace % 2 == 0);
	    	}

	    	private boolean vitesseEstNulle() {
	    		return (this.vitesse == 0.0f);
	    	}

	    }
	    ```

	=== "Voiture.java"
		``` java
		// La classe Voiture hérite de la classe Vehicule : mot clé extends
	    public class Voiture extends Vehicule {
	    	// Attributs
	    	private String marque;
	    	private String typeMoteur;

	    	// Constructeur par défaut
	    	public Voiture() {
	    		// Ici, super() fait appel au constructeur par défaut de la classe Vehicule
	    		super();
	    	}

	    	// Constructeur avec paramètres
	    	public Voiture(int vitesse, int nombreDePlace, String marque, String typeMoteur){
	    		// Ici, super(...) fait appel au constructeur avec paramètres de la classe Véhicule
	    		super(vitesse, nombreDePlace);
	    		this.marque = marque;
	    		this.typeMoteur = typeMoteur;
	    	}

	    	// Setters
	    	public void setMarque(float marque){
	    		this.marque = marque;
	    	}

	    	public void setTypeMoteur(int typeMoteur){
	    		this.typeMoteur = typeMoteur;
	    	}

	    	// Getters
	    	public float getMarque(){
	    		return this.marque;
	    	}

	    	public int getTypeMoteur(){
	    		return this.typeMoteur;
	    	}

	    	/* 
	    	Méthodes : @Override permet de signaler qu'il s'agit d'une méthode de la classe mère qu'on surcharge.
	    	On peut également noter que dans la classe mère, la méthode est protégée, et elle devient publique ici.
	    	Il s'agit d'une particularité de l'encapsulation : On peut modifier la visibilité si celle-ci devient moins restrictive.
	    	On aurait donc pas pu définir la méthode comme étant privé içi par exemple.
	    	*/
	    	@Override
	    	public boolean nombreDePlaceEstPair() {

	    		return (super.getNombreDePlace() % 2 == 0 ? true : false);
	    	}

	    }
	    ```

	=== "Main.java"
		``` java
		public class Main {

			public static void main(String[] args) {
				Voiture voiture1 = new Voiture(70, 4, "BMW", "Essence");
				// Une voiture est une sorte de véhicule, on peut donc créer un Objet Vehicule qui est une instance de Voiture.
				Vehicule voiture2 = new Voiture();
			}
		}
		```

=== "C++"

On peut noter la présence du mot clé : **super**, parfois **super()**.

- **super** permet de faire référence à l'objet parent. Ainsi, `super.getNombreDePlace()` permet de récupérer le nombre de place du parent.
- **super()** permet de faire appel au constructeur par défaut de l'objet parent. Ainsi, le `super()` du constructeur par défaut de Voiture va faire appel au constructeur par défaut de Véhicule. On peut cependant noter la présence de `super()` dans le constructeur par défaut de Vehicule en Java, pourtant cette classe n'hérite d'aucune classe ! Et bien... si ! En Java, toutes les classes créées héritent d'une classe nommé **Object** ! On peut également faire appel à des constructeurs avec paramètres en les rajoutant dans `super(...)`.