# Cheatsheet

- Fichiers
```python
with open("fichier.txt", "r", encoding="utf-8") as f:
	contenu: str = f.read()
	contenu: str = repr(f.read())
    contenu: list = f.read().splitlines()  # nouvel élément à chaque \n
    f.seek(0) # renvoie le curseur au début du fichier

with open("fichier.txt", "w/a", encoding="utf-8") as f:
	f.write(contenu)
```

- CSV
```python
import csv

# lire
with open("ransomeware_iocs.csv") as f:
	iocs = [row for row in csv.reader(f)]

# écrire depuis une liste
with open("file.csv", "w") as f:
	writer = csv.writer(f)
	writer.writerows(maliste)

# écrire depuis un dictionnaire
with open("newfile.csv", "w") as f:
	entetes = mondictionnaire[0].keys() # récupère les headers et les met en keys
	writer = csv.DictWriter(f, fieldnames=entetes) # créé un objet DictWriter inluant le header
	writer.writeheader() # écrit le hearder
	writer.writerows(ship_dict) # écrit les données par ligne
```

- JSON
```python
import json  

# lire et enregistrer dans une variable
with open("json_newships.json", "r") as f:
	ships: dict = json.load(f)  

# écrire depuis un dictionnaire
with open("newfile.json", "w") as f:
	json.dump(mondictionnaire, f, indent=4)
```

- Pathlib
	- voir directement dans le cours

# Intro

> [!warning] Sous Windows :
> - soit inverser les backslashes en slashes `\\` → `/`
> - soit utiliser les raw strings avec un `r` : `chemin = r"M:\\Python”` </aside>

# Ouvrir, lire un fichier

Pour lire ou modifier un fichier il faut :
- l’ouvrir
- lire/modifier le ficher
- le fermer

Sans la fermeture du fichier, l’exploitation du fichier n’est pas complète et cela créera une erreur
```python
f = open(chemin, "r")
     # code
f.close()
```

On peut ouvrir le fichier uniquement dans le bloc d’instruction `with`. Pas besoin de fermer le fichier
```python
with open(chemin, "r", encoding="utf-8") as f:
    # code
```

## Les modes d’ouverture d’un fichier

l’argument `“r”` correspond au mode d’ouverture du fichier qui peuvent être les suivants

| Operateur       | Fonction | Description                                                                                                                                                         |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| r               | read     | Ouvre un fichier en *lecture uniquement*. Le pointeur est placé au début du fichier. C'est la valeur par défault.                                                   |
| w               | write    | Ouvre un fichier en *écriture uniquement*. Écrase le contenu du fichier s'il existe déjà, crée un nouveau fichier sinon. Le pointeur est placé au début du fichier. |
| a               | append   | Ouvre un fichier en écriture uniquement. Le pointeur est placé à la fin du fichier s'il existe, sinon un nouveau fichier est créé.                                  |
| rb / wb / ab    | binary   | Ouvre le fichier en mode *binaire* (lecture des octets au lieu des caractères).                                                                                     |
| r+ / w+ / a+    |          | Ouvre le fichier en lecture et en écriture.                                                                                                                         |
| r+              |          | Erreur si le fichier n’existe pas, <br>pointeur au début, <br>données existantes remplacées (fichier non tronqué à zéro).                                           |
| w+              |          | fichier créé si n’existe pas, <br>pointeur au début, <br>données existantes écrasées (fichier tronqué à zéro).                                                      |
| a+              |          | fichier créé si n’existe pas, <br>pointeur à la fin, <br>données ajoutées aux existantes.                                                                           |
| rb+ / wb+ / ab+ |          | Combinaison des précédents en binaire.                                                                                                                              |

```python

chemin = r"C:\\User\\Documents\\mon_texte.txt"

f = open(chemin,"r", encoding='utf-8') # ouverture
	  contenu = f.read()               # lecture
f.close()                              # fermeture

with open(chemin, "r", encoding='utf-8') as f: # ouverture auto
    contenu = repr(f.read())                   # retourne une chaine de caractère brute (avec les /n par exemple)
    contenu = f.read().splitlines()            # retourne une liste avec à chaque \n un nouvel élément de liste
```

## Parser et lister chaque ligne d'un fichiers

```python
with open("auth.log") as f:
	logs = [l.strip() for l in f.readlines()]

['10 Oct 2022 15:22:31 - User admin logged in',
 '10 Oct 2022 15:25:10 - User bob logged in',
 '10 Oct 2022 16:02:24 - User admin logged out']
```
## Écrire dans un fichier

1. Stocker le chemin dans une variable
2. Ouvrir le fichier en mode append
3. Écrire (str ou variable contenant du texte)
4. Renvoyer le curseur au début si on souhaite lire par la suite
```python
fichier = r"M:\\Python\\mon fichier.txt"

# ajouter un texte dans le fichier f
with open(fichier, "a", encoding='utf-8') as f:  
    f.write("\\n\\nBonjour")
	f.seek(0) # renvoyer le curseur caractère 0
	print(f.read())
```

