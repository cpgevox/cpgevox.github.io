---
layout: papage
title: Aide-mémoire de Python
parent: top
---

# Types simples

## Généralités

On parle des types de base (qui l'on développera par la suite), de
coercion, de la commande ``type``

## Booléens

c

## Entiers et flottants
…et complexes

## Caractères
Ne pas oublier de parler d'unicode et du caractère d'échappement.

### Caractère d'échappement

Le **backslash** (ou contre-oblique) permet d'obtenir certains caractères qui ne sont pas directement accessibles au clavier. En voici quelques exemples&nbsp;:

```python
>>> print("a\tb") # tabulation
a	b
>>> print("a\nb") # retour à la ligne
a
b
>>> print("a\"b\"c") # guillemets
a"b"c
>>> print("a\\b") # backslash
a\b
>>> "\u2126" # unicode
'Ω'
```

# Instructions de bases

## Affectation
Cette opération permet de modifier la valeur d'une variable. La syntaxe d'une affectation est la suivante&nbsp;:

```python
nom_de_variable = expression
```

En dépit de sa notation, il ne s'agit pas d'une égalité. Une affectation consiste en deux étapes:

1. on évalue l'``expression`` (qui peut utiliser la valeur de ``nom_de_variable``),
2. _puis_ on modifie la valeur de ``nom_de_variable`` en lui attribuant la valeur obtenue lors de l'évaluation de l'``expression``.

Les lignes suivantes sont donc tout à fait correctes et ont un sens précis (alors que l'équation mathématique $a = a + 1$ n'a, elle, pas de solutions)&nbsp;:

```python
>>> a = 3
>>> a
3
>>> a = a + 1
>>> a
4
```

## Commentaires
Ils ne font rien… mais sont utiles pour lire et comprendre un programme. On peut donc comparer ce commentaire-là, inutile&nbsp;:

```python
if a = 1 :
	# a = 1
	print('La variable a est égale à 1.')
```

à ce commentaire-ci (qui fait suite au précédent)&nbsp;:

```python
else : # a != 1
	print("La variable a n'est pas égale à 1.")
```

Il faut, en général, que les commentaires soient intéressants et aident réellement à la compréhension du code. En particulier, un commentaire qui ne fait que reformuler une ligne de code n'est pas très intéressant.

C'est un art difficile…

Regardons juste un dernier exemple, dans une boucle ``while``, où l'on rappelle les informations en sortie de boucle.

```python
n = 10
while n > 1 :
	n = n - 1
# On a maintenant : n <= 0
print(n, 'n\'est pas strictement positif.')
```

## Boucles ``for``

### Syntaxe générale

Le bloc d'instructions qui doit être exécuté par la boucle est signalé par une **tabulation**.

Il fait faire attention à la présence nécessaire du ``:``.

```python
for variable in iterable:
	instructions
```

### Itérables

Un _itérable_ est un type de données composite séquentiel, comme une liste, que l'on parcourt en séquence, dans un ordre précis. Voici quelques exemples de données itérables&nbsp;:

```python
for i in range(10):
	print(i)
for x in ['a', 1, True, "Bonjour"]:
	print(x)
for c in "Bonjour":
	print(c)
```

Un autre exemple important d'itérable est constitué des fichiers, comme nous le verrons plus tard.

### Exemple d'utilisation
On peut calculer la somme de tous les entiers de 1 à 100 ainsi&nbsp;:

```python
somme = 0
for x in range(1,101):
	somme = somme + x
print(somme)
```

et le maximum d'une liste comme cela&nbsp;:

```python
def maximum_liste(l):
	m = l[0]
	for x in l:
		m = max(m, x)
	return m
```

## Boucles ``while``

### Syntaxe générale

```python
while condition:
	instructions
```

La ``condition`` est une expression booléenne. La boucle s'exécute tant que cette condition est vérifiée (c'est-à-dire qu'elle renvoie ``true``). Ainsi, la boucle s'achève la première fois que la condition n'est plus vérifiée.

```python
# ce code n'affichera pas de bétises
n = 10
while n > 0:
	# ici, n > 0
	print(n, "est strictement positif")
	n = n - 1
# ici, on n'a plus n > 0
# donc n <= 0
print(n, "n'est pas strictement positif")
```

### Exemple d'utilisation

On cherche à dépasser une certaine valeur.

```python
f = 1
n = 0
while f < 10000 :
	# invariant de boucle :
	# f = n!
	n = n + 1
	f = f * n
# invariant de boucle (toujours vérifié) : f = n!
# condition de sortie : f >= 10000
# d'où : n! >= 10000
print('Plus petit n tel que n! >= 10000 :', n)
```

## Fonctions et procédures

### Syntaxe générale

```python
def nom_de_fonction(arguments):
	instructions
```

Si la fonction renvoie une valeur, cela sera fait par le biais de la fonction ``return`` qui, de plus, interrompt l'exécution de la fonction. Dans l'exemple suivant, le ``print`` ne sera jamais exécuté.

```python
>>> def f(x, y):
... 	return(x * y + 1)
... 	print("Bonjour")
... 
>>> f(4, 5)
21
```

### ``return`` et ``print``

Insistons sur le fait qu'une valeur renvoyée par une fonction doit l'être par le biais de ``return``. Il peut être tentant d'utiliser un ``print`` à la place, mais c'est en fait une mauvaise idée. Considérons les deux fonctions suivantes&nbsp;:

```python
def vrai_fonction(x):
	return (2 * x + 1)

def fausse_fonction(x):
	print(2 * x + 1)
```

Elles ont apparemment un comportement comparable&nbsp;:

```python
>>> vrai_fonction(4)
9
>>> fausse_fonction(4)
9
```

Mais il n'en est rien, puisque ``fausse_fonction`` ne renvoie rien&nbsp;:

```python
>>> 1 + vrai_fonction(4)
10
>>> 1 + fausse_fonction(4)
9
Traceback (most recent call last):
	File '<stdin>', line 1, in <module>
TypeError: unsupported operand type(s) for +:
	'int' and 'NoneType'
```

# Listes et compagnie

## Généralités
Un **type de données composite séquentiel**, comme une liste, est un type qui comporte plusieurs éléments organisés dans un ordre précis. On trouve aussi les chaînes de caractères, ou **strings**, qui sont des successions de caractères, et les **tuples**.

* ``len(t)`` renvoie la longueur (le nombre d’éléments) de&nbsp;``t``.

* ``t[i]`` renvoie le ``i``-ème élément de&nbsp;``t`` 
	*  La numérotation va de&nbsp;``0`` à&nbsp;``len(t)-1``.
	* Une position négative fait compter à rebours à partir du dernier élément (qui a la position&nbsp;``-1``).

```python
>>> l = [3, 4, 1, 2]
>>> len(l)
4
>>> l[1], l[-1]
(4, 2)
```

La **section** (ou **slice**) ``t[i:j]`` sélectionne les éléments de&nbsp;``t`` de la position&nbsp;``i`` incluse à la position&nbsp;``j`` exclue.

* On peut omettre l’un ou l’autre des indices, auquel cas la sélection part du début ou va jusqu’à la fin,
* On peut donner des positions négatives,
*  On peut donner un troisième argument indiquant le pas, qui peut être négatif.

```python
>>> "abcdefghijklmnopqrstuvwxyz"[5:20]
'fghijklmnopqrst'
>>> "abcdefghijklmnopqrstuvwxyz"[-4:-1]
'wxy'
>>> "abcdefghijklmnopqrstuvwxyz"[5:20:2]
'fhjlnprt'
>>> "abcdefghijklmnopqrstuvwxyz"[::-2]
'zxvtrpnljhfdb'
```

* ``t.count(x)`` retourne le nombre d’occurences de&nbsp;``x`` dans&nbsp;``t``.

* ``t.index(x)`` indique la position du premier élément&nbsp;``x`` dans&nbsp;``t``.

```python
>>> "ananas".count("a")
3
>>> [1, 2, 3, 4, 3, 2, 4, 1].count(3)
2
>>> [1, 4, 3, 2, 5, 4,1].index(4)
1
```

On peut «&nbsp;ajouter&nbsp;» des séquences de même type (on parlera plutôt de **concaténation**) et les «&nbsp;multiplier&nbsp;» (par un entier, c'est une concaténation itérée).

```python
>>> [1, 2] + [3, 4]
[1, 2, 3, 4]
>>> [1, 2] * 5
[1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
>>> "a" * 20
'aaaaaaaaaaaaaaaaaaaa'
```

## Chaines de caractères

notations, lien avec caractères
quelques capacités type objet
pos et find sont un peu plus évolués, on peut mettre des chaînes et pas seulement des caractères.

```python
>>> "Choubidoubidou".count("ou")
3
>>> "Choubidoubidou".index("dou")
6
>>> "Choubidoubidou".index("choucroute")
Traceback (most recent call last):
	File '<stdin>', line 1, in <module>
ValueError: substring not found
```

### Quelques commandes supplémentaires

% Comme les chaînes de caractères ne sont pas mutables, les commandes suivantes laissent la chaîne de départ inchangée.

* ``s.upper()`` et ``s.lower()`` renvoient une chaîne de caractère obtenue à partir de ``s`` en mettant toutes les lettres en majuscules ou en minuscules.

* ``s.split()`` renvoie une liste en coupant ``s`` à chaque espace. Si l'on fournit une chaîne en argument, c'est cette chaîne qui servira à établir les coupures.

```python
>>> "Quel beau chapeau".split()
['Quel', 'beau', 'chapeau']
>>> "143,543,412".split(",")
['143', '543', '412']
>>> "143,543,412".split("4")
['1', '3,5', '3,', '12']
```

* ``s.join(it)`` renvoie une chaîne de caractères obtenue en concatenant les chaînes de caractères de l'_itérable_ ``it`` séparées par&nbsp;``s``. C'est un peu l'inverse d'un ``split``.

```python
>>> " -- ".join(['143', '543', '412'])
'143 -- 543 -- 412'
>>> ",".join("Choucroute")
'C,h,o,u,c,r,o,u,t,e'
```

## Listes

% @@ Ajouter alias et copie.

% @@ Ajouter listes en compréhension

Une liste est **mutable**, ce qui signifie que l’on peut modifier son contenu, case par case ou par _slice_ entier.

```python
>>> l = [1, 2, "Bonjour", 4]
>>> l[2] = 3
>>> l
[1, 2, 3, 4]
>>> l[1:2] = [21, 22, 23, 24]
>>> l
[1, 21, 22, 23, 24, 3, 4]
>>> l[2:4] = []
>>> l
[1, 21, 24, 3, 4]
```


### Quelques commandes

* ``l.insert(x, pos)`` modifie ``l`` en insérant l’élément ``x`` à la position ``pos``.

* ``l.remove(x)`` modifie ``l`` en supprimant la première occurence de la valeur&nbsp;``x``.

* ``l.append(x)`` modifie ``l`` en ajoutant l’élément ``x`` en queue.

* ``l.extend(l2)`` modifie ``l`` en concaténant la liste ``l2`` en queue de liste. Une autre manière de procéder est d'écrire ``l = l + l2``.

* ``l.sort()`` trie les éléments de ``l`` par ordre croissant.

* ``l.pop()`` retire le dernier élément de ``l`` et le renvoie.

* ``l.reverse()`` renverse la liste.

```python
>>> l = [1, 2, 3, 4]
>>> l.pop()
4
>>> l
[1, 2, 3]
>>> l.reverse()
>>> l
[3, 2, 1]
```

### Duplication

Pour dupliquer une liste, on évitera de faire une simple affectation, car les deux variables corresponderont à la même liste&nbsp;:

```python
>>> l1 = [1, 2, 3]
>>> l2 = l1
>>> l2[1] = 'a'
>>> l1, l2
([1, 'a', 3], [1, 'a', 3])
```

Pour y remédier, voici deux solutions&nbsp;:

```python
>>> l1 = [1, 2, 3]
>>> l2 = l1.copy() # Par appel de la méthode copy
>>> l2[1] = 'a'
>>> l1, l2
([1, 2, 3], [1, 'a', 3])
>>> l3 = l1[:] # Par création d'un slice
>>> l3[1]="z"
>>> l1, l3
([1, 2, 3], [1, 'z', 3])
```

### Listes en compréhension

Il s'agit d'une manière de définir une liste à partir d'une autre (ou plus généralement à partir d'un _itérable_) en indiquant comment la remplir.

```python
>>> [x * 2 + 1 for x in [1, 2, 3, 4]]
[3, 5, 7, 9]
>>> [ord(c) for c in "Bonjour"]
[66, 111, 110, 106, 111, 117, 114]
```

## Tuples
Cette construction correspond à la notion de produit cartésien en mathématiques, et la notation est la même.

```python
>>> a = (1, 'Bonjour', True, 2.0)
```

On peut accéder à ses éléments en indiquant sa position, de même que des slices, et c'est une structure _itérable_&nbsp;:

```python
>>> a[1]
'Bonjour'
>>> a[1:3]
('Bonjour', True)
>>> for i in a:
... 	print(i)
...
1
Bonjour
True
2.0
```

Par contre, contrairement aux listes, ce n'est pas un type de donnée _mutable_, ce qui signifie que l'on ne peut modifier son contenu&nbsp;:

```python
>>> a[2] = False
Traceback (most recent call last):
  File '<stdin>', line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

Notons enfin que l'on peut utiliser les tuples pour des affectations multiples, ce qui est particulièrement magique si l'on veut échanger le contenu de deux variables&nbsp;:

```python
>>> a, b = 1, 3
>>> a
1
>>> b
3
>>> a, b = b, a
>>> a
3
>>> b
1
```

## Compléments sur les itérables

### ``range``

Une fonction très utile (et que vous connaissez déjà bien). Rappelons que ses arguments sont ``range([start], stop, [step])``, que les arguments entre crochets sont optionnels et que l'énumération s'arrête _avant_ ``stop``.

### Fichiers

La variable retournée par l'ouverture d'un fichier en lecture est un itérable contenant des chaînes de caractères.

Par exemple, pour afficher toutes les lignes d'un fichier, on peut écrire&nbsp;:

```python
with open('Plan_secret.md', mode = 'r', encoding = 'utf-8') as fl:
	for line in fl:
		print(len(line))
```
On peut créer une liste contenant toutes les lignes d'un fichier ainsi (on définit une liste en compréhension)&nbsp;:

```python
with open('Plan_secret.md', mode = 'r', encoding = 'utf-8') as fl:
	lignes = [ligne for ligne in fl]
```
Bien sûr, on peut utiliser ``lignes = fl.readlines()`` pour obtenir le même résultat, mais il est souvent peu judicieux de charger entièrement un fichier avant de le traîter.

### ``enumerate``

Une petite fonction supplémentaire qui, appliquée à un itérable, renvoie un nouvel itérable donnant des tuples indiquant les éléments précédés de leur position dans la liste.

```python
>>> l = ["chou", "bi", "dou", "wa"]
>>> [x for x in enumerate(l)]
[(0, 'chou'), (1, 'bi'), (2, 'dou'), (3, 'wa')]
```

L'exemple suivant affiche le contenu d'un fichier avec numérotation des lignes.

```python
with open('Plan_secret.md', mode = 'r', encoding = 'utf-8') as fl:
	for nb, line in enumerate(fl):
		print("%4d : %s" % (nb, line), end = "")
```

<!-- % \subsubsection{next\vphantom{)}} -->
<!-- % Cela nous mène aux exceptions… -->

# Entrées et sorties

## Interaction avec l'utilisateur

### ``input``

La fonction ``input``, qui prend en argument une chaîne de caractère, affiche cette chaîne à l'écran, puis retourne la **chaîne de caractère** tapée par l'utilisateur.

```python
>>> n = input("Entrez un nombre : ")
Entrez un nombre : 42
>>> n
'42'
>>> type(n)
<class 'str'>
>>> n + 1
Traceback (most recent call last):
  File '<stdin>', line 1, in <module>
TypeError: Cannot convert 'int' object to str implicitly
```

Si l'on veut une donnée d'un type autre que ``string``, il faut explicitement faire une conversion de type.

```python
>>> n = int(input("Entrez un nombre : "))
Entrez un nombre : 43
>>> n
43
>>> type(n)
<class 'int'>
>>> n + 1
44
```

### ``print``

Pour afficher des informations dans la console, on utilise la fonction ``print``. On peut donner zéro, un ou plusieurs données à imprimer, ainsi que des arguments optionnels&nbsp;: ``sep`` qui est une chaîne de caractère insérée entre chaques arguments (par défaut, ``sep = ' '``), et ``end`` qui est ajoutée à la fin (par défaut, on a ``end = '\\n'``).

```python
>>> print(True, 1, "a")
True 1 a
>>> print(True, 1, "a", sep = " -- ")
True -- 1 -- a
>>> print(True, 1, "a", sep = ",\n", end = ".\n")
True,
1,
a.
```

### Formatage de chaînes de caractères

Pour formater un affichage, on pourra utiliser la méthode ``format`` des chaînes de caractères. Voici quelques exemples&nbsp;:

```python
>>> "Le nombre {} est plus grand que {}".format(31,42)
'Le nombre 31 est plus grand que 42'
>>> "Le nombre {1} est plus grand que {0}".format(31,42)
'Le nombre 42 est plus grand que 31'
>>> "{0: <10}-{1:.^10}-{2:_>10}".format("Hodor","Hodor?","Hodor!")
'Hodor     -..Hodor?..-____Hodor!'
>>> print('"{:5d}" et a "{:04d}"'.format(22,12))
"   22" et "0012"
>>> print("'{:010.6f}' et '{:8.3f}'".format(pi,exp(1)))
'003.141593' et '   2.718'
```

On pourra trouver de nombreux exemples supplémentaires (mais en anglais) sur la page [https://pyformat.info]().

## Fichiers
Il faut savoir ouvrir un fichier en lecture et en écriture, savoir comprendre un nom de fichier avec chemin complet, comment écrire ces chemins, …

Comment lire (plusieurs manières), écrire…

On peut parler de la construction ``with`` pour les fichiers.

```python
with open('Cheatsheet.md', mode = 'r') as fl :
	for nb, line in enumerate(fl) :
		print("%4d : %s" % (nb, line), end = "")
```

# Modules

## Généralités
a

## Module ``random``
a

## Module ``math``
La plupart des fonctions et constantes mathématiques de bases ne sont pas disponibles par défaut, et s'obtiennent grâce à ce module.


```python
>>> pi
Traceback (most recent call last):
  File '<stdin>', line 1, in <module>
NameError: name 'pi' is not defined
>>> cos(0)
Traceback (most recent call last):
  File '<stdin>', line 1, in <module>
NameError: name 'cos' is not defined
>>> import math
>>> math.pi
3.141592653589793
>>> math.cos(0)
1.0
```

À moins d'avoir l'intention douteuse de nommer des variables ou fonctions comme des fonctions mathématiques célèbres, il semble en général peu risqué d'ouvrir ce module.

```python
>>> from math import *
>>> tan(pi/4) # Bon, passons...
0.9999999999999999
```

## Module ``os``
De ce module, retenons deux fonctions utiles pour se retrouver dans l'arborescence de fichiers&nbsp;:

``os.getcwd()`` renvoie une chaîne de caractère indiquant le répertoire de travail courant.

``os.chdir(chemin)`` mets le répertoire de travail à la valeur indiquée par la chaîne de caractères ``chemin``.

Sous Linux ou OS&nbsp;X, cela peut ressembler à cela&nbsp;:

```python
>>> os.getcwd()
'/Users/maitre_du_monde/conquete'
>>> os.chdir('plan_a')
>>> os.getcwd()
'/Users/maitre_du_monde/conquete/plan_a'
>>> os.chdir('../plan_b')
>>> os.getcwd()
'/Users/maitre_du_monde/conquete/plan_b'
>>> os.chdir('/Users/maitre_du_monde/repli')
>>> os.getcwd()
'/Users/maitre_du_monde/repli'
```

@@@ À mettre avec les fichiers, chemins, etc.&nbsp;: Sous Windows, on utilise normalement le _backslash_ ``\``. Cependant, pour simplifier les choses, il est possible d'utiliser le _slash_ ``/`` comme le reste du monde (que ce soit sous Linux, OS&nbsp;X ou plus généralement un système de type Unix, ou même pour les URLs utilisées pour les adresses internet).
