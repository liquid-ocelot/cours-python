# Classes

Dans ce chapitre on fera la distinction entre une classe et un objet qui est une instance d'une classe. 

## Définir une classe

On va commencer simplement avec une classe définissant une personne.

```python


class Person: #1

    def __init__(self, firstname, lastname, age): #2
        self.firstname = firstname #3
        self.lastname = lastname
        self.age = age
```
`#1` Cette ligne défini la classe, donc avec le mot clé class et le nom de la classe (par convention, ce nom doit être écrit en notation CamelCase).

`#2` Méthode spéciale qui défini le constructeur, les méthodes dans les classes commencent par le même mot clé que les fonctions `def`, le nom `__init__` est le nom attribué pour le constructeur de la classe. On a ensuite les arguments du constructeur, ici firstname, lastname et age sont des arguments définis par l'utilisateur, contrairement au self qui n'est pas renseigné par l'utilisateur, qui désigne l'objet qui est initialisé.

`#3` Les trois instructions contenues dans le constructeur définient les atribues de la classe en reprenant les arguments du constructeur.

## Instancier une classe

Pour instancier la classe défini précédemment, le code suivant suffit:

```python
personne = Person("John", "Doe", 21)
```

Ici `Person("John", "Doe", 21)` fait appelle au constructeur `__init__`, qui retourne une instance qui sera contenue dans la variable `personne`.

## Accéder aux attributs

On va accéder aux  attributs de l'objet défini précédemment.

```python

print(personne.age) #Va print 21

print(personne.firstname) #Va print John

#On peut aussi redéfinir les attributs

personne.age = 35 #On change la valeur de l'attribut age de personne

```

## Définir une méthode

On va reprendre la définition de la classe Person pour y ajouter deux méthodes.

```python
class Person: #1

    def __init__(self, firstname, lastname, age): #2
        self.firstname = firstname #3
        self.lastname = lastname
        self.age = age

    def bonjour(self):
        print("Bonjour " + self.firstname)

    def getAge(self):
        return self.age
```

On a ajouté ici deux nouvelles méthodes, on les utilisera de cette manière: 

```python
personne = Person("John", "Doe", 21)

personne.bonjour() #l'appelle de cette méthode affichera "Bonjour John" dans la console

age = personne.age() #l'appelle de cette méthode retourne l'age de la personne, donc la variable age contiendra 21
```

## Attribut statique

Contrairement à un attribut non statique, qui est lié à une instance de la classe, un attribut statique est un attribut sur la classe, qui n'est donc pas rattaché à une instance en particulier mais qui est partagé par toutes les instances. Pour en faire la démonstration, on va une fois de plus modifier la classe Person.

```python
class Person: 

    count = 0 #1

    def __init__(self, firstname, lastname, age): 
        self.firstname = firstname 
        self.lastname = lastname
        self.age = age
        Person.count += 1 #2

    def __del__(self): #3
        Person.count -= 1
```

Ici on utilise un attribut statique pour faire le compte du nombre d'instance de la classe Person.
`#1` On défini dans le corps de la classe l'attribut count qu'on initialise à 0.

`#2` Dans le constructeur on ajoute une ligne pour incrémenter le compte, à noter que pour accéder à l'attribut statique on fait appelle à la classe `Person` et non pas l'objet `self`.

`#3` Cette méthode spéciale est la méthode appelé à la destruction d'un objet, donc ici on décrémente de 1.

## Méthode statique

Les méthodes statiques sont des méthodes qui n'ont pas besoin d'instance de la classe pour être appelé. C'est un moyen de créer des espaces de noms.

```python
class Person: 

    def __init__(self, firstname, lastname, age): 
        self.firstname = firstname 
        self.lastname = lastname
        self.age = age

    @staticmethod
    def est_majeur(age):
        if(age > 17):
            return True
        return False

```

Pour definir une méthode statique il faut ajouter le décorateur `@staticmethod`. Cette méthode ne prend pas d'argument `self`.

L'appel de la méthode se fait de cette manière:

```python
Person.est_majeur(10) #retourne False

Person.est_majeur(21) #retourne True
```

## Méthode de classe

Une méthode de classe est une méthode qui au lieu de prendre un objet `self` en argument, prend la classe en argument `cls`. En python, on ne peut pas surcharger les fonctions (c'est à dire que plusieurs fonctions ne peuvent pas porter le même nom), donc on ne peut pas avoir plusieurs constructeurs pour une classe. Les méthodes de classes offrent un moyen détourné pour faire d'autres constructeurs.

```python
class Person: 

    def __init__(self, firstname, lastname, age): 
        self.firstname = firstname 
        self.lastname = lastname
        self.age = age

    @classmethod
    def naissance(cls, firstname, lastname):
        return cls(firstname, lastname, 0)
```
Dans la methode naissance, on fait appelle au constructeur de la classe, qui retourne une instance de la classe.

```python
enfant = Person.naissance("Jane", "Doe")
#la variable enfant va contenir une personne nommée Jane Doe avec un age de 0
```