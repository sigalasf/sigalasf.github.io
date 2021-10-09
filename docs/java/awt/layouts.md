## Les Layouts

Les layouts désignent la disposition des composants dans le conteneur. En d'autres termes, nous pouvons dire qu'il s'agit de placer les composants à une position particulière dans le conteneur. La tâche de mise en page des contrôles est effectuée automatiquement par le Layout Manager.

Le gestionnaire de mise en page positionne automatiquement tous les composants à l'intérieur du conteneur. Si nous n'utilisons pas le gestionnaire de disposition, les composants sont également positionnés par le gestionnaire de disposition par défaut. Il est possible de positionner les contrôles à la main mais cela devient très difficile pour les deux raisons suivantes :

- Il est très fastidieux de manipuler un grand nombre de contrôles dans le conteneur.

- Souvent, les informations relatives à la largeur et à la hauteur d'un composant ne sont pas fournies lorsque nous avons besoin de les agencer.

Java nous fournit divers gestionnaires de mise en page pour positionner les contrôles. Les propriétés telles que la taille, la forme et la disposition varient d'un gestionnaire de disposition à l'autre. Lorsque la taille de l'applet ou de la fenêtre d'application change, la taille, la forme et la disposition des composants changent également en réponse, c'est-à-dire que les gestionnaires de disposition s'adaptent aux dimensions de l'appletviewer ou de la fenêtre d'application.

Le gestionnaire de mise en page est associé à chaque objet issus de la classe *Container*. Chaque gestionnaire de disposition est un objet de la classe qui implémente l'interface *LayoutManager*.


### FlowLayout

Il s'agit du LayoutManager par défaut des applets. Il place les composants **ligne par ligne de gauche à droite**. Chaque ligne est complétée progressivement avant de passer à la suivante.

|  Constructeur    |Rôle  |
| ------------ | ------------- |
| FlowLayout() | Création d'un flow layout avec un alignement CENTER et un espacement horizontal/vertical de 5.  |
| FlowLayout(int align) | Permet de préciser l'alignement des composants dans le conteneur (CENTER, LEFT, RIGHT ... )  |
| FlowLayout( int align, int hgap, int vgap) | Permet de préciser l'alignement et l'espacement horizontal et vertical  |

!!! example "FlowLayout"
	=== "Code"
		```java linenums="1"
			public class CustomFrame extends Frame {
   				public CustomFrame() {
      				super();
      				this.setTitle(" Titre de la Fenetre ");
      				this.setSize(300, 150);
      				this.setLayout(new FlowLayout());
      				this.add(new Button("Bouton 1"));
      				this.add(new Button("Bouton 2"));
      				this.add(new Button("Bouton 3"));
      				this.pack();
      				this.show();
   				}

   				public static void main(String[] args) {
      				new CustomFrame();
   				}
			}
		```
	=== "Résultat"
		![Flow Layout](/img/flowlayout.png)

		Fenêtre redimensionnée :

		![Flow Layout Resize](/img/flowlayoutresize.png)

### BorderLayout

Ce LayoutManager découpe la surface en 5 zones : North, South, East, West, Center. Le composant du milieu dispose de la place non utilisée par les 4 autres composants.

|  Constructeur    |Rôle  |
| ------------ | ------------- |
| BorderLayout() | - |
| BorderLayout(int hgap,int vgap) | Permet de préciser l'espacement horizontal et vertical des composants. |

!!! example "BorderLayout"
	=== "Code"
		```java linenums="1"
			public class CustomFrame extends Frame {
   				public CustomFrame() {
      				this.super();
      				this.setTitle(" Titre de la Fenetre ");
      				this.setSize(300, 150);
      				// Border Layout
      				this.setLayout(new BorderLayout());
      				// Placement des composants
      				this.add(new Button("bouton haut"), BorderLayout.NORTH);
      				this.add(new Button("bouton bas"), BorderLayout.SOUTH);
      				this.add(new Button("bouton gauche"), BorderLayout.WEST);
      				this.add(new Button("bouton droite"), BorderLayout.EAST);
      				this.add(new Button("bouton milieu"), BorderLayout.CENTER);
      				this.pack();
      				this.show();
   				}

   				public static void main(String[] args) {
      				new CustomFrame();
   				}
			}
		```
	=== "Résultat"
		![Border Layout](/img/borderlayout.png)

