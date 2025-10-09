# Écriture d’un entier positif dans une base b >= 2

## Système décimal ou base 10

Dans le système décimal que l'on utilise tous les jours, les nombres sont écrit à l'aide des 10 chiffres bien connus : 0, 1, 2, 3, 4, 5, 6, 7, 8 et 9. 

C'est la position d'un chiffre dans un nombre qui indique son importance, ou **poids**, dans ce nombre. Par exemple, le nombre qui s'écrit 2083 est égal à 2 milliers plus 8 dizaines plus 3 unités. Il n'est pas égal au nombre 8320, même s'il s'écrit avec les mêmes chiffres 0, 2, 8 et 3.

Tout nombre entier naturel peut s’écrire comme combinaison linéaire de puissance de 10. Par exemple, les chiffres du nombre 2083 correspondent à :

|chiffre|2|0|8|3|
|:-:|:-:|:-:|:-:|:-:|
|i|3|2|1|0|
|$10^i$|$10^3$|$10^2$|$10^1$|$10^0$|
|combinaison|$2 \times 10^3$|$0 \times 10^2$|$8 \times 10^1$|$3 \times 10^0$|

$2083 = 2 \times 10^3 + 0 \times 10^2 + 8 \times 10^1 + 3 \times 10^0$

De manière générale, un nombre $n$ qui s'écrit dans le système décimal avec $p$ chiffres $d_{p−1}d_{p−2}...d_2d_1d_0$  (chaque $d_i$ est un chiffre valant entre 0 et 9)[^1.1] est égal à : 

[^1.1]: Dans l'écriture $d_{p−1}d_{p−2}...d_2d_1d_0$, le chiffre $d_{p−1}$ est dit de « poids fort » et $d_0$ de « poids faible ». On a l'habitude d'écrire les nombres en partant du poids le plus fort à gauche jusqu'au poids le plus faible à droite, cette représentation est appelée « gros boutisme », ou « *big endian* », mais certains systèmes d'exploitation utilisent la convention inverse, appelée « petit boutisme », ou « *little endian* ».

$n = d_{p−1} \times 10^{p−1}  + d_{p−2} \times 10^{p−2} + ... +  d_2 \times 10^2 + d_1 \times 10^1 + d_0 \times 10^0$

ou encore avec la formule mathématique d'une somme de $0$ à $p-1$ :
$n = \sum_{i=0}^{p-1} d_i × 10^i$


Noter qu'on peut écrire 10 nombres allant de 0 à 9 avec 1 seul chiffre, 100 nombres allant de 0 à 99 avec 2 chiffres, 1000 nombres allant de 0 à 999 avec 3 chiffres, ... $10^p$ nombres allant de 0 à $10^p-1$ avec $p$ chiffres.

Quand on ajoute un chiffre 0 à droite d'un nombre $n$, tous les chiffres sont décalés vers la droite, les puissances de 10 correspondantes sont augmentées d'une unité, donc le nombre $n$ est multiplié par 10.


Réciproquement, on peut écrire chacun des chiffres d'un nombre décimal $n$ qui s'écrit dans le système décimal avec $p$ chiffres $d_{p−1}d_{p−2}...d_2d_1d_0$ par un algorithme simple qui consiste à effectuer une succession de divisions entières par 10  :

!!! notetip inline end "" 
	L'opérateur de division entière ```//``` et l’opération modulo ```%``` utilisés avec des entiers (de type ```int```) donnent respectivement le quotient et le reste d'une division euclidienne : si `a` et `b` sont des entiers tels que $a = b \times q + r$,  alors ```a // b``` renvoie $q$ et ```a % b``` renvoie $r$.



- Le reste de la division entière de $n$ par $10$, `n % 10` en Python, renvoie $d_0$. Cela permet d'obtenir le dernier chiffre de l'écriture décimale de $n$.

