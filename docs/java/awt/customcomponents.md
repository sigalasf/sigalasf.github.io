## Composants customisés

Avant de s'atarder sur la création de composants customisés, revenons sur les notions de :

- Panel
- Frame
- Window

### Panel

Panel est un composant qui permet de placer plusieurs composants dessus. Un Panel peut donc contenir d'autres Panel.

### Frame

Frame est un composant qui fonctionne comme la fenêtre principale de l’application graphique. Il est créé en utilisant la classe Frame. Pour toute application graphique, la première étape consiste à créer un cadre. Il existe deux méthodes pour créer un cadre: en étendant la classe Frame ou en créant un objet de la classe Frame.

### Différences entre Frame et Panel

Le Panel nécessite une Frame pour l'afficher. Une Frame, elle, peut être constituée d'un Panel ou d'un ensemble de Panel.

Les différences principales sont :

- **La hiérarchie de classe** : Panel est une sous-classe de **Container**, alors que Frame est une sous-classe de **Window** (qui eest une sous-classe de **Container**). 
- **Barre de titre** : Panel n'a pas de barre de titre contrairement à Frame.
- **Frontière** : Panel n'a pas de bordure contrairement à Frame.
- **Layouts par défaut** : Panel utilise **FlowLayout** par défaut, contrairement à Frame qui utilise **BorderLayout** par défaut.

### Création d'un nouveau composant

Il est possible de définir de nouveaux composants qui héritent directement de Panel :

!!! example "FlowLayout"
	=== "Code"
		```java linenums="1"
			public class PanneauClavier extends Panel {
   				public PanneauClavier() {
      				this.setLayout(new GridLayout(4,3));
      				for (int num=1; num <= 9 ; num++) {
        				this.add(new Button(Integer.toString(num)));
      				}
      				this.add(new Button("*");
      				this.add(new Button("0");
      				this.add(new Button("# ");
   				}
			}

			public class demo extends Applet {
   				public void init() { 
   					this.add(new PanneauClavier()); 
   				}
			}
		```