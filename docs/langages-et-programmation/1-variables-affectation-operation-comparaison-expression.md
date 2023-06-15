# Variables, affectation, opération, comparaison, expression

## Variable

!!! abstract "Cours" 
    Les données utilisées par un programme sont stockées dans des **variables**.

On peut voir une variable est un comme une “boite” identifiée par un nom dans laquelle on place des informations. Le contenu de cette “boite” évolue pendant l’exécution du programme[^1].

Dans la plupart des langages, et en particulier Python, le nom d’une variable :

- est constitué de lettres minuscules (```a``` à ```z```) et majuscules (```A``` à ```Z```), de nombres (```0``` à ```9```) ou du caractère souligné (```_```) ;
- ne doit pas comporter d’espace, de signes d’opération ```+```, ```-```, ```*``` ou ```/```, ni de caractères spéciaux comme ```',"``` ou ```@``` ;
- ne doit pas débuter par un chiffre ;
- ne doit pas être un mot réservé de Python, par exemple ```for```, ```if```, ```print```, etc. ;
- est sensible à la casse, ce qui signifie que les variables ```TesT```, ```test``` ou ```TEST``` sont différentes.

En pratique cela permet d’éviter les noms de variable réduits à une lettre et d’utiliser des noms qui ont un sens ! 

La [PEP 8](https://peps.python.org/pep-0008/) [^2] donne un grand nombre de recommandations de style pour écrire du code Python agréable à lire, et en particulier de nommer les variables par des mots en minuscule séparés par des blancs soulignés  « ```_``` »  par exemple ```nom_de_variable``` (style appelé  « *snake case* »[^3]).

[^1]:
    La notion de variable en informatique diffère des mathématiques. En mathématique une variable apparait dans l’expression symbolique d’une fonction $f(x)=2x+3$, ou dans une équation $2x+3=5x-3$ pour désigner une inconnue qu’il faut trouver, ou encore dans  une formule comme $(a+b)² =a²+2ab+b²$ pour indiquer que l’égalité est vraie pour toutes les valeurs de $a$ et $b$.

[^2]:
    [Une PEP (pour *Python Enhancement Proposal*)](https://www.python.org/dev/peps/#introduction) est un document fournissant des informations à la communauté Python, ou décrivant une nouvelle fonctionnalité. En particulier la [PEP 8](https://peps.python.org/pep-0008/) décrit les conventions de style de code agréable à lire.

[^3]: 
    En opposition au style appelé « *camel case* » qui consiste à écrire les mots attachés en commençant par des majuscules comme ```NomDeVariable```.

## Types de variables

!!! abstract "Cours" 
    Les variables peuvent être de **types** différents en fonction des informations qu’on veut y stocker.

On trouve par exemple :

- des nombres entiers (type ```int```) ;
- des nombres décimaux appelés « flottants » (type ```float```)  (:warning: le séparateur décimal est un point, PAS une virgule), noter qu'on peut par exemple écrire `5.`ou `.5` pour 5.0 ou 0.5 et `2e5` pour $2.10^5$ ;
- des booléens  prenant seulement les valeurs `True` ou `False` (type ```bool```) ;
- des textes ou chaines des caractères (type ```str```) écrits entre une paire de guillemets (```"```) ou d’apostrophes (```'```) ;
- des p_uplet, tableaux, dictionnaires , etc. 

##	Affectation

!!! abstract "Cours" 
    L'**affectation** consiste à stocker une valeur dans une variable. Dans la plupart des langages informatiques l’affectation est représentée par le signe « `=` ».

En algorithmique, l’affectation est symbolisée par une flèche allant de la valeur (à droite) vers la variable (à gauche)
Exemple : affecter la valeur 3 à la variable toto. ( en algorithmique  on écrit : 	```toto ←  3```)
``` python 
toto = 3
```

En pratique : Saisir dans un console Python :
``` python 
>>> toto = 3
>>> titi = 2.5
>>> tata = "ok"
```

Noter que la PEP 8 recommande de mettre des espace autour du signe = (mais ce n’est pas lu par Python) .
Attention, on ne peut pas écrire :
``` python 
>>> 3 = toto
  File "<interactive input>", line 1
SyntaxError: can't assign to literal
```

On peut aussi affecter la valeur d’une variable à une autre variable, par exemple :
``` python 
>>> a = 5
>>> b = a
>>> b
5
```
On peut aussi affecter la valeur de plusieurs variables en une seule ligne :
``` python 
>>> a, b = 5, 6
>>> a
5
>>> b
6
```

Note : La PEP 8 recommande de mettre un espace après les virgules (mais pas avant).
En Python, c’est l’affectation qui définit le type de la variable .
``` python 
>>> a = 3
>>> b = 3.0
>>> c = '3.0'
```
Les variables ```a```, ```b``` et ```c``` sont de types ```int```, ```float``` et ```str``` respectivement. 
On ne peut pas utiliser une variable avant de l’avoir définie.
``` python 
>>> d
Traceback (most recent call last):
  File "<interactive input>", line 1, in <module>
NameError: name 'd' is not defined
```

## Opérateurs arithmétiques sur les nombres
Les opérations arithmétiques usuelles sont effectuées sur des nombres et/ou des variables de types ```int``` ou ```float``` :

|opérateur|notation|
|---|:-:|
|addition|```a + b```|
|soustraction|```a - b```|
|multiplication|```a * b```|
|puissance|```a**b```|
|divisions décimale|```a / b```|

``` python 
>>> a = 5
>>> b = 2
>>> a + b
7
>>> a**b
25
>>> a / b
2.5
```
Notes :

- le résultat d’une opération est de type ```float``` si ```a``` ou ```b``` est de type ```float```, sinon de type ```int```, sauf pour la division où le résultat est toujours ```float``` ;
- pour obtenir la racine carrée d’un nombre on peut utiliser ```a ** 0.5``` ;
- l’ordre des priorités mathématiques est respecté ; 
- la PEP 8 recommande d'entourer les opérateurs (```+```,  ```-```, ```/```, ```*```) d'un espace avant et d'un espace après.

La division entière ```//``` et l’opération modulo ```%``` utilisés avec des entiers donnent respectivement le quotient et le reste de la division euclidienne, de type ```int``` : si $a = bq+r$ alors a ```// b``` donne q et ```a % b``` donne r .
``` python
>>> a = 17
>>> b = 5
>>> a // b				
3
>>> a % b
2
```
On peut affecter une valeur à une variable qui dépend de son ancienne valeur, par exemple l’augmenter d’une quantité donnée (on dit incrémenter).
``` python
>>> a = 3				
>>> a = a + 1				
>>> a					
4
>>> a = 0
>>> a = 2 * a + 1		
>>> a
9
```
Des raccourcis d’écriture existent en python pour aller plus vite (mais attention aux erreurs en les utilisant !) :
```a += 1``` signifie ```a = a + 1```, 	```a += b``` signifie ```a = a + b``` et ```a *= 2``` signifie ```a = a * 2```.


