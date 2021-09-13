# Les décorateurs

## Décorateurs simple

Les décorateurs sont des fonctions qui prennent en argument une fonction et qui retourne une fonction.

```python
def decorateur(func):
    def f():
        print("avant la fonction")
        func()
        print("apres la fonction")
    return f


@decorateur
def hello():
    print("hello world")
```

Dans le code précédent on définit d'abord la fonction `decorateur` qui prend en argument la fonction `func`, et qui dans son corps définit la fonction `f`. Dans cette fonction interne, on appelle la fonction `func` et des fonctions print. Enfin la fonction `décorateur` retourne la fonction `f`.

Ensuite avant la déclaration de la fonction `hello`, on utilise un décorateur en utilisant le `@` + le nom de la fonction. Donc en utilisant le décorateur `@decorateur`, on utilise la fonction `decorateur` et on passe la fonction `hello` en tant qu'argument. En utilisant ce décorateur la fonction `hello` est redéfini. 

L'exécution des décorateurs est effectué lors de la compilation du bytecode.

En executant la fonction `hello` on obtiendra le résultat suivant:

```python
hello()
>>> avant la fonction
>>> hello world
>>> apres la fonction
```