### CardLayout

Ce LayoutManager aide à construire des boîtes de dialogue composées de plusieurs onglets. Un onglet se compose généralement de plusieurs contrôles : on insère des panneaux dans la fenêtre utilisée par le CardLayout Manager. Chaque panneau correspond à un onglet de boîte de dialogue et contient plusieurs contrôles. Par défaut, c'est le premier onglet qui est affiché.

|  Constructeur    |Rôle  |
| ------------ | ------------- |
| CardLayout() | - |
| CardLayout(int hgap,int vgap) | Permet de préciser l'espacement horizontal et vertical des composants. |


!!! example "CardLayout"
	=== "Code"
		```java linenums="1"
			public class CustomFrame extends Frame {
   				public CustomFrame() {
      				super();
      				this.setTitle("Titre de la Fenetre ");
      				this.setSize(300,150);
      				CardLayout cardLayout = new CardLayout();
      				this.setLayout(cardLayout);

      				// Création d'un panneau contenant les contrôles d'un onglet
      				Panel panel = new Panel();
      
      				// Ajouter les composants au panel
      				panel.add(new Button("Bouton 1 panneau 1"));
      				panel.add(new Button("Bouton 2 panneau 1"));

      				// Inclure le panneau dans la fenetre sous le nom "Page1" : Il s'agit du premier onglet affiché par défaut.
      				this.add("Page1", panel);

     				// Déclaration et insertion de l'onglet suivant
      				panel = new Panel();
      				panel.add(new Button("Bouton 1 panneau 2"));
      				this.add("Page2", panel);
     
      				pack();
      				show();  
   				}

   				public static void main(String[] args) {
      				new CustomFrame();
   				}
			}
		```
	=== "Résultat"
		![Card Layout](/img/cardlayout.png)


Lors de l'insertion d'un onglet, un nom doit lui être attribué. Les fonctions nécessaires pour afficher un onglet de boîte de dialogue ne sont pas fournies par les méthodes du conteneur, mais seulement par le Layout Manager. Il est nécessaire de sauvegarder temporairement le Layout Manager dans une variable où déterminer le gestionnaire en cours par un appel à getLayout(). Pour appeler un onglet donné, il faut utiliser la méthode **show()** du CardLayout Manager.


!!! example "CardLayout"
	=== "Code"
		```java linenums="1"
			((CardLayout)getLayout()).show(this, "Page2");
		```
	=== "Résultat"
		![Card Layout](/img/cardlayoutp2.png)

!!! warning "Note"
	Les méthodes **first()**, **last()**, **next()** et **previous()** servent à parcourir les onglets de boîte de dialogue.

	```java linenums="1"
		((CardLayout)getLayout()).first(this);
	```


### GridLayout

Ce LayoutManager établit un réseau de cellules identiques qui forment une sorte de quadrillage invisible : les composants sont organisés en lignes et en colonnes. Les éléments insérés dans la grille ont tous la même taille. Les cellules du quadrillage se remplissent de gauche à droite ou de haut en bas.


|  Constructeur    |Rôle  |
| ------------ | ------------- |
| GridLayout(int columns, int rows) | Les deux premiers entiers spécifient le nombre de lignes ou de colonnes de la grille.  |
| GridLayout(int columns, int rows, int hgap, int vgap) | permet de préciser en plus l'espacement horizontal et vertical des composants.  |


!!! example "GridLayout"
	=== "Code"
		```java linenums="1"
			public class CustomFrame extends Frame {
   				public CustomFrame() {
      				super();
      				this.setTitle("Titre de la Fenetre ");
      				this.setSize(300,150);
      				setLayout(new GridLayout(2, 3));
      				this.add(new Button("bouton 1"));
      				this.add(new Button("bouton 2"));
     				this.add(new Button("bouton 3"));
      				this.add(new Button("bouton 4")); 
      				this.add(new Button("bouton 5 tres long"));
      				this.add(new Button("bouton 6"));
     
      				pack();
      				show();  
   				}

   				public static void main(String[] args) {
      				new CustomFrame();
   				}
			}
		```
	=== "Résultat"
		![Grid Layout](/img/gridlayout.png)



### GridBagLayout

Ce gestionnaire (grille étendue) est le plus riche en fonctionnalités : le conteneur est divisé en cellules égales mais un composant peut occuper plusieurs cellules de la grille et il est possible de faire une distribution dans des cellules distinctes. Un objet de la classe GridBagConstraints permet de donner les indications de positionnement et de dimension à l'objet GridBagLayout.

Les lignes et les colonnes prennent naissance au moment où les contrôles sont ajoutés. Chaque contrôle est associé à un objet de la classe GridBagConstraints qui indique l'emplacement voulu pour le contrôle.

```java linenums="1"
	GridBagLayout gridBagLayout = new GridBagLayout();
	GridBagConstraints gridBagConstraints = new GridBagConstraints();
```

L'objet **GridBagConstraints** peut être manipulé via les variables :

|  Variable    |Rôle  |
| ------------ | ------------- |
| gridx et gridy | Ces variables contiennent les coordonnées de l'origine de la grille. Elles permettent un positionnement précis à une certaine position d'un composant. Par défaut elles ont la valeur GrigBagConstraint.RELATIVE qui indique qu'un composant se range à droite du précédent. |
| gridwidth, gridheight  | Définissent combien de cellules va occuper le composant (en hauteur et largeur). Par défaut la valeur est 1. L'indication est relative aux autres composants de la ligne ou de la colonne. La valeur GridBagConstraints.REMAINDER spécifie que le prochain composant inséré sera le dernier de la ligne ou de la colonne courante. La valeur GridBagConstraints.RELATIVE place le composant après le dernier composant d'une ligne ou d'une colonne. |
| fill | Définit le sort d'un composant plus petit que la cellule de la grille. GridBagConstraints.NONE conserve la taille d'origine : valeur par défaut GridBagConstraints.HORIZONTAL dilaté horizontalement GridBagConstraints.VERTICAL dilaté verticalement GridBagConstraints.BOTH dilatés aux dimensions de la cellule. |
| ipadx, ipady | Permettent de définir l'agrandissement horizontal et vertical des composants. Ne fonctionne que si une dilatation est demandée par fill. La valeur par défaut est (0,0). |
| anchor | Lorsqu'un composant est plus petit que la cellule dans laquelle il est inséré, il peut être positionné à l'aide de cette variable pour définir le côté par lequel le contrôle doit être aligné dans la cellule. Les variables possibles sont NORTH, NORTHWEST, NORTHEAST, SOUTH, SOUTHWEST, SOUTHEAST, WEST et EAST. |
| weightx, weighty | Permettent de définir la répartition de l'espace en cas de changement de dimension. |

!!! example "GridBagLayout"
	=== "Code"
		```java linenums="1"
			public class CustomFrame extends Frame {
   				public CustomFrame() {
      				super();
      				this.setTitle("Titre de la Fenetre ");
      				this.setSize(300,150);

      				Button b1 = new Button(" bouton 1 ");
      				Button b2 = new Button(" bouton 2 ");
      				Button b3 = new Button(" bouton 3 ");

      				GridBagLayout gridBagLayout = new GridBagLayout();
      				GridBagConstraints gridBagConstraints = new GridBagConstraints();
      				this.setLayout(gridBagLayout);

      				// Propriétés du GridBadConstraints
      				gridBagConstraints.fill = GridBagConstraints.BOTH;
      				gridBagConstraints.weightx = 1;
      				gridBagConstraints.weighty = 1;

      				// Mise en forme des objets
      				gridBagLayout.setConstraints(b1, gridBagConstraints);
      				gridBagLayout.setConstraints(b2, gridBagConstraints);
      				gridBagLayout.setConstraints(b3, gridBagConstraints);

      				this.add(b1);
      				this.add(b2);
      				this.add(b3);
     
      				pack();
      				show();  
   				}

   				public static void main(String[] args) {
      				new CustomFrame();
   				}
			}
		```
	=== "Résultat"
		![GridBag Layout](/img/gridbaglayout.png)

		Cet exemple place trois boutons l'un à coté de l'autre. Ceci permet en cas de changement de dimension du conteneur de conserver la mise en page : la taille des composants est automatiquement ajustée.

		Pour placer les 3 boutons l'un au-dessus de l'autre, il faut affecter la valeur 1 à la variable gbc.gridx :

		![GridBag Layout](/img/gridbaglayoutx.png)
