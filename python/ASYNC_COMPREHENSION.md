# 🐍 Fiche complète : Async Generators, Async Comprehensions et Typage de Generators en Python

## 1. Typage des générateurs (`Generator`, `Iterator`, `Iterable`)

### Comment typer un générateur classique en Python
- **Problème** : Comment préciser le type d'un générateur qui `yield` des valeurs ?

- **Solution** : Utiliser `typing.Generator`, `typing.Iterator` ou `typing.Iterable`.

#### `typing.Generator`
```python
from typing import Generator

def numbers() -> Generator[int, None, None]:
    yield 1
    yield 2
```
- La signature générale est `Generator[YieldType, SendType, ReturnType]`
  - `YieldType` : le type des valeurs produites par `yield`.
  - `SendType` : le type de données pouvant être envoyées dans le générateur avec `.send()`.
  - `ReturnType` : le type de la valeur retournée par `return` dans le générateur (rarement utilisé).

🔵 **Exemple plus complet** :
```python
def my_generator() -> Generator[str, int, float]:
    x = yield "start"  # reçoit un int
    yield "processing"
    return 1.0  # retourne un float
```

### `typing.Iterator` et `typing.Iterable`
- **Iterator** : si ton générateur n'accepte pas `.send()`, il est souvent suffisant de typer avec `Iterator[YieldType]`.
- **Iterable** : si seule l'itération externe compte (peu utilisé pour les générateurs).

---

## 2. Générateurs asynchrones (`async def` + `yield`)

### Qu'est-ce qu'un générateur asynchrone ?
- Un **générateur asynchrone** combine :
  - la capacité d'**attendre** (`await`)
  - et celle de **produire** des valeurs au fil du temps (`yield`).

Introduit en Python **3.6** (via [PEP 530](https://peps.python.org/pep-0530/)).

🔵 **Exemple simple** :
```python
async def async_gen():
    for i in range(3):
        yield i
        await asyncio.sleep(1)
```

- **Usage** : tu dois utiliser `async for` pour itérer dessus :

```python
import asyncio

async def main():
    async for value in async_gen():
        print(value)

asyncio.run(main())
```

👉 Utile quand tu veux générer **des flux de données au fil du temps** sans tout bloquer.

---

## 3. Compréhensions asynchrones (`async for` dans une compréhension)

### Qu'est-ce qu'une async comprehension ?
- Introduite aussi en Python **3.6**.
- Syntaxe : comme une compréhension classique, mais en utilisant `async for`.

🔵 **Exemple** :
```python
async def async_numbers():
    for i in range(5):
        yield i
        await asyncio.sleep(0.1)

async def squares():
    return [i * i async for i in async_numbers()]

# Exécution
import asyncio
print(asyncio.run(squares()))
```

### ⚡ Remarques importantes :
- Les **listes**, **sets**, **dicts** peuvent être créés avec async comprehensions.
- Mais **les compréhensions de générateurs** (`(i async for i in ...)`) **ne sont pas autorisées** avant Python 3.7 !

---

## 4. Comment écrire correctement un générateur asynchrone

### Structure de base :
- Définir la fonction avec `async def`
- Utiliser `yield` pour émettre les valeurs
- Utiliser `await` à l'intérieur si besoin d'attendre

🔵 **Exemple avec plus de logique** :
```python
import asyncio

async def delayed_count(limit: int):
    for i in range(limit):
        await asyncio.sleep(0.5)
        yield i

async def main():
    async for number in delayed_count(5):
        print(f"Got number: {number}")

asyncio.run(main())
```

---

## 5. Comment typer un générateur asynchrone (`AsyncGenerator`)

- Utiliser `typing.AsyncGenerator` pour typer les fonctions génératrices asynchrones.

#### Syntaxe :
```python
from typing import AsyncGenerator

async def async_counter() -> AsyncGenerator[int, None]:
    for i in range(5):
        yield i
```
- `AsyncGenerator[YieldType, SendType]` :
  - `YieldType` : type des valeurs produites
  - `SendType` : type pouvant être envoyé (rarement utilisé)

### 🔥 Petit résumé visuel :

| Type            | Description |
|-----------------|-------------|
| `Generator`     | Générateur classique (avec `yield`) |
| `AsyncGenerator`| Générateur asynchrone (`async def` + `yield`) |
| `Iterator`      | Objet itérable par `next()` |
| `Iterable`      | Objet pouvant être parcouru (ex : boucle `for`) |

---

# ✨ Bonus : Avantages pratiques des Async Generators et Async Comprehensions

- **Moins de mémoire** : génération d'éléments un par un sans charger toute la collection.
- **Réactivité** : particulièrement utile pour des applications réseaux, des APIs, de la lecture de fichiers volumineux, du streaming.
- **Simplification du code** : plutôt que de séparer la production et la consommation de données en plusieurs fonctions, on peut écrire du code plus direct et lisible.

---

# 📚 Pour aller encore plus loin

- [PEP 525 — Asynchronous Generators](https://peps.python.org/pep-0525/) (définit les async generators eux-mêmes)
- [PEP 530 — Asynchronous Comprehensions](https://peps.python.org/pep-0530/) (définit l'usage dans les compréhensions)
- [Python Typing — AsyncGenerator Documentation](https://docs.python.org/3/library/typing.html#typing.AsyncGenerator)

---
