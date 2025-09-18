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
