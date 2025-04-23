# ⚡ Programmation Asynchrone en Python : Comprendre `async`, `await` et les tâches concurrentes

## 📌 Qu’est-ce que la programmation asynchrone ?

Dans un programme **synchrone**, chaque ligne s’exécute **l’une après l’autre**. Si une tâche prend du temps (ex. : accès réseau), tout le programme attend… et **ne fait rien d’autre** pendant ce temps.

La **programmation asynchrone** permet d’**exécuter certaines tâches “en arrière-plan”**, sans bloquer le reste du programme. C’est idéal pour :

- les **requêtes réseau** (HTTP, API),
- les **opérations sur fichiers**,
- ou toute opération **I/O-bound** (liée aux entrées/sorties).

---

## 🔁 La boucle d’événements (`event loop`)

C’est le **moteur de l’asynchrone** en Python. Elle :

- tourne en continu,
- vérifie s’il y a des tâches à exécuter,
- et les lance quand elles sont prêtes.

💡 Elle donne **l’illusion du parallélisme** en **alternant rapidement entre les tâches**.

---

## ⚙️ Les mots-clés `async` et `await`

- `async def` permet de **définir une fonction asynchrone** (appelée **coroutine**).
- `await` permet de **mettre en pause** cette fonction pour attendre le résultat d’une autre coroutine.

---

## 📘 Exemple simple

```python
import asyncio

async def dire_apres(delai, message):
    await asyncio.sleep(delai)
    print(message)

async def main():
    print("Démarré")
    await dire_apres(1, "Bonjour")
    await dire_apres(2, "Monde")
    print("Terminé")

asyncio.run(main())
```

🔍 Ici :
- La fonction `dire_apres` attend (`await`) pendant un certain temps.
- L’appel de la seconde coroutine **n’est déclenché qu’après la première**.

🕒 Résultat :
- `Bonjour` après 1 seconde
- `Monde` après 3 secondes au total

---

## 🌀 Différence avec un code synchrone

Dans un code classique :

```python
import time

def dire_apres(delai, message):
    time.sleep(delai)
    print(message)

print("Démarré")
dire_apres(1, "Bonjour")
dire_apres(2, "Monde")
print("Terminé")
```

Pendant le `sleep`, **tout s’arrête**. Aucun autre traitement ne peut avoir lieu.

Avec l’asynchrone, pendant le `await`, la boucle peut **gérer d’autres tâches**.

---

## 🤹‍♂️ Exécution concurrente avec `create_task()`

Si tu veux **lancer plusieurs coroutines en parallèle** (ou plus exactement, de façon **concurrente**), utilise `asyncio.create_task()` :

```python
async def main():
    task1 = asyncio.create_task(dire_apres(1, "Bonjour"))
    task2 = asyncio.create_task(dire_apres(2, "Monde"))

    print("Démarré")

    await task1
    await task2

    print("Terminé")

asyncio.run(main())
```

🔍 Ici :
- Les deux tâches sont créées **en parallèle**,
- L’attente (`await`) se fait **en parallèle**, sans bloquer l’autre,
- Le temps total est d’environ **2 secondes** au lieu de 3.

---

## 🧠 Résumé

| Concept                      | Description |
|-----------------------------|-------------|
| `async def`                 | Définit une fonction asynchrone (coroutine) |
| `await`                     | Met en pause une coroutine pour en attendre une autre |
| `asyncio.run(coroutine)`    | Démarre une boucle d’événements et exécute une coroutine |
| `create_task()`             | Lance une coroutine en tâche concurrente |
| **Boucle d’événements**     | Cœur du système, elle exécute les coroutines planifiées |

---

## ✅ Quand utiliser la programmation asynchrone ?

👍 Recommandée pour :
- les programmes avec **beaucoup de requêtes I/O** (réseau, fichiers),
- les **applications web** (API, serveurs),
- les **interfaces utilisateur** (GUI, réactivité).

👎 À éviter pour :
- les calculs lourds (CPU-bound),
- les boucles de calcul intensif (préférer `threading` ou `multiprocessing`).

---
