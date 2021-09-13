# Les fonctions

## Définition et appel de fonction

Une fonction se défini à l'aide du mot clé `def`

```python

def add_2(n):
    return n + 2
```

L'appel de cette fonction se fait de cette manière suivante:

```python
add_2(1) # retourne 3
```

## Arguments par défaut

On peut ajouter des arguments avec des valeurs par défaut aux fonctions.

```python
def pow(n, exp = 2):
    return n ** exp
```
Cette fonction retourne n à la puissance exp, elle peut être utilisé de deux manières.

```python
pow(10) # retourne 10 ^ 2 = 100

pow(3, 3) # retourne 3 ** 3 = 27
```
Cette fonction prend donc au minimum un argument, avec le second qui est optionnel, car il a une valeur par défaut.

## Fonction anonyme

Les mot clé `lambda`permet la création d'une fonction anonyme. Cependant, les fonctions anonymes sont limités à des expressions, on ne peut donc pas faire d'assignation ou d'utiliser des déclaration du type `while`, `if` etc...

Par ces contraintes l'utilisation des fonctions anonymes reste limité, une des utilisations possibles de ces fonctions est en tant qu'argument d'une fonction.

```python
l = [1, 2, 3, 4]

result = map(lambda x: x*2, l)

print(list(result))
```

Dans ce code on définit d'abord une liste d'entier, on utilise ensuite la fonction map qui prend en argument une fonction et un itérable et qui va appliquer cette fonction à chaque élément de l'itérable. Ici la fonction qu'on applique à chaque élément de la liste est la fonction anonyme `lambda x: x*2` qui pour chaque x retourne x*2.

Cette fonction retourne un objet map, qu'on convertit ensuite en liste pour pouvoir afficher le résultat. Ici le résultat sera `[1, 2, 3, 4]`.

## Annotations de fonctions

Python donne la possibilité d'ajouter des métadatas aux paramètres des déclarations de fonction et de la valeur de retour.

```python
def hello(name:str = "jack") -> str:
    return "hello " + name

def fact(n:"int >= 0") -> int:
    if (n == 0):
        return 1
    return n * fact(n - 1) 
```

Chaque argument peut avoir une annotation précédé par `:` (et s'il y a une valeur par défaut il précède le `=`). Pour annoter la valeur de retour on ajoute après la parenthère fermante de la déclaration de fonction tout d'abord `->`, puis le type. L'expression peut-être de n'importe quel type, comme `str`, `int` ou un string.

Les annotations ne sont pas faite pour faire une vérification des types lors de l'execution du code, les informations sont juste stockées dans l'attribut `__annotations__`, et n'ont donc aucun sens pour l'interpréteur python. Cependant ces informations peuvent être utilisées par les IDE par exemple.

## *args et **kwargs

