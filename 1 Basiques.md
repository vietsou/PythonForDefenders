## Les types natifs

#### Classes d’objet:

- `str` = chaine de caractères
- `int` = nombre entier
- `float` = nombre décimal
- `bool` = True ou False

Ainsi, on peut convertir une chaîne de caractères en nombre entier ou vice-versa :

- `str(5)` -> `"5"`
- `int("5")` -> `5`

## Les variables

### Affectation

#### simple
`a = 5`
#### parallèle
`a, b = 5, 10`
#### multiple
`a = b = 5`
### Singleton et 'small integer caching'

Le mot **Singleton** fait référence au fait qu'**un objet est unique.**
- `True` et `False` ou l'objet `None`.
- les **nombres compris entre `-5` et `256`**
- les **chaînes de caractères courtes.**

-> on se réfère toujours au **même objet en mémoire.**

### Règles et conventions de nommage
ref : **PEP8**.

- `website_url` 
- `number_of_students`
- `bank_account_id`
- `name`
### Liste des mots réservés à Python
```
1. False
2. None
3. True
4. and
5. as
6. assert
7. break
8. class
9. continue
10. def
11. del
12. elif
13. else
14. except
15. finally
16. for
17. from
18. global
19. if
20. import
21. in
22. is
23. lambda
24. non local
25. not
26. or
27. pass
28. raise
29. return
30. try
31. while
32. with
33. yield
```
## Type d'objets et conversion
https://docs.python.org/3/library/stdtypes.html
### Types
#### Null
- None
#### Numérique
- int
- float
#### Booléen
- bool
#### Séquence de texte
- str
#### Séquentiels
- dict
- tuple
- list
- range
#### Séquences Binaires
- bytes
- bytearray
- memory view
#### Set
- set
- frozenset

### Concaténation avec str()
**str()** transforme son argument en chaîne de caractères. 
Ceci est la méthode pour concaténer des *str* et des *int* ensembles

```python
nombre = 15
resultat = "Le nombre est " + str(nombre)
print(resultat)
	-> Le nombre est 15
```
### Vérification avec isdigit() et is_integer()
**isdigit()** sert à vérifier si l'argument passé avant ne contient une donnée numérique
**is_integer()** vérifie si l'argument est un *int*
```python
(3.2).isdigit()
	-> true
(3.2).is_integer()
	-> false
```
### Conversion et fonction avec type()
```python
a = "5"
b = int(a)

print(b)
print(type(b))

	-> 5
	-> <class 'int'>
```
### fstring
Le **fstring** permet d’insérer la valeur d’une ou plusieurs variables à l’intérieur d’une chaîne de caractères.
```python
liste = ['Pommes', 'Poires', 'Bananes']
print(f"Voici votre liste de courses : {liste}")
	-> Voici votre liste de courses : ['Pommes', 'Poires', 'Bananes']
```
### Concaténation possible
```python
nombre = 15

print("Le nombre est : ", nombre)           // concaténation
print("Le nombre est : " + str(nombre))     // conversion et concaténation

print(f"Le nombre est : {nombre}")          // fstring

print("Le nombre est : %d" % nombre)        // placeholder avec %
print("Le nombre est : {}".format(nombre))  // méthode format()
```

### bytes & bstring
Enregistre la chaine sous formes de bytes
```python
string_word = "coucou" # type is str
in_bytes_word = b"coucou" # type is bytes
```

