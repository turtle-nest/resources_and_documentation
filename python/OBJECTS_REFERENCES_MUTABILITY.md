# **Cours Python : Objets, Références et Mutabilité**

## 🧱 1. Qu'est-ce qu'un **objet** ?

En Python, **tout est objet**. Cela signifie que chaque valeur manipulée — que ce soit un entier, une chaîne de caractères, une liste ou une fonction — est une instance d'une **classe** et possède une **identité**, un **type** et une **valeur**.

Un objet est donc une **entité en mémoire** avec :
- une **identité** (adresse mémoire),
- un **type** (ex. : `int`, `str`, `list`...),
- un **état** (les données qu'il contient).

---

## 🧬 2. Différence entre **classe** et **objet (ou instance)**

- Une **classe** est un **modèle**, une **structure** définissant les attributs et méthodes d’un type d’objet.
- Un **objet** (ou **instance**) est une **réalisation concrète** de cette classe.

Exemple :
```python
class Voiture:
    def __init__(self, couleur):
        self.couleur = couleur

ma_voiture = Voiture("rouge")  # ma_voiture est un objet, une instance de la classe Voiture
```

---

## 🔄 3. Différence entre objet **mutable** et **immutable**

- Un **objet mutable** peut **être modifié** après sa création (par exemple une `list`).
- Un **objet immutable** ne peut **pas être modifié** : toute opération crée un **nouvel objet** (comme un `int` ou un `str`).

Exemples :
```python
# Immutable
a = "Bonjour"
a = a + " tout le monde"  # un nouvel objet string est créé

# Mutable
liste = [1, 2, 3]
liste.append(4)  # la liste est modifiée en place
```

---

## 🔗 4. Qu'est-ce qu'une **référence** ?

Une **référence** est le **lien** qu'une variable établit vers un objet en mémoire.

Quand on écrit :
```python
x = [1, 2, 3]
```
`x` est une **référence** à un objet liste `[1, 2, 3]`.

---

## ➡️ 5. Qu'est-ce qu'une **assignation** (assignment) ?

L’**assignation** est le processus par lequel une variable reçoit une **référence à un objet**.

```python
a = 42  # a est une référence vers l'objet entier 42
b = a   # b pointe vers le même objet que a
```

---

## 🪞 6. Qu'est-ce qu'un **alias** ?

Un **alias** est une **autre variable** qui référence le **même objet**.

```python
a = [1, 2]
b = a  # b est un alias de a
b.append(3)
print(a)  # [1, 2, 3] : a a aussi changé
```

---

## ❓ 7. Comment savoir si deux variables sont **identiques** ?

Deux variables sont **identiques** si elles **réfèrent au même objet** en mémoire.

On utilise l’opérateur `is` :
```python
a = [1]
b = a
print(a is b)  # True
```

---

## 🔗 8. Comment savoir si deux variables sont liées au **même objet** ?

On utilise aussi `is` ou la fonction `id()` :
```python
a = [1, 2]
b = a
print(id(a) == id(b))  # True
```

---

## 🧠 9. Comment afficher l’**identifiant** d’une variable (adresse mémoire dans CPython) ?

Avec la fonction intégrée `id()` :
```python
x = "Python"
print(id(x))
```
> Cela renvoie l’**adresse mémoire** de l’objet pointé par la variable (dans l’implémentation CPython).

---

## 🔁 10. Qu’est-ce que **mutable** et **immutable** ?

- **Mutable** : modifiable après sa création (ex. : `list`, `dict`, `set`)
- **Immutable** : non modifiable (ex. : `int`, `float`, `str`, `tuple`, `frozenset`)

---

## 📦 11. Quels sont les types **mutables** intégrés ?

- `list`
- `dict`
- `set`
- `bytearray`

---

## 📦 12. Quels sont les types **immutables** intégrés ?

- `int`, `float`, `complex`
- `bool`
- `str`
- `tuple`
- `frozenset`
- `bytes`
- `NoneType`

---

## 🧾 13. Comment Python passe-t-il les variables aux fonctions ?

Python utilise un mécanisme appelé **"passage par affectation de l'objet"**, souvent appelé "pass-by-object-reference".

- Quand on passe un objet à une fonction, la **référence** à cet objet est copiée.
- Si l’objet est **mutable**, il peut être **modifié** à l’intérieur de la fonction.
- Si l’objet est **immutable**, il ne peut **pas être modifié**, mais la variable locale peut **pointer vers un nouvel objet**.

Exemple :
```python
def ajouter_un(x):
    x += 1
    return x

a = 10
ajouter_un(a)  # a reste 10 car int est immutable

def ajoute_élément(l):
    l.append(4)

liste = [1, 2, 3]
ajoute_élément(liste)
print(liste)  # [1, 2, 3, 4]
```

---

## ✅ Résumé visuel :

| Concept              | Explication courte                            |
|----------------------|-----------------------------------------------|
| Objet                | Entité mémoire avec type, valeur, identité    |
| Classe vs Objet      | Classe = modèle / Objet = instance            |
| Mutable              | Peut être modifié (ex: liste)                 |
| Immutable            | Ne peut pas être modifié (ex: string)         |
| Référence            | Lien entre variable et objet                  |
| Assignation          | Donne une référence à une variable            |
| Alias                | Deux variables référant au même objet         |
| Identité             | Vérifiée avec `is` ou `id()`                  |
| Types mutables       | `list`, `dict`, `set`, `bytearray`           |
| Types immuables      | `int`, `str`, `tuple`, `bool`, `bytes`...    |
| Passage de variable  | Copie de la référence (modifiable si mutable) |

---
