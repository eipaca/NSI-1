# Constructions élémentaires

En Python, l’indentation, ou décalage vers la droite du début de ligne, délimite les séquences d’instructions et facilite la lisibilité en permettant d’identifier des blocs. La ligne précédant une indentation se termine toujours par le signe deux-points.
En Python, on utilise 4 espaces (ou Tab ) pour faire une indentation (on pourrait aussi utiliser un seul ou plusieurs espaces  mais il faut être consistant).

##	Instructions conditionnelles
Une instruction conditionnelle exécute, ou pas, une séquence d’instructions suivant la valeur d’une condition (une expression booléenne qui prend la valeur `True` ou `False`).
```py
if condition:
    instructions
```
Par exemple, ce programme détermine le stade de la vie d’une personne selon son age.
```py
age = int(input("Quel age avez-vous ?"))
if age >= 18:
    stade = "adulte"
    print(f"Vous êtes un {stade}")
    print(f"Vous avez {age} ans")
```
Note : ne pas oublier les  deux points « `:` » après la condition et l’indentation après.
L’indentation détermine la séquence à exécuter (ou pas), dans ce cas les trois instructions qui suivent. Quand la condition (l’expression booléenne) `age >= 18` n’est pas vérifiée, aucune des trois instructions n’est exécutée. 

On peut choisir de ne pas indenter l’instruction `print(f"Vous avez {age} ans")`, elle ne fera plus partie de l’instruction conditionnelle et sera exécutée dans tous les cas. Par contre si on n’indentait pas l’instruction `print(f"Vous êtes {stade}")`, la variable `stade` ne serait pas définie quand la condition n’est pas vérifiée et dans ce cas on aurait un message erreur.
```py
age = int(input("Quel age avez-vous ?"))
if age >= 18:
    stade = "adulte"
    print(f"Vous êtes {stade}")
print(f"Vous avez {age} ans")
```
La structure if-else permet de gérer le cas où la condition est fausse :
```py
if condition:
    instructions
else :
    instructions_sinon
```
Note: `else` n’a pas de condition, il est toujours suivi des deux points « `:` » 
```py
age = int(input("Quel age avez-vous ?"))
if age >= 18:
    stade = "adulte"
else:
    stade = "enfant"
print(f"Vous êtes {stade}")
print(f"Vous avez {age} ans")
```
Dans ce cas, la variable `stade` est toujours définie, on peut ne plus indenter l’instruction `print(f"Vous êtes {stade}")`. 
La structure `if-elif-else` permet de remplacer des instructions conditionnelles imbriquées pour gérer plusieurs cas distincts:
```py
if condition_1:
    instructions_si_1
elif condition_2:
    instructions_si_2
elif condition_3:
    instructions_si_3
…
else :
    instructions_sinon
```
Ces deux programmes font la même chose:

if age >= 18:
    stade = "adulte"
else:
    if age >= 12:
        stade = "ado"
    else:
        if age >= 2:
            stade = "enfant"
        else :
            stade = "bébé"
print(f"Vous êtes {stade}, vous avez {age} ans")	if age >= 18:
    stade = "adulte"

elif age >= 12:
    stade = "ado"

elif age >= 2:
    stade = "enfant"
else :
    stade = "bébé"
print(f"Vous êtes {stade}, vous avez {age} ans")
Dès qu’une condition est vérifiée, le programme ne teste pas les conditions elif suivantes ni else mais saute directement à la fin du bloc conditionnel, ici print(f"A {age} ans, vous êtes {stade}"). Par exemple, si on affecte la valeur 10 à la variable age, le programme exécute le bloc elif age >= 12:….mais pas les blocs suivants elif age >=2 :…. ni stade = "bébé" :…. 
Rappel : il faut éviter les conditions d’égalité avec les nombres de type float. Par exemple : 
if 2.3 - 0.3  == 2:
    print('Python sait bien calculer avec les float')
else:
    print('Python ne sait pas bien calculer avec les float')
PEP8 : Eviter de comparer des variables booléennes à True ou False avec == ou avec is. On écrit:
cond = True
if cond:
	print("la condition est vraie"
mais pas  if cond == True:  ni  if cond is True:


