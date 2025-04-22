# 🧠 Cours Python : Les annotations de type, le duck typing et mypy

---

## I. **Les annotations de type en Python 3**

### Qu'est-ce que c’est ?

Depuis Python 3, on peut **ajouter des indications de type** pour les variables, les paramètres de fonctions, et les valeurs de retour. Ces indications sont **facultatives**, mais elles permettent de rendre le code **plus clair**, **mieux documenté**, et **plus facile à valider statiquement**.

### Exemple simple :

```python
def add(a: int, b: int) -> int:
    return a + b
```

Ici :
- `a: int` indique que le paramètre `a` est un entier,
- `b: int` également,
- `-> int` indique que la fonction retourne un entier.

**Important :** Python **ne vérifie pas les types à l'exécution**. Ce sont **juste des annotations**.

---

## II. **Utiliser les annotations de type pour les variables**

Depuis Python 3.6, on peut aussi annoter les **variables** :

```python
age: int = 30
name: str = "Alice"
coordinates: tuple[float, float] = (48.8566, 2.3522)
```

Tu peux aussi déclarer le type sans initialiser :

```python
score: float
```

---

## III. **Typing avancé avec le module `typing`**

Le module `typing` permet d’annoter des structures plus complexes.

### Importation :

```python
from typing import List, Dict, Tuple, Optional, Union
```

### Exemples :

```python
def process(data: List[str]) -> None:
    for item in data:
        print(item)

def get_user(id: int) -> Optional[str]:
    # Peut retourner None si l'utilisateur n'existe pas
    return "Alice" if id == 1 else None

def parse(value: Union[int, str]) -> str:
    return str(value)
```

---

## IV. **Le duck typing en Python**

### Définition :

Le **duck typing** vient de l’expression :
> "If it looks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck."

Autrement dit : **on ne vérifie pas le type exact**, mais **le comportement** de l'objet.

### Exemple :

```python
def quack(obj):
    obj.quack()

class Canard:
    def quack(self):
        print("Coin !")

class Jouet:
    def quack(self):
        print("Couic !")

quack(Canard())  # Coin !
quack(Jouet())   # Couic !
```

Peu importe si `Canard` et `Jouet` sont de la même classe ou non. Du moment qu’ils possèdent la méthode `quack`, le code fonctionne.

---

## V. **Valider son code avec `mypy`**

### Qu’est-ce que `mypy` ?

`mypy` est un outil de **vérification statique de types**. Il lit les annotations de type et signale les incohérences **sans exécuter le code**.

### Installation :

```bash
pip install mypy
```

### Utilisation :

```bash
mypy ton_fichier.py
```

### Exemple d'erreur détectée :

```python
def say_hello(name: str) -> str:
    return 42  # Erreur ! Ce n’est pas une chaîne

# mypy dira :
# error: Incompatible return value type (got "int", expected "str")
```

### Avantages :
- Détecte les erreurs **avant l’exécution**
- Améliore la **lisibilité**
- Facilite la **maintenance**
- Compatible avec les IDE (VSCode, PyCharm)

---

## VI. Résumé visuel

| Notion             | Exemple                                      |
|--------------------|----------------------------------------------|
| Annotation simple  | `x: int = 5`                                 |
| Fonction typée     | `def f(x: int) -> float:`                    |
| Structure complexe | `List[Tuple[str, int]]`                      |
| Duck typing        | Fonctionne tant que l’objet a la bonne méthode |
| Validation         | `mypy mon_script.py`                         |

---

## VII. Conclusion

Les **annotations de type** sont un outil puissant pour écrire du **code plus robuste, plus lisible, et plus maintenable**. Elles ne changent pas le comportement de ton programme, mais elles t’aident (ainsi que ton équipe et tes outils) à détecter les erreurs plus tôt.

Le **duck typing** reste au cœur de Python, mais tu peux combiner les deux approches en annotant **des interfaces de comportement** plutôt que des classes précises.

Enfin, l’outil **mypy** te permet de transformer tes annotations en véritable garde-fou statique, **sans sacrifier la flexibilité de Python**.

---