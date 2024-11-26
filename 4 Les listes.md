### Quand doit-on utiliser une liste ?

- Est-ce que j'ai besoin d'associer une valeur à une clé ? Oui ?→ **Dictionnaire**
- Est-ce que j'ai besoin de modifier ma structure de données ? Non → **Tuple**
- Est-ce que j'ai besoin de garder les éléments dans le même ordre ? Non → **Set**
- Pour toutes les autres possibilités → **Liste**

### Parenthèse sur les sets

J'utilise la fonction `set()` pour convertir ma liste `villes` d'origine en `set`, ce qui va avoir pour effet de retirer tous les doublons car les sets ne les acceptent pas. Ensuite je n'ai plus qu'à reconvertir ce set en liste pour la récupérer sans les doublons.

1. `villes = ['Paris', 'Lille', 'Lyon', 'Paris', 'Strasbourg']`
2. `ville = list(set(villes))`
3. `print(ville) # ['Lyon', 'Lille', 'Strasbourg', 'Paris']`

### Créer une liste
- Avec les crochets → `[]`
- Avec le constructeur → `list()`

```python
liste_vide = []
liste_vide = list()
```

Généralement on utilise `list()` quand tu as besoin de convertir un autre objet en liste :

```python
site = 'Docstring'
site_to_liste = list(site)
print(site_to_liste)  
	-> ['D', 'o', 'c', 's', 't', 'r', 'i', 'n', 'g']
```

### Accéder à des éléments
- `liste[indice]` → Retourne l'élément associé à l'indice
- `liste[début:fin:pas]` → Retourne le ou les éléments en fonction de l'intervalle précisé
#### Indices
```python
liste = [1,2,3,4,5,6,7,8]
print(liste[0])  # 1er élément (1)
print(liste[1])  # 2ème élément (2)
print(liste[-1]) # dernier élément (8)
```
#### Slicing
Cela te permet de créer un intervalle de sélection dans ta liste et de préciser éventuellement un pas si tu souhaites récupérer un élément sur deux par exemple.

```python
liste = [1,2,3,4,5,6,7,8]

print(liste[0:2]) # [1,2]
print(liste[0::2]) # [1,3,5,7]
print(liste[4:]) # [5,6,7,8]
print(liste[:]) # [1,2,3,4,5,6,7,8]
print(liste[:-1]) # [1,2,3,4,5,6,7]
print(liste[::-1]) # inverse la liste
```

**(!)** l'indice de début est **inclusif** tandis que l'indice de fin est **exclusif.**
### Ajouter des éléments
Python dispose de plusieurs méthodes :
- `.append(item)`
	- Ajoute un item à la fin de la liste
- `.insert(index, item)`
	- Ajoute un item à la position indiquée en paramètre
- `.extend(iterable)`
	- Ajouter tous les items de la collection dans ta liste
#### append(item)`
C'est la méthode la plus connue et celle qui est le plus souvent utilisée :
```python
liste.append(9)
```

#### insert(index, item)
Beaucoup moins utilisée mais qui peut s'avérer utile:
```python
villes = ['Paris', 'Lille', 'Lyon']

villes.insert(1, 'Strasbourg')
villes.insert(-1, 'Rennes')

print(villes)  
	-> ['Paris', 'Strasbourg', 'Lille', 'Lyon', 'Rennes']
```

#### extend(iterate)

```python
liste1 = [1,2,3,4]
liste2 = [5,6,7,8]

liste1.extend(liste2)

print(liste1)  
	-> [1,2,3,4,5,6,7,8]
```

### Modifier des éléments

Une liste est muable (modifiable)
#### liste[indice] = valeur
→ Assigne une nouvelle valeur à l'objet

```python
villes = ['Paris', 'Lille', 'Lyon']
villes[1] = 'Strasbourg'
	-> ['Paris', 'Strasbourg', 'Lyon']
```
#### liste[début:fin] = [valeur1, valeur2, ...]
→ Assigne des nouvelles valeur sur l'intervalle donnée

```python
villes = ['Paris', 'Lille', 'Lyon']
villes[1:] = ['Strasbourg', 'Rennes']
	-> ['Paris', 'Strasbourg', 'Rennes']
```

### Supprimer des éléments

Il existe trois façons de supprimer un élément :

#### del liste[indice]
→ Supprime un ou plusieurs éléments d'une liste. 
Peut aussi être utilisé pour **détruire** complètement une liste.

```python
villes = ['Paris', 'Lille', 'Lyon']

del villes[0]
print(villes)  # ['Lille', 'Lyon']

del villes
print(villes)  # NameError
```
#### liste.pop(index)
→ Retire un élément de la liste. 
Si pas d'indice précisé, cela retire automatiquement le dernier élément. 
Et surtout, cela permet de récupérer l'élément supprimé.

```python
villes = ['Paris', 'Lille', 'Lyon']

ma_ville = villes.pop(1)

print(villes)    # [’Paris', 'Lyon']
print(ma_ville)  # Lille
```
#### liste.remove(item)
→ Supprime un élément de la liste.
**/!\\** Un élément non dans la liste qui serait appelé par pop crée une *ValueError*
```python
villes = ['Paris', 'Lille', 'Lyon']
villes.remove('Paris')
print(villes)  # ['Lille', 'Lyon']
```

```python
villes = ['Paris', 'Lille', 'Lyon']
villes.remove('Marseille')
print(villes)  # ValueError
```