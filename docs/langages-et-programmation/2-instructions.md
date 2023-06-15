# Instructions

Une instruction (ne pas confondre avec une expression) est commande qui doit être effectuée par la machine avant de passer à la suivante. Une séquence est une suite d’instructions exécutées dans l’ordre où elles sont écrites.
Affecter une valeur à une variable est une instruction.

- `a = 2`	est une instruction qui affecte la valeur `2` à la variable `a`.
- `print('hello world')`	est une instruction qui affiche la chaine  `'hello world'` dans la console.

## type()
On peut écrire une instruction pour connaitre le type d’une variable avec `type()`.

```py
>>> x = 2
>>> type(x)
<class 'int'>
>>> y = 2.0
>>> type(y)
<class 'float'>
>>> z = '2'
>>> type(z)
<class 'str'>
```
 
PEP8 : pas d’espace avant et à l’intérieur des parenthèses d’une fonction.
Rappel : En Python, la valeur `2` (type `int`) est égale à `2.0` (type `float`) et mais est différente de `'2'` (type `str`). 

## Conversion de type
On peut convertir une variable d’un type à un autre dans une instruction en utilisant:

|fonction|description|exemple|
|---|---|---|
|`int()`|Convertit une chaine de caractères ou un flottant en entier|`>>> int(2.8)`<br>`2`<br>`>>> int('2')`<br>`2`|
|`float()`|Convertit une chaine de caractères ou un entier en flottant|`>> float(5)`<br>`5.0`<br>`>>> float('5.5')`<br>`5.5`|
|`str()`|Convertit un entier ou un flottant en une chaine de caractères|`>>> str(5.5)`<br>`'5.5'`|

	
> **_NOTE:_** Observer dans la console comment un flottant qui prend une valeur entière (5) est affiché avec un point (5.0):

``` py
>>> a = 5
>>> a
5
>>> float(a)
5.0
```

## Instructions d’entrée et sortie
Une instruction d’entrée permet à un programme de lire des valeurs saisies au clavier par l’utilisateur. Une instruction de sortie affiche des messages à l’écran.
En python, la fonction `input()` permet d’écrire une instruction d’entrée qui affecte la valeur saisie à une variable. 
``` py
>>> saisie = input('Saisir un message')
>>> saisie
'abc'
```
La valeur renvoyée par `input()` est toujours du type chaine de caractères (type `str`). Pour obtenir un entier ou un flottant, il faut la convertir.
```py
>>> nombreentier = input('Entrez un nombre entier')
>>> nombreentier
'25'
```
Ici la valeur affectée à `nombreentier` est une chaine de caractères `'25'`. Pour obtenir un entier, il faut la convertir avec `int()`.
``` py
>>> nombreentier = int(input('Entrez un nombre entier'))
>>> nombreentier
25
```
Note : si l’utilisateur ne saisit pas un nombre entier, cela génère un message d’erreur.
Une instruction de sortie s’écrit en utilisant `print()` pour afficher à l’écran des chaines de caractère et/ou des variables, séparés par des virgules. 
```py
>>> print('hello')
hello
>>> message='world'
>>> print('hello', message)
hello world
>>> nombre = 5
>>> print(nombre)
5
>>> print('le nombre est', nombre)
le nombre est 5
>>> a = 5
>>> b = 6
>>> print('la somme de', a, 'et de', b, 'est', a + b)
la somme de 5 et de 6 est 11
```
PEP8 : on met des espaces après les caractères « `:` » et  « `,` » (mais pas avant).
Par défaut, `print()` provoque un retour à la ligne après l’affichage. Pour éviter cela on utilise une autre chaine de caractères à accoler à la fin de l’affichage avec `end=`, par exemple un espace ou même rien. 
```py
>>> print('hello', end=' ')
Hello >>>
```

Python 3.6 a introduit les chaine de caractères f-strings (formatted string) qui s’écrivent avec  f devant et permettent d’y insérer des variables, ou même des expressions. 
```py
>>> nom = 'Paul'
>>> age = 23
>>> print(f'Bonjour {nom}, vous avez {age} ans')
Votre nom est un Paul et vous avez 23 ans
```

Exercice corrigé : Écrire un premier programme en Python

Pour passer d’un pixel couleur codé RGB (mélange des trois couleurs rouge, vert, bleu) à un pixel en nuance de gris, on utilise la formule suivante :
G=0,11 × R + 0,83 × V + 0,06 ×B
Ecrire le programme qui demande en entrée les 3 couleurs d’un pixel et affiche en sortie la nuance de gris.

	Déterminer les informations à saisir, à calculer. Nommer les variables correspondantes et leur type.
Les informations à saisir sont les valeurs de rouge, de vert et de bleu. Il faut donc créer 3 variables par exemple R,V et B de type entier. L’information à calculer est le niveau de gris, que l’on peut stocker dans une quatrième variable aussi de type entier. 
	Exprimer le ou les traitements à effectuer
Le traitement à effectuer est donné par la formule. Attention, le résultat de la formule est un flottant, il doit être converti en nombre entier
	Déterminer la ou les variables à afficher
La variable à afficher est le niveau de gris G
	Ecrire le programme
R = int(input('Rouge:'))
V = int(input('Vert:'))
B = int(input('Bleu:'))
G = int(0.11 * R + 0.83 * V + 0.06 * B)
print('Le niveau de Gris est', G)

Note : Dans un premier temps on n’utilise pas def main(): généré par défaut par PyScripter
Note2: Essayer le programme sans faire la conversion des variables R, V et B en int et constater l’erreur produite
Note3 : On peut utiliser une f-string dans la dernière instruction : print(f'Le niveau de Gris est {G}')
Note4 : On peut ajouter des commentaires pour commenter un bloc d’instruction # Demande les 3 couleurs ou juste une ligne # Calcule le niveau de gris.
# Demande les 3 couleurs
R = int(input('Rouge:'))
V = int(input('Vert:'))
B = int(input('Bleu:'))

G = int(0.11 * R + 0.83 * V + 0.06 * B)   # Calcule le niveau de gris

print('Le niveau de Gris est', G)



























