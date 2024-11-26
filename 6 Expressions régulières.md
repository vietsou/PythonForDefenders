## Raw data vs Strings
- l'utilisation de raw strings permet de ne pas tenir compte de l'interprétation de certains caractères traduis par le système ou l'application
- importer la blbliothèque `re` pour *regular expressions*, 

```python
import re

# print de string classique
print("Is it a raw string?\nNo it isn't.")
		# Is it a raw string?
		# No it isn't.

# print de raw string
print(r"Is it a raw string?\nYes it is.")
		# Is it a raw string?\nYes it is.
```

## Définir un pattern grace à des regex

### re.compile()

Utilisation de **`re.compile()`** pour définir un pattern grâce à des regexs

```python
# email pattern : 'test@test.com'
email_pattern = re.compile(r"[a-zA-Z0-9_\-\+\. ]+\@[a-zA-Z0-9-]+\.[a-zA-Z0-9-]{2,}")

# exemple de log pattern : '10 Oct 2022 15:22:31 - User admin logged in'
log_pattern = re.compile(r"^(\d{2} [A-Z][a-z]{2} \d{4} \d{2}:\d{2}:\d{2} - User [a-z]+ .+)$")

# hash patterns
md5_pattern = re.compile(r"(?<![0-9a-f])[0-9a-f]{32}(?![0-9a-f])") # 32 caractères, et pas d'autre avant ni après
sha1_pattern = re.compile(r"(?<![0-9a-f])[0-9a-f]{40}(?![0-9a-f])")
sha256_pattern = re.compile(r"(?<![0-9a-f])[0-9a-f]{64}(?![0-9a-f])")
sha512_pattern = re.compile(r"[0-9a-f]{128}")

# ipv4 pattern
ipv4_pattern = re.compile(r"(?:[0-9]{1,3}\.){3}[0-9]{1,3}")

# domain pattern
domain_pattern = re.compile(r"(?:[A-Za-z0-9\-]+\. )+[A-Za-z]{2, }")

# url pattern
url_pattern = re.compile(r"https?://(?:[A-Za-z0-9\-]+\.)+[A-Za-z0-9]{2, }(?::\d{1,5})?[/A-Za-z0-9\-%?=\+\.]+")

# lister les fonctions 
dir(email_pattern)
```

## Méthodes de recherche

- `match()` : cherche un match au début d'une chaîne de caractères. S'il la chaîne ne correspond pas au pattern, il retourne `None`
- `search()` : cherche un match dans tout l'argument mais retourne uniquement le premier match rencontré
- `findall()` : retourne une `list` de tous les matches 

```python
sample: str = "test.com test@test.com testattest.com test@test.c test@bad_domain.com, tst+t_1@good-domain.com"

# match
email_1st_match = email_pattern.match(sample)
		# None

# search
email_1st_match = email_pattern.search(sample)
		# <re.Match object; span=(0, 13), match='test@test.com'>
email_1st_match.group()
		# 'test@test.com'

# findall
email_all_legit = email_pattern.findall(sample)
		# ['test@test.com', 'tst+t_1@good-domain.com']

```

## Name Capture Groups

- permet de définir des groupes avec **`?P<...>`** dans la définition du pattern
- ces groupes sont *callable* par la suite avec la méthode **`group()`**
	- `group()` sans argument retourne tout sous forme de string
	- `group("timestamp")` va retourner uniquement le groupe demandé

```python
import re 

# parse de auth.log
with open("auth.log") as f:
	logs = [l.strip() for l in f.readlines()]

# contenu de logs 
# ['10 Oct 2022 15:22:31 - User admin logged in',
#  '10 Oct 2022 15:25:10 - User bob logged in',
#  '10 Oct 2022 16:02:24 - User admin logged out']

# définition du pattern avec les NCG
log_pattern = re.compile(r"^(?P<timestamp>\d{2} [A-Z][a-z]{2} \d{4} \d{2}:\d{2}:\d{2}) - User (?P<user>[a-z]+) (?P<action>.+_?.+)$")

# création d'un objet match
monlog = log_pattern.match(logs[0])

print(monlog)
		# <re.Match object; span=(0, 43), match='10 Oct 2022 15:22:31 - User admin logged in'>
print(monlog.group())
		# '10 Oct 2022 15:22:31 - User admin logged in'
print(monlog.group("timestamp"))
		# '10 Oct 2022 15:22:31'
print(monlog.groupdict())
		# {'timestamp': '01 Nov 2022 09:15:23', 'user': 'admin', 'action': 'logged in'}
```

### parser un log et output un dictionnaire
```python
import re 

# parse de auth.log
with open("auth.log") as f:
	logs = [l.strip() for l in f.readlines()]

logs_parsed: dict = [log_pattern.match(l).groupdict() for l in logs]
		# 
```

## exercice 1 - log parser

### consigne

- parser un fichier `auth.log` et relever toutes les heures dans un fichier `adminlogtime.txt`

### code

```python
import re
from pprint import pprint

# parse de auth.log
with open("auth.log") as f:
	logs = [l.strip() for l in f.readlines()]
  
# définition du pattern avec les NCG
log_pattern = re.compile(r"^(?P<timestamp>\d{2} [A-Z][a-z]{2} \d{4} \d{2}:\d{2}:\d{2}) - User (?P<user>[a-z]+) (?P<action>.+)$")
  
for line in logs :
	match = log_pattern.match(line)
	if match.group("user") == "admin":
		with open("adminlogtime.txt", "a") as f:
		f.write(match.group("timestamp"))
		f.write(" >> ")
		f.write(match.group("action"))
		f.write("\n")
```

### output 

```
# adminlogtime.txt
01 Nov 2022 09:15:23 >> logged in
03 Nov 2022 14:18:45 >> logged out
06 Nov 2022 22:14:56 >> logged in
09 Nov 2022 11:37:25 >> logged out
11 Nov 2022 13:29:19 >> logged in
14 Nov 2022 20:45:55 >> logged out
17 Nov 2022 12:25:09 >> logged in
20 Nov 2022 15:33:22 >> logged out
```