#### decode()
[lien](https://www.geeksforgeeks.org/python-strings-decode-method/)
```python
in_bytes_word.decode() # decode from bytes to strings
```

#### encode()
The `encode()` method encodes the string, using the specified encoding. 
If no encoding is specified, UTF-8 will be used. [lien W3shcool](https://www.w3schools.com/python/ref_string_encode.asp)
```python
txt = "My name is Ståle".encode() # encode from string to bytes 
	-> b"My name is St\xc3\xe5le"
```

## Interagir avec l'utilisateur
### Fonction input()
```python
age = input("Quel âge avez-vous ? ")
	-> Quel âge avez-vous ? 25
print(age)
	-> 25
```
## Manipuler les chaînes de caractères
### Minuscules et majuscules
```python
"Bonjour".upper()   -> BONJOUR
"Bonjour".lower()   -> bonjour

"bonjour tout le monde".capitalize()   -> Bonjour tout le monde
"bonjour tout le monde".title()        -> Bonjour Tout Le Monde
```
### Modification et tri du texte
#### replace()
Remplace *arg1* par *arg2*.

```python
"bonjour".replace("jour", "soir")  
	-> bonsoir
"a b c d e".replace(" ", "") 
	-> abcde
```
#### strip(), rstrip(), lstrip()
- Sans argument : supprime les espaces vides.
- Avec argument : supprime tous les caractères présents dans l'arg1 en partant du début, jusqu'à ne plus trouver de caractère à enlever (ici jusqu'au *b*). Dès lors, il arrête et recommence en partant de la fin de la chaîne, c'est pour cela que le *o* de *bon* est toujours présent.
```python
"   bonjour   ".strip()
	-> bonjour
"   bonjour   ".strip(" ujor")
	-> bon
```
#### split()
Permet de séparer des éléments d'une chaîne de caractère en :
1. supprimant la chaîne en argument,
2. retournant chaque élément dans une **liste**.
```python
"1, 2, 3".split(", ")
# ['1', '2', '3',]
```
#### join()
Inverse de split, il permet de joindre les éléments d'une liste dans une unique *str* en les séparant par une *str* donnée.
```python
invites = ['Max', 'Patrick', 'Yasmine',]
" - ".join(invites)

	-> Max - Patrick - Yasmine
```
### Les autres fonctions de gestion de chaîne de caractères.

|**Méthode**|**Description**|
|---|---|
|`capitalize()`|Convertit le premier caractère de la chaîne en majuscule|
|`casefold()`|Convertit la chaîne en minuscules, plus agressif que `lower()`|
|`center()`|Retourne une chaîne centrée, avec des espaces ou un caractère spécifié|
|`count()`|Retourne le nombre de fois qu'une sous-chaîne apparaît dans la chaîne|
|`encode()`|Retourne une version encodée de la chaîne|
|`endswith()`|Retourne `True` si la chaîne se termine par la valeur spécifiée|
|`expandtabs()`|Change la taille des tabulations dans la chaîne|
|`find()`|Cherche une sous-chaîne et retourne l'index de sa première occurrence, ou `-1` si non trouvée|
|`format()`|Formate une chaîne en utilisant des variables ou des paramètres|
|`index()`|Cherche une sous-chaîne et retourne l'index de sa première occurrence|
|`isalnum()`|Retourne `True` si tous les caractères sont alphanumériques|
|`isalpha()`|Retourne `True` si tous les caractères sont des lettres|
|`isdecimal()`|Retourne `True` si tous les caractères sont des nombres décimaux|
|`isdigit()`|Retourne `True` si tous les caractères sont des chiffres|
|`isidentifier()`|Retourne `True` si la chaîne est un identifiant valide en Python|
|`islower()`|Retourne `True` si tous les caractères sont en minuscule|
|`isnumeric()`|Retourne `True` si tous les caractères sont numériques|
|`isprintable()`|Retourne `True` si tous les caractères sont imprimables|
|`isspace()`|Retourne `True` si tous les caractères sont des espaces|
|`istitle()`|Retourne `True` si chaque mot commence par une majuscule|
|`isupper()`|Retourne `True` si tous les caractères sont en majuscule|
|`join()`|Joint les éléments d'un itérable avec le caractère spécifié|
|`ljust()`|Retourne une chaîne justifiée à gauche|
|`lower()`|Convertit la chaîne en minuscule|
|`lstrip()`|Supprime les caractères spécifiés en début de chaîne|
|`maketrans()`|Crée une table de correspondance pour la méthode `translate`|
|`partition()`|Divise la chaîne en un tuple contenant trois parties|
|`replace()`|Remplace une sous-chaîne par une autre|
|`rfind()`|Cherche une sous-chaîne et retourne l'index de la dernière occurrence|
|`rindex()`|Comme `rfind()`, mais lève une erreur si non trouvée|
|`rjust()`|Retourne une chaîne justifiée à droite|
|`rpartition()`|Divise la chaîne en un tuple contenant trois parties, en partant de la droite|
|`rsplit()`|Divise la chaîne en une liste en utilisant un séparateur, en partant de la droite|
|`rstrip()`|Supprime les caractères spécifiés en fin de chaîne|
|`split()`|Divise la chaîne en une liste en utilisant un séparateur|
|`splitlines()`|Divise la chaîne en une liste sur les retours à la ligne|
|`startswith()`|Retourne `True` si la chaîne commence par la valeur spécifiée|
|`strip()`|Supprime les caractères spécifiés en début et fin de chaîne|
|`swapcase()`|Inverse la casse des caractères (majuscules deviennent minuscules et vice-versa)|
|`title()`|Met la première lettre de chaque mot en majuscule|
|`translate()`|Applique une table de correspondance pour traduire la chaîne|
|`upper()`|Convertit la chaîne en majuscule|
|`zfill()`|Remplit la chaîne avec des zéros pour atteindre une longueur spécifiée|

## Les opérateurs de bases

### Les égalités
`=` → affectation de variable
`==` → égalité ou valeur égale
`is` → est l’objet

### Les comparaisons
`<` `<=` `>` `>=`
`!=` n’est pas égale à (différent de)
### Les opérateurs classiques
`-` `+` `*` `/` `//` `%` `**`

```python
print(11//2)   # 5  - retourne le résultat entier d’une division (division euclidienne)
print(11 % 2)  # 1  - modulo retourne le reste d'une division
print(2**5)    # 32 - exposant
```

## Le module math
### Appel du module

`import math`

Une fois le module importé, vous pouvez utiliser toutes les fonctions contenues à l'intérieur du module, en **préfixant** la fonction du nom du module. Par exemple pour calculer une racine carrée :

```python
import math

racine = math.sqrt(16)
print(racine)
# 4.0
```

### Fonctions les plus utilisés dans le module **math** :

`math.sqrt(16)` : racine carrée, donne ici 4.
`math.ceil(-4.7)` : entier immédiatement supérieur, donne ici -4.
`math.exp(2)` : exponentielle.
`math.factorial(5)` : factorielle 5, donc 120 ici (fonctionne uniquement pour les entiers positifs).
`math.floor(-4.7)` : partie entière, donne ici -5.
`math.isinf(x)` : teste si x est infini (inf) et renvoie True si c'est le cas.
`math.log(2)` : logarithme en base naturelle.
`math.log(8, 2)` : log de 8 en base 2.
`math.log10(2)` : logarithme en base 10.
`math.pow(2, 3)` : 2 puissance 3 (peut aussi s'écrire 2 ** 3).
### Fonctions trigonométriques : 
`math.sin` `math.cos` `math.tan` `math.asin` `math.acos` `math.atan` (argument en radians).
### Fonctions hyperboliques : 
`math.sinh` `math.cosh` `math.tanh` `math.asinh` `math.acosh` `math.atanh`
`math.degrees(x)` : convertit de radians en degrés.
`math.radians(x)` : convertit de degrés en radians.
### Les constantes :
pi : `math.pi` (3.14159...)
nombre d'Euler : `math.e` (2.71828...)