<aside> ⚠️ Si on souhaite écrire puis lire le fichier, il est préférable de rouvrir le fichier dans un autre bloc en lecture seule, surtout avec les fichiers JSON

</aside>


# Le module Pathlib, la classe Path
Historiquement, on utilisait des modules comme le module `os`, `glob` ou encore `shutil` pour exécuter des opérations de création, suppression et gestion des fichiers.

Beaucoup plus simple à utiliser, La classe `Path` permet de créer un objet représentant un chemin vers un fichier ou un dossier de notre ordinateur. Ce chemin peut exister ou ne pas exister sur notre disque dur, ce n'est pas un prérequis.

## Concaténation des chemins
Pour concaténer des chemins, c'est très simple, il suffit d'utiliser un slash `/` (peu importe l'OS)
```python
from pathlib import Path

home = Path.home()              
	# PosixPath('/Users/thibh/')
documents = home / "Documents"  
	# PosixPath('/Users/thibh/Documents')
```

On peut également utiliser la méthode `joinpath` sur un objet `Path`. Ça peut être pratique si vous avez par exemple une liste de dossiers que vous souhaitez concaténer (grâce à l'unpacking et à l'opérateur splat `*`) :
```python
from pathlib import Path

home = Path.home()    
	# PosixPath('/Users/aelphi/')

dossiers = ['Projets', 'Django', 'blog']
home.joinpath(*dossiers)  
	# PosixPath('/Users/aelphi/Projets/Django/blog')
```
## Extraire les éléments du chemin
```python
from pathlib import Path

P = Path(”/users/vietsou/Documents/index.html)

P.name      # nom du fichier (index.html)
P.parent    # dossier parent (/users/aelphi/Documents)
P.stem      # stem (index)
P.suffix    # extension avec le point (.html)
P.suffixes  # renvoie une liste de suffixes si plusieurs existent :
               # (ex: ['.tar', '.gz'])
P.parts     # renvoie un tuple ("/", "Users", "aelphi", "documents", "index.html")
```
## Vérifier existence et le type de chemins
```python
P.exists()  # revoie True si le fichier existe
P.is_dir()  # renvoie True si P est un répertoire
P.is_file() # renvoie True si P est un fichier
```
## Créer et supprimer des dossiers
```python
from pathlib import Path
import shutil

dossier = Path("/Users/aelphi/Documents/Projets/SiteWeb")

dossier.mkdir()               # créer un dossier (erreur si le dossier existe)
dossier.mkdir(exist_ok=True)  # pour palier à l'erreur
dossier.mkdir(parents=True)   # si la hierarchie n'existe pas encore

dossier.rmdir()           # supprime le dossier (si vide)
shutil.rmtree(dossier)    # supprime un dossier non vide       
```
## Créer, lire et écrire dans un fichier
```python
from pathlib import Path

fichier = Path("/Users/thibh/Documents/SiteWeb/index.html")

fichier.touch() # créé le fichier
fichier.unlink() # supprime le fichier

fichier.write_text("Accueil du site")

fichier.read_text()
	# Accueil du site
```
## Scanner un dossier
### avec iterdir()
```python
from pathlib import Path

for f in Path.home().iterdir():
	print(f.name) # itérer à travers un dossier

dossiers = [d for d in Path.home().iterdir() if d.is_dir()]
# itère dans home et affiche d si d est un dossier
```
### avec glob et rglob
```python
from pathlib import Path

for f in Path.home().glob("*.png"):
	print(f.name)

for f in Path.home().rglob("*.png"):
	print(f.name)
```

# Les fichiers CSV

- importert la bibliothèque csv avec `import csv`
- Les fichiers **csv** sont des données séparées par des virgules

## Lire un fichier CSV
### csv.reader()

 `csv.reader()` va itérer sur `coucou` et retourner une liste de lignes
 
```python
import csv

with open("coucou.csv") as coucou:
	iocs = [row for row in csv.reader(coucou)]

[['jour', ' description', ' fin'], 
['bla0', ' blabliblo0', ' et voila0'], 
['bla1', ' blabliblo1', ' et voila1'], 
['bla2', ' blabliblo2', ' et voila2'], ...
```

### csv.DictReader()

`csv.DictReader()` va itérer sur `coucou` et retourner un dictionnaire en prenant la headerline en guise de clé

```python
import csv

with open("coucou.csv") as coucou:
iocs = [row for row in csv.DictReader(coucou)]

# retourne
[{'jour': 'bla0', 'description': ' blabliblo0', 'fin': ' et voila0'},
 {'jour': 'bla1', 'description': ' blabliblo1', 'fin': ' et voila1'},
 {'jour': 'bla2', 'description': ' blabliblo2', 'fin': ' et voila2'}, ...

```

### Filtrage
Pour filtrer un colonne, on peut transformer utiliser set sur un colonne 
- **set()** permet d'enlever les doublons uniq
- **list()** permet d'utiliser `sort()` et d'obtenir des résultats uniques

```python
import csv

with open("coucou.csv") as coucou:
	dict_iocs = [row for row in csv.DictReader(coucou)]

# set permet d'enlever les doublons uniq
# list permet de sort() (pas utilisable sur set)

final = list(set([ioc['jour'] for ioc in dict_iocs])) 
final.sort()
print(final)

# retourne
['bla0', 'bla1', 'bla2', 'bla3', 'bla4', 'bla5', 'bla6', 'bla7', 'bla8', 'bla9']
```

## Ecrire un fichier CSV

### Depuis une liste
- on peut créer un fichier csv 
- `csv.writer()` : pour créer un objet writer
- `writerows(liste)` : pour écrire les lignes

```python
ship_list = [
	['jour', 'description', 'fin'], 
	['bla0', 'blabliblo0', 'et voila0'], 
	['bla1', 'blabliblo1', 'et voila1'], 
	['bla2', 'blabliblo2', 'et voila2'], ...
]
```

```python
with open("new_ship_list.csv", "w") as f:
	writer = csv.writer(f)
	writer.writerows(ship_list)
```

### Depuis un dictionnaire

- avec un dictionnaire en entrée, 
- `keys()` : pour récupérer les clés
- `csv.DictWriter(dictionary, fieldnames)` : pour créer un objet DictWriter et inclure le header qu'on a récoltés avec `keys()` juste avant
- `writeheader()` : pour écrire le header
- `writerows(dictionnaire)` : pour écrire les lignes

input
```python
ship_dict = [
    {"name": "Titanic", "type": "Ocean Liner", "year_built": 1912, "passenger_capacity": 2435},
    {"name": "Queen Mary", "type": "Ocean Liner", "year_built": 1936, "passenger_capacity": 2139},
    {"name": "USS Enterprise", "type": "Aircraft Carrier", "year_built": 1960, "passenger_capacity": 4600},
    {"name": "Allure of the Seas", "type": "Cruise Ship", "year_built": 2010, "passenger_capacity": 6296},
    {"name": "HMS Victory", "type": "Warship", "year_built": 1765, "passenger_capacity": 850}
]
```

code
```python
with open("new_ship_list.csv", "w") as f:
	fieldnames = ship_dict[0].keys() # récupère les headers et les met en keys
	writer = csv.DictWriter(f, fieldnames=fieldnames) # créé un objet DictWriter 
	writer.writeheader()
	writer.writerows(ship_dict)
```

output
```csv
name,type,year_built,passenger_capacity
Titanic,Ocean Liner,1912,2435
Queen Mary,Ocean Liner,1936,2139
USS Enterprise,Aircraft Carrier,1960,4600
Allure of the Seas,Cruise Ship,2010,6296
HMS Victory,Warship,1765,850
```
![[Pasted image 20241111221225.png]]

# Les fichiers JSON

## Théorie

JSON est un format de données standardisé qui est indépendant du langage de programmation. 

- La structure la plus extérieure est un objet, dénoté par des accolades `{}`.
- Les objets contiennent des **paires clé-valeur**, 
	- où la **clé** est une chaîne de caractères 
	- et la **valeur** peut être une chaîne de caractères, un nombre, un objet, un tableau, un booléen ou null.
- Les clés et les chaînes de caractères sont écrites entre guillemets doubles `"`.
- Les objets peuvent être imbriqués dans d'autres objets.
- Les **tableaux** sont écrits entre crochets `[]` et peuvent contenir plusieurs valeurs de n'importe quel type.
- `Null` est utilisé pour représenter une non-valeur.

Même chose mais avec les fichiers JSON qui vont pouvoir garder la même structure qu’à l’intérieur de python, et garder les types 

```json
{
  "cours": {
    "titre": "Introduction au JSON",
    "instructeur": {
      "nom": "John Doe",
      "email": "johndoe@example.com"
    },
    "duree": "4 semaines",
    "sujets": ["Structure JSON", "Syntaxe JSON", "Utilisation du JSON"],
    "prerequis": null
  }
}
```

## Ecrire un fichier JSON à partir d'un dictionnaire
- load de données à partir d'un fichier csv
	- création d'un dicitonnaire
- `json.dump(dictionnaire, objet_json_opened)` : ecrit les données du dictionnaire dans le fichiers


```python
import csv

with open("new_ship_list.csv") as f:
	reader = csv.DictReader(f)
	ships = [i for i in reader]

  
import json  

with open("json_newships.json", "w") as json_file:
	json.dump(ships, json_file, indent=4)
```

output
```json
[
	{
		"name": "Titanic",
		"type": "Ocean Liner",
		"year_built": "1912",
		"passenger_capacity": "2435"
	},
	{
		"name": "Queen Mary",
		"type": "Ocean Liner",
		"year_built": "1936",
		"passenger_capacity": "2139"
	},
	...
```

## Charger des fichiers json dans une variable

```python
import json

with open("json_newships.json", "r") as f:
	ships: dict = json.load(f)  
```
