## Qu'est-ce que AWT ?

**Abstract Window Toolkit (AWT)** est une bibliothèque graphique pour Java, faisant partie de **Java Foundation Classes (JFC)**. Cette bibliothèque a été introduite dès les premières versions de Java (depuis Java 2), la bibliothèque de gestion de fenêtre officielle est Swing. Toutefois, AWT sert encore de fondement à Swing, dans la mesure où de nombreuses classes Swing héritent de classes AWT.

AWT permet notamment la création d'objets graphiques préconçus tel que des boutons, des sliders ou encore des menus déroulants.

![AWT Components](/img/awtcomponents.png)

### Dimensionnement des composants

En général, le dimensionnement des composants est automatique grâce au **LayoutManager**. Pour donner à un composant une taille donnée, il faut redéfinir la méthopde **getPreferedSize()** de la classe *Component*.

!!! example "Dimensionnement des composants"
	=== "Code"
		```java linenums="1"
			public class CustomButton extends Button {
				@Override
	   			public Dimension getPreferredSize() {
	      			return new Dimension(800, 250);
	   			}
			}
		```
	=== "Commentaire"
		La méthode **getPreferedSize()** indique la taille souhaitée mais pas celle imposée. En fonction du LayoutManager, le composant pourra ou non imposer sa taille.
		Cette méthode oblige à sous-classer tous les composants.
		Une autre façon de faire est de se passer des Layout et de placer les composants à la main en indiquant leurs coordonnées et leurs dimensions.
		Pour supprimer le Layout par défaut d'une classe, il faut appeler la méthode setLayout() avec comme paramètre null.
		Trois méthodes de la classe Component permettent de positionner des composants à la position (x,y) par rapport au conteur dans lequel il est inclus et d'indiquer sa largeur et sa hauteur : `setBounds(int x, int y, int largeur, int hauteur)`, `setLocation(int x , int y)` et `setSize(int largeur, int hauteur)`.

### Posionnement des composants

Lorqu'un composant graphique est intégré dans un conteneur, son emplacement est determiné de façon automatique : La mise en forme est dynamique.
Cependant, un layout manager peut être utilisé pour définir la position de chaque élément inséré. Dans ce cas, la position spécifiée est relative aux autres composants.

Chaque layout manager implémente l'interface java.awt.LayoutManager.

Pour affecter un LayoutManager, il faut faire appel à la méthode **setLayout()** de la classe *Container*.

!!! example "Appel à setLayout()"
	=== "Code"
		```java linenums="1"
			Panel panel = new Panel();
   			panel.setLayout( new GridLayout(5,5));
		```

Pour créer un espace entre les composants et le bord de leur conteneur, il faut redéfinir la méthode **getInsets()** de la classe *Container*.

!!! example "Redéfinition de getInsets()"
	=== "Code"
		```java linenums="1"
			@Override
			public Insets getInsets() {
   				Insets normal = super.getInsets();
   				// Cet exemple permet de laisser 10 pixels en plus entre chaque bords du conteneur.
   				return new Insets(normal.top + 10, normal.left + 10,
   				normal.bottom + 10, normal.right + 10);
			}
		```