# Interfaces ou classes abstraites ?

## Les interfaces

Une interface permet de déclarer des méthodes, qui définit donc un ensemble de services visibles depuis l’extérieur, sans se préoccuper de la façon dont ces services seront réellement implémentés. Une classe qui implémente une interface doit obligatoirement implémenter chacune des méthodes déclarées dans l’interface, à moins qu’elle ne soit elle-même déclarée abstraite.

## Les classes abstraites

Une classe abstraite est une classe dont toutes les méthodes n’ont pas été implémentées. Elle n’est donc pas instanciable, mais sert avant tout à factoriser du code. Une classe qui hérite d’une classe abstraite doit obligatoirement implémenter les méthodes manquantes (qui ont été elles-mêmes déclarées « abstraites » dans la classe parente). En revanche, elle n’est pas obligée de réimplémenter les méthodes déjà implémentées dans la classe parente (d’où une maintenance du code plus facile).