- Le quotient de la division entière de $n$ par $10$, `n // 10` en Python, renvoie $d_{p−1}d_{p−2}...d_2b_1$. On remplace $n$ par ce nombre pour trouver les autres chiffres.


Il suffit alors de répéter l'opération jusqu'à ce que $n$ soit égal à 0, on aura bien obtenu tous les chiffres de l'écriture décimale de $n$. 


Prenons l'exemple du nombre $n = 2083$, le reste de la division entière par 10 est 3 et le quotient 208.

![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-1-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-1-dark-mode.png#only-dark){width=25% align=right}

``` py
>>> 2083 % 10
3
>>> 2083 // 10
208
```

On a déjà trouvé le dernier chiffre : 3. Continuons avec 208. Le reste de la division entière de 208 par 10 est 8 et le quotient 20.

![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-2-light-mode.png#only-light){width=25% align=right}

![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-2-dark-mode.png#only-dark){width=25% align=right}

``` py
>>> 208 % 10
8
>>> 208 // 10
20
```

On obtient le 8. Continuons avec 20. Le reste de la division entière de 20 par 10 est 0 et le quotient 2.

![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-3-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-3-dark-mode.png#only-dark){width=25% align=right}

``` py
>>> 20 % 10
0
>>> 20 // 10
2
```

On obtient le 0. Continuons avec 2. Le reste de la division entière de 2 par 10 est 2 et le quotient 0.

![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-4-light-mode.png#only-light){width=25%  align=right}
![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-4-dark-mode.png#only-dark){width=25% align=right}


``` py
>>> 2 % 10
2
>>> 2 // 10
0
```
On a obtenu le dernier chiffre 2.  Le quotient est 0, inutile de continuer les divisions, tous les chiffres ont été trouvés.


![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-5-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 2083 par 10](assets/1-2083-divise-par-10-5-dark-mode.png#only-dark){width=25% align=right}

Noter qu'on a obtenu les chiffres de l'écriture décimale de 2083, mais :warning: de gauche à droite, il faut donc les lire de droite à gauche pour retrouver 2083.

On peut traduire cet algorithme en Python, par exemple pour écrire une fonction `etoile` qui renvoie une chaîne de caractère composées de tous les chiffres d'un nombre entier `n` suivis d'une étoile.

``` py
def etoile(n):
	n_etoile = ''
	while n > 0:
		n_etoile =  str(n % 10) + '*' + n_etoile
		n = n // 10
	return n_etoile

>>> etoile(2083)
'2*0*8*3*'
```
On note que le cas ou `n` est égal à `0`, la fonction n'entre pas dans la boucle `while` et renvoie une chaîne vide. On peut traiter le cas séparément en ajoutant les lignes :

``` py
def etoile(n):
	if n == 0:
		return '0*'
	n_etoile = ''
	while n > 0:
		...
```



!!! question "Exercice corrigé" 
    Un nombre harshad, ou nombre de Niven, est un entier naturel qui est divisible par la somme de ses chiffres dans une base donnée [...]. En base dix, les vingt premiers nombres harshad strictement supérieurs à 10 sont (suite A005349 de l'OEIS) :
	12, 18, 20, 21, 24, 27, 30, 36, 40, 42, 45, 48, 50, 54, 60, 63, 70, 72, 80 et 81.
    Source : [https://fr.wikipedia.org/wiki/Nombre_harshad](https://fr.wikipedia.org/wiki/Nombre_harshad).
	
	
	Écrire un programme demande un nombre entier et affiche s'il est un nombre harshad ou pas.

	


??? Success "Réponse"

    ``` py
	n = int(input())
	n_initial = n
	somme = 0
	while n > 0:
		somme = somme + n % 10
		n = n // 10
	if n_initial % somme == 0:
		print(n_initial, "est un nombre de harshad")
	else:
		print(n_initial, "n'est pas un nombre de harshad")

	```
   

## Système binaire ou base 2

!!! abstract "Cours" 
	En binaire, ou base 2, les seuls chiffres utilisés pour écrire des nombres sont 0 et 1, aussi appelés « bits » pour *binary digits*, ou « chiffres binaires » en français. 

	8 bits forment un **octet**.



Par exemple on peut écrire $1101$, que l'on note aussi $1101_2$, pour indiquer qu'il est écrit en binaire.

Il convient également de ne pas lire ces nombres comme on lirait des nombres décimaux. Ainsi, $1101_2$ ne se dit pas « mille cent un » mais plutôt « un un zéro un ».

Comme dans le système décimal, c'est la position qui indique le poids de chaque bit dans un nombre. Mais en binaire, c'est une combinaison linéaire de puissances de 2. Par exemple, les bits du nombre $1101_2$ correspondent à :

|bits|1|1|0|1|
|:-:|:-:|:-:|:-:|:-:|
|i|3|2|1|0|
|$2^i$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|combinaison|$1 \times 2^3=8$|$1 \times 2^2=4$|$0 \times 2^1=0$|$1 \times 2^0=1$|



$1101_2 = 1 × 2^3 + 1 × 2^2 + 0 × 2^1 + 1 × 2^0 = 13_{10}$

Noter le $..._{10}$ pour indiquer que $13$ est un nombre en base 10.



!!! abstract "Cours" 

	De manière générale, un nombre $n$ qui s'écrit dans le système binaire avec $p$ bits $b_{p−1}b_{p−2}...b_2b_1b_0$  (chaque $b_i$ est un bit valant 0 ou 1) a une valeur décimale égale à : 

	$n = b_{p−1} \times 2^{p−1}  + b_{p−2} \times 2^{p−2} + ... +  b_2 \times 2^2 + b_1 \times 2^1  + b_0 \times 2^0$

	ou encore avec la formule mathématique d'une somme de $0$ à $p-1$ :
	$n = \sum_{i=0}^{p-1} b_i × 2^i$




	



### Écrire un nombre binaire en décimal

La formule précédente permet d'écrire facilement un nombre binaire en décimal. Il suffit de multiplier chaque bit par la puissance de 2 correspondante et de faire la somme des valeurs obtenues. 

Énumérons les premiers nombres binaires et quelques autres :

|binaire|combinaison|décimal|
|-:|:-|:-|
|$0$|0|0||
|$1$|$1 \times 2^0$|1|
|$10$|$1 \times 2^1$|2|
|$11$|$1 \times 2^1 + 1 \times 2^0$|3|
|$100$|$1 \times 2^2$|4|
|$101$|$1 \times 2^2 + 1 \times 2^0$|5|
|$110$|$1 \times 2^2 + 1 \times 2^1$|6|
|$111$|$1 \times 2^2 + 1 \times 2^1 + 1 \times 2^0$|7|
|$1000$|$1 \times 2^3$|8|
|$1 \space 0000$|$1 \times 2^4$|16|
|$10 \space 0000$|$1 \times 2^5$|32|
|$100 \space 0000$|$1 \times 2^6$|64|
|$1000 \space 0000$|$1 \times 2^7$|128|
|$1111 \space 1111$|$1 \times 2^8 + 1 \times 2^7 + 1 \times 2^6 +...1 \times 2^0$|255|


!!! question "Exercice corrigé" 
    Calculer la valeur décimale des nombres binaires suivants :

	- 11010
	- 10101
	- 11100110

	

??? Success "Réponse"
    
	$11010_2 = 1 \times 2^4 + 1 \times 2^3 + 1 \times 2^1 = 16 + 8 + 2 = 26_{10}$
	
	$1 \space 0101_2 = 1 \times 2^4 + 1 \times 2^2 + 1 \times 2^0 = 16 + 4 + 1= 21_{10}$
	
	$1110 \space 0110_2 = 1 \times 2^7 + 1 \times 2^6 + 1 \times 2^5 + 1 \times 2^2 + 1 \times 2^1 = 
	128 + 64 + 32 + 4 + 2=230_{10}$





Traduisons cela en Python. Pour plus de simplicité, on peut parcourir le nombre binaire de gauche à droite.


``` py
def bin_to_dec(n):
    """ str -> int
	Renvoie l'écriture décimale de la chaine de caractère n représentant un nombre binaire
	"""
    dec = 0
    for i in range(len(n)):
	    dec = dec + int(n[-i-1]) * 2**i
	return dec
```


En Python, les nombres binaires s'écrivent avec le préfixe ```0b``` et l'équivalent en décimal est affiché automatique dans la console :

``` py
>>> 0b1101
13
```


### Écrire un nombre décimal en binaire

Il existe plusieurs méthodes pour écrire un nombre décimal en binaire : 

- Trouver les puissances de 2 est la méthode la plus simple qui aide à comprendre la structure du binaire, mais elle est peu utilisée en pratique.

- Effectuer des divisions successives par 2 est pratique pour un calcul algorithmique.

- Utiliser une fonction Python.

#### Trouver les puissances de 2

On peut faire l'opération inverse de l'écriture d'un nombre binaire en décimal en essayant de retrouver la combinaison linéaire de puissances de 2 d'un nombre binaire.

Cherchons pas exemple, l'écriture binaire du nombre $13_{10}$. Il faut remplir le tableau des puissances de 2 suivant :

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|?|?|?|?|?|

On pourrait commencer par remplir le tableau à droite, du côté des petites puissances de 2 : $2^0 = 1$

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|?|?|?|?|1|

Puis on continue :  $2^0 + 2^1 = 1+2=3$

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|?|?|?|1|1|

Et encore :  $2^0 + 2^1 + 2^2  = 1+2+4=7$

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|?|?|1|1|1|

Mais quand on arrive là, on est coincé ! La puissance suivante est $2^3 = 8$, c'est trop grand pour obtenir $13$ et toutes les autres puissances seront encore plus grande. 

Il faut donc procéder dans l'autre sens, en partant de la gauche, du côté des grandes puissances[^1.2].

[^1.2]: Ce type d'algorithme appartient à la famille des « algorithmes gloutons ».

$2^4 = 16$, c'est plus grand que $13$, on ne peut pas prendre le bit correspondant, on met 0 ! 

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|0|?|?|?|?|

$2^3 = 8$, c'est plus petit que $13$, on met 1 pour le bit correspondant. Il reste $13-8=5$ à trouver. 

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|0|1|?|?|?|

$2^2 = 4$, c'est plus petit que $5$, on met 1 pour le bit correspondant. Il reste $5-4=1$ à trouver. 

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|0|1|1|?|?|

$2^1 = 2$, c'est plus grand que  $1$,  on ne peut pas prendre le bit correspondant, on met 0. 

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|0|1|1|0|?|

$2^0 = 1$, c'est le dernier bit que l'on cherchait, on met 1. 

|i|4|3|2|1|0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
|binaire|0|1|1|0|1|

On a bien trouvé l'écriture binaire de $13_{10}$, c'est $1101_2$.

Voilà l'algorithme que l'on a suivi :

- On repère la plus grande puissance de 2 plus petite ou égale au nombre.
- On soustrait, puis on continue avec le reste.
- On met 1 si la puissance est utilisée, 0 sinon.


!!! question "Exercice corrigé" 
    Compléter le tableau pour écrire $22_{10}$ et $29_{10}$ en binaire :

	|i|4|3|2|1|0|
	|:-:|:-:|:-:|:-:|:-:|:-:|
	|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$|
	|$22_{10}$||||||
	|$29_{10}$||||||


	

??? Success "Réponse"
    
	|i|4|3|2|1|0||
	|:-:|:-:|:-:|:-:|:-:|:-:||
	|$2^i$|$2^4=16$|$2^3=8$|$2^2=4$|$2^1=2$|$2^0=1$||
	|$22_{10}$|1|0|1|1|0|$= 10110_2$|
	|$29_{10}$|1|1|1|0|1|$= 11101_2$|

	
	


C'est une méthode simple et intuitive, mais en pratique elle est inefficace et peu utilisée, en particulier pour les grands nombres, car elle consiste à calculer et garder en mémoire de nombreuses puissances de 2 inutiles. 

#### Effectuer des divisions successives par 2

De la même manière qu'on a utilisée précédemment pour trouver les chiffres en base 10 d'un nombre par une succession de divisions entières par 10, on peut écrire un nombre décimal $n$ sous sa forme binaire $b_{p−1}b_{p−2}...b_2b_1b_0$ en effectuant des divisions entières par 2 :

- Le reste de la division entière de $n$ par $2$, `n % 2` en Python, renvoie $b_0$. Cela permet d'obtenir le dernier bit de l'écriture binaire de $n$.

- Le quotient de la division entière de $n$ par $2$, `n // 2` en Python, renvoie $b_{p−1}b_{p−2}...b_2b_1$. On remplace $n$ par ce nombre pour trouver les autres bits.


Il suffit alors de répéter l'opération jusqu'à ce que $n$ soit égal à 0, on aura bien obtenu tous les bits de l'écriture binaire de $n$. 

:warning: Attention, on obtient les bits de la gauche vers la droite.

Prenons l'exemple de $n_{10} = 13$,  le reste de la division entière par 2 est 1 et le quotient 6.

![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-1-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-1-dark-mode.png#only-dark){width=25% align=right}

``` py
>>> 13 % 2
1
>>> 13 // 2
6
```

On a déjà trouvé le dernier bit : 1. Continuons avec 6. Le reste de la division entière de 6 par 2 est 0 et le quotient 3.

![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-2-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-2-dark-mode.png#only-dark){width=25% align=right}


``` py
>>> 6 % 2
0
>>> 6 // 2
3
```

On obtient le bit 0. Continuons avec 3. Le reste de la division entière de 3 par 2 est 1 et le quotient 1.

![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-3-light-mode.png#only-light){width=25%  align=right}
![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-3-dark-mode.png#only-dark){width=25% align=right}

``` py
>>> 3 % 2
1
>>> 3 // 2
1
```

On obtient le bit 1. Continuons avec 1. Le reste de la division entière de 1 par 2 est 1 et le quotient 0.

![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-4-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-4-dark-mode.png#only-dark){width=25% align=right}


``` py
>>> 1 % 2
1
>>> 1 // 2
0
```
On a obtenu le dernier bit, c'est encore 1.  Le quotient est 0, inutile de continuer les divisions, tous les bits ont été trouvés.


![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-5-light-mode.png#only-light){width=25% align=right}
![Divisions euclidiennes successives de 13 par 2](assets/1-13-divise-par-2-5-dark-mode.png#only-dark){width=25% align=right}


On a obtenu les bits de l'écriture binaire de $13_{10}$, mais :warning: de gauche à droite, il faut donc les lire de droite à gauche pour trouver $1101_2$.


!!! question "Exercice corrigé" 
    Écrire les nombres suivants en binaire :

	- 178
	
	- 761


	

??? Success "Réponse"
    
	$178_{10} = 10110010_2$

	$761_{10} = 1011111001_2$
	


On peut traduire cet algorithme en Python, par exemple pour écrire une fonction `dec_to_bin` qui renvoie l'écriture binaire d'un nombre entier `n` :


``` py
def dec_to_bin(n):
    """ int -> str
	Renvoie l'écriture binaire de l'entier n 
	"""
    b = ''
    while n > 0:
		b =  str(n % 2) + b     
		n = n // 2
	return b
   

>>> bin_to_dec(13)
'1101'
```

:warning: Il faut écrire `b =  str(n % 2) + b` et non pas `b =  b + str(n % 2)`, c''est un bug classique, car le premier bit trouvé est $b_0$ et le dernier est $b_{p−1}$.

On note que le cas ou `n` est égal à `0`, la fonction n'entre pas dans la boucle `while` et renvoie une chaîne vide. On peut traiter le cas séparément au début de la fonction :


``` py
def dec_to_bin(n):
    """ int -> str
	Renvoie l'écriture binaire de l'entier n 
	"""
	if n == 0:
		return '0'
    b = ''
    while n > 0:
		b =  str(n % 2) + b
		n = n // 2
	return b
   
```

#### Fonction Python `bin`

En Python, il existe bien sûr une fonction `bin` qui permet d'écrire un nombre décimal en binaire, mais il est souvent interdit de l'utiliser dans le cadre de NSI :

``` py
>>> bin(13)
'0b1101'
```

### Opérations
Les quatre opérations de base (addition, soustraction, multiplication et division) restent exactement les mêmes qu'en écriture décimale, mais sont plus simples parce qu'il n'y a que les deux chiffres 0 et 1.


-	Addition

	On additionne bit à bit en prenant soin d'aligner les bits de même poids à droite et on calcule de la droite vers la gauche en passant la retenue si nécessaire. 

	Les additions bit à bit sont simples :

	- 0 + 0 = 0    
	- 0 + 1 = 1
	- 1 + 0 = 1
	- 1 + 1 = 10 :warning: passer la retenue de 1 à droite

	Exemple : Calculer  $101101 + 1100$
	

		
	![Exemple d'addition posée en binaire : 101101+1100](assets/1-addition-binaire-light-mode.png#only-light){width=15% align=right}
	![Exemple d'addition posée en binaire : 101101+1100](assets/1-addition-binaire-dark-mode.png#only-dark){width=15% align=right}

	On aligne d'abord à gauche les bits des deux nombres l'un au dessus de l'autre. Puis on commence par ajouter les deux bits les plus à droite, $1 + 0 = 1$, puis on continue vers la gauche, $0 + 0 = 0$. On arrive à $1 + 1$, ce qui fait $10$, on garde le $0$ et on ajoute une retenue de $1$ à gauche. On ajoute les bits suivants, avec cette retenue on a $1 + 1 + 1$, ce qui fait $11$, on garde le $1$ et on ajoute une nouvelle retenue de $1$ encore à gauche. Les deux derniers bits ne sont que sur le premier nombre, on fait comme si c'était des $0$ sur le second pour terminer l'addition. On trouve le résultat final, $101101 + 1100 = 111011$, c'est l'équivalent binaire de $45+12=57$ en décimal.
	


	!!! question "Exercice corrigé" 
		Calculer les additions suivantes en binaire :

		- $10101 + 1011$
		
		- $11101 + 11011$

		- $11010 + 11010$


		

	??? Success "Réponse"

		$10101 + 1011 = 11110$
		
		$11101 + 11011 = 111000$

		$11010 + 11010 = 110100$

 
 
 
-	Soustraction

	Comme pour l'addition, on soustrait bit à bit en prenant soin d'aligner les bits de même poids à droite et on calcule de la droite vers la gauche en passant la retenue si nécessaire. 

	Les soustractions bit à bit sont simples :

	- 0 - 0 = 0    
	- 1 - 0 = 1
	- 1 - 1 = 0
	- 0 - 1.  :warning: Il faut calculer 10 - 1 = 1  et passer la retenue de 1 à droite

	Exemple : Calculer  $110001 - 11100$

		
	![Exemple de soustraction posée en binaire : 110001-11100](assets/1-soustraction-binaire-light-mode.png#only-light){width=15% align=right}
	![Exemple de soustraction posée en binaire : 110001-11100](assets/1-soustraction-binaire-dark-mode.png#only-dark){width=15% align=right}

	On aligne d'abord à gauche les bits des deux nombres le plus grand au dessus de l'autre. Puis on commence par soustraire les deux bits les plus à droite, $1 - 0 = 1$, et on remonte vers la gauche, $0 - 0 = 0$. On arrive à $0 - 1$, on garde le $0$ et on ajoute la retenue de $1$ au chiffre du bas à droite. Ici on applique la méthode française (ou méthode « par compensation »)[^1.3] qui consiste à ajouter la retenue à la gauche du nombre en bas : $11 + 1 = 100$. On continue la soustraction en remplaçant ces deux bits $11$ par $100$. On obtient $0 - 0 = 0$, puis $1-0=1$, et enfin $1-1=0$. On trouve le résultat final, $110001 - 11100 = 010101$, ou $10101$ en omettant le $0$ inutile à gauche, c'est l'équivalent binaire de $49-28=21$ en décimal.

	[^1.3]: Il existe une autre méthode, appelée méthode anglo-saxonne « par emprunt » ou « par cassage », qui consiste à soustraire la retenue du nombre du haut.


	!!! question "Exercice corrigé" 
		Calculer les additions suivantes en binaire :

		- $10101 - 1001$
		
		- $10000 - 1$

		- $1101001 - 1011011$


		

	??? Success "Réponse"

		$10101 - 1001 = 1100$
		
		$10000 - 1 = 111000$

		$1101001 - 1011011 = 1110$




- Multiplication

	On a fait dans un exercice précédant la multiplication d'un nombre binaire par 2 en l'ajoutant à lui-même :	$11010 + 11010 = 110100$

	On aurait pu aussi poser cette multiplication bit à bit comme pour une multiplication dans le système décimal, en notant que 2 s'écrit 10 en binaire :

			
	![Exemple de multiplication posée en binaire : 11010x10](assets/1-multiplication-binaire-light-mode.png#only-light){width=15% align=right}
	![Exemple de multiplication posée en binaire : 11010x10](assets/1-multiplication-binaire-dark-mode.png#only-dark){width=15% align=right}

	On commence par multiplier $11010$ par le $0$ de $10$ et on écrit le résultat, $0$, sur la première ligne. Puis on multiplie $11010$ par le $1$ de $10$ et on écrit le résultat, $11010$, sur la seconde ligne en décalant d'un bit vers la gauche. On fait ensuite la somme des deux lignes et on obtient le résultat final $110100$.

	On constate que multiplier un nombre binaire par 2 ($= 10_2$ en binaire) se fait en ajoutant un zéro à droite.
	
	En effet, si on reprend la décomposition en puissances de 2 de $11010_2$ (ou $26_{10}$) :
	
	$11010_2 = 1 \times 2^4 + 1 \times 2^3 + 1 \times 2^1$

	quand on le multiplie par 2, toutes les puissances augmentent d'une unité. On obtient bien le nombre binaire :

	$2 \times(1 \times 2^4 + 1 \times 2^3 + 1 \times 2^1) = 1 \times 2^5 + 1 \times 2^4 + 1 \times 2^2 = 110100_2$

	qui s'écrit $52_{10}$ en décimal.

	!!! abstract "Cours" 
		Quand on ajoute un bit 0 à droite d'un nombre, tous les bits sont décalés vers la droite, les puissances de 2 correspondantes sont augmentées d'une unité, donc le nombre est multiplié par 2.

	De la même façon, on peut multiplier deux nombres binaires ensembles.

	!!! question "Exercice corrigé" 
		Calculer les additions suivantes en binaire :

		- $1101 \times 11$
		
		- $10101 \times 101$

		- $1000 \times 1000$

		

	??? Success "Réponse"

		$1101 \times 11 = 100111$

		$10101 \times 101 = 1101001$

		$1000 \times 1000 = 1000000$
		

