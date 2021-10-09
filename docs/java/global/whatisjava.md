## Qu'est-ce que Java ?

> **Java** est un langage de programmation, initialement développé par Sun Microsystems puis acquis par Oracle à la suite du rachat de l'entreprise en 2009. Plus d'information sur le [site d'Oracle](https://www.oracle.com/fr/java/).

La technologie Java regroupe :

- Des standards (la plate-forme Java) définis sous forme de spécification par le [JCP (Java Community Process)](https://www.jcp.org/) :
	- **Java SE (Java Standard Edition) :** Contient toutes les bibliothéques et API Java de base tel que `java.lang`, `java.io`, `java.net`, `java.util` ...
	- **Java EE (Java Entreprise Edition) :** En plus des bibliothèques de base, ajoute des bibliothèques pour déployer du Java multi-niveaux, basé sur des composants fonctionnant sur un serveur d'application. Java EE est donc utile pour déployer des applications web d'entreprise.
	- **Java ME (Java Micro Edition) :** Est utilisé dans le développement d'applications mobiles et dans les systèmes embarqués.
- Des logiciels dont des implémentations de ces spécifications
- Des communautés d'entreprises, organisations à but non lucratif, pouvant posséder des parties des marques, brevets et parts de marché liés à la technologie Java.

## Notions de JDK, JVE et JVM

### Le JDK

Le **JDK (Java Development Kit)** est un environnement de développement logiciel utilisé pour développer des applications et des applets Java. Il comprend le **JRE (Java Runtime Environment)**, un interpréteur Java, un compilateur (javac), un archiveur (jar), un générateur de documentation (javadoc) et d'autres outils nécessaires au développement Java.

### Le JRE

Le **JRE (Java Runtime Environment)** fournit des exigences minimales pour l'exécution d'une application Java. Il comprend la **JVM (Java Virtual Machine)**, des classes principales et des fichiers de soutien.

### La JVM

La **JVM (Java Virtual Machine)** agit comme un moteur d'éxecution pour exécuter les applications Java. C'est elle qui appelle la méthode principale présente dans un code Java.

Les applications Java sont appelées WORA (Write Once Run Anywhere). Cela signifie qu'un programmeur peut développer un code Java sur un système et s'attendre à ce qu'il fonctionne sur n'importe quel autre système compatible Java sans aucun ajustement. Tout ceci est possible grâce à la JVM.

Pour mieux comprendre, il faut s'attarder sur la compilation en Java.

## Compilation Java

Lorsqu'on développe en Java, le code est écrit dans des fichiers source *.java*.

Lorsqu'un fichier .java est compilé grâce à *javac* par exemple, un fichier .class contenant du code d'octets (aussi appelé bytecode) est créé.

Afin que le bytecode soit reconue par l'OS, celui-ci passe par différentes étapes lorsque nous l'exécutons. Ces étapes sont assurées par la JVM.

Le schéma ci-dessous résume les étapes de compilation/interprétation du code Java :

![Compilation Java](/img/comp_java.png)


## Installation

Pour compiler et exécuter du code Java, il faut donc un JDK, un JRE et une JVM.

Chaque fois que le développeur télécharge un JDK, celui-ci inclut un JRE compatible avec la version, et ce JRE comprend lui-même un JVM par défaut. Il faut savoir qu'il est cependant possible de [télécharger le JRE indépendamment du JDK et de choisir la JVM parmi les différents types disponibles](https://www.oracle.com/java/technologies/javase-jre8-downloads.html).

**Quel JDK choisir ?**

[Un sondage sur 10500 développeurs Java](https://blogs.oracle.com/javamagazine/the-largest-survey-ever-of-java-developers) a été réalisé en 2018, dans lequel une question porte sur le JDK qu'ils utilisent.
Voici le résultat de ce sondage :

![Survey Java 2018](/img/jdk_survey_2018.png)

Les JDK les plus utilisés sont donc [Oracle JDK](https://www.oracle.com/fr/java/technologies/javase-downloads.html) et [OpenJDK](https://openjdk.java.net/).

- OpenJDK

**OpenJDK** est une implémentation gratuite et open-source de la plate-forme Java SE Edition. Il a été initialement publié en 2007 comme le résultat du développement que Sun Microsystems a commencé en 2006.

Il convient de souligner que l'OpenJDK est une implémentation de référence officielle de Java Standard Edition depuis la version SE 7.

- Oracle JDK

La société Oracle fournit un JDK nommé **Oracle JDK**.
Comme la grande majorité des JDK, celui-ci est basé sur OpenJDK.

Les différences majeurs entre les deux JDK cités ci-dessus proviennent de leur performance et licences. [Un article de 2020 par Baeldung explique ces différences](https://www.baeldung.com/oracle-jdk-vs-openjdk).