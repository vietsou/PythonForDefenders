## Installer un module

```
pipx install <nom_du_module>
```
## Le module `random`
### fonction `randint()`
```python
import random
r = random.randint(0, 5) 
	-> retournera une valeur int entre 0 et 5 inclus.
```
### fonction `uniform()`
idem `randint()` mais retourne un _float_.
### fonction `randrange()`
```python
r = random.randrange(0, 100, **10**) retournera une valeur *int* entre 0 et 100 exclus par pas de 10.
```
## Fonctions builtin et module pprint
### fonction `dir()`
`print(dir(module))` affiche toutes les fonctions appelables d’un module
### fonction `help()`
`help(random.randint)` donne du texte d’explication sur un module ou une fonction (`q` pour quitter)
### fonction `pprint()`
comme la fonction `print()` mais de façon plus lisible (en colonne)
## Le module `pathlib`

```python
from pathlib import Path

# Création d'un objet Path à partir d'un chemin de fichier ou de répertoire
p = Path('/chemin/vers/un/fichier/ou/un/répertoire')

# Vérification de l'existence d'un fichier ou d'un répertoire
print(p.exists())

# Accès aux différentes parties du chemin
print([p.name](<http://p.name/>))         # Nom du fichier ou du répertoire
print(p.parent)       # Répertoire parent
print(p.stem)         # Nom du fichier sans extension
print(p.suffix)       # Extension du fichier

# Création d'un sous-répertoire
subdir = p / 'sous-répertoire'
subdir.mkdir()

# Création d'un fichier dans ce sous-répertoire
file = subdir / 'mon_fichier.txt'
file.touch()

# Parcours des fichiers et répertoires d'un répertoire
for f in p.iterdir():
print(f)

# Lecture et écriture dans un fichier
with file.open('r') as f:
print(f.read())

with file.open('w') as f:
f.write('Nouveau contenu du fichier')
```

## Objet dit _callable_ et la fonction `callable()`

### Principe
Un objet *callable* est un objet qui peut être invoqué comme une fonction. Pour être plus clair, considérez l'objet comme une box qui peut effectuer une action spécifique lorsque vous appuyez sur un bouton 
### Syntaxe
C’est grâce aux parenthèses **`()`** que l’on peut voir si un objet est _callable_ ou non. Le module **pprint** (qui contient plusieurs fonctions) n’est pas _callable._ En revanche la fonction `pprint()` est callable.
### Erreur
`TypeError : "str" is not callable`
### Fonction callable()
Retourne `True` ou `False` selon que l'objet soit callable ou non
## les modules d’aide
### le module **dir**
Permet de voir les fonctions utilisables dans un module
### le module help
Affiche une petite aide sur une fonction en particulier

```python
import random
help(random.randint)
# randint(a, b) method of random.Random instance
    Return random integer in range [a, b], including both end points.
```

## la fonction `pprint()` du module pprint

La fonction **`pprint()`** est la fonction principale du module **pprint**. Elle prend un objet Python comme argument et **imprime une version formatée et indentée** de cet objet sur la sortie standard.

## Autres méthodes et fonctions

#### len() 
retourne la longueur d’une str ou d'une liste
#### round()
arrondi à l’entier le plus proche
#### min()
retourne le plus petit nombre d’une liste ou série, fonctionne avec l’alphabet
#### max()
inverse de min()
#### range(x)
retourne une liste de x int (de 0 à x-1)

```python
"bonjour".**len**() # 7

n = 7.43
l.**round**() = 7

nb = **range**(5)
print(nb) # [0,1,2,3,4]

print(nb.**min**()) # 0
print(nb.**max**()) # 4
```