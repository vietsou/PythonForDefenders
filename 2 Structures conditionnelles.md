## `if`

### Principe

En Python, on écrit une structure conditionnelle grâce au mot clé `if` :

```python
if condition:
     // code
... suite du code
```

Python exécute le code qui se trouve à l'intérieur de la structure conditionnelle uniquement si la `condition` est vraie (`True`). Si la condition n’est pas vérifiée, le code n'est pas exécuté.
*note : En Python, `None` et `0` sont des valeurs interprétées comme `False`*

### Syntaxe
- ajouter **deux points** `:`
- **indenter** le code à l'intérieur de la structure conditionnelle

```python
 age = 24 
 MAJORITE = 18

 if age >= MAJORITE:
     print("Je suis majeur !")

```

## `if` / `else`

Si la condition est False, c’est le code sous else qui va s’exécuter.

```python
age = 15 
MAJORITE = 18

if age >= MAJORITE:
    print("Je suis majeur !")
else:
    print("Je suis mineur...")
```

## `if` / `elif` / `else`

### Principe

Permet d'ajouter des conditions supplémentaires à une structure conditionnelle avant de passer au `else`.
On peut ajouter autant de `elif` que nécessaire.

<aside> 💡 si une des conditions est `True` et que le code est exécuté, toute la boucle conditionnelle s’arrête.

</aside>

```python
age = 18 
MAJORITE = 18 
if age > MAJORITE:
    print("Je suis majeur !")
elif age == MAJORITE:
    print("Tout juste majeur depuis aujourd'hui")
else:
    print("Je suis mineur..")
  
print("J'ai", age, "ans !")
```

### Imbriquer des structures conditionnelles
On peut imbriquer une structure conditionnelle dans une autre structure, puis dans une autre, etc... On appelle ça de **l'imbrication** en français (« **nesting** » en anglais). Cela permet de préciser encore plus la condition.

### Syntaxe

Il suffit de déclarer votre nouvelle structure à l'intérieur de la précédente avec une **indentation.**

```python
 age = 18 
 MAJORITE = 18

 if age >= MAJORITE:
     print("Je suis majeur !")
     if age == MAJORITE:
         print("Tout juste majeur depuis aujourd'hui")
 else:
     print("Je suis mineur..")
```

## Les Opérateurs ternaires
### Syntaxe
```python
variable = valeur_si_vrai if condition else valeur_si_faux
```
### Exemple
```python
age = 20
majeur = True if age >= 18 else False
# majeur = True
```
