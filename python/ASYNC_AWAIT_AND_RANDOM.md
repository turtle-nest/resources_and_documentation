# 📝 **Python Asynchrone & `random`**

## 🔹 1. `async` et `await` : syntaxe

- `async def` : définit une **coroutine** (fonction asynchrone).
- `await` : **suspend** l’exécution pour **attendre** une autre coroutine.

```python
async def ma_coroutine():
    await autre_coroutine()
```

🔧 Une fonction contenant `await` **doit être async**.

---

## 🔹 2. Exécuter un programme `async` avec `asyncio`

Utilise `asyncio.run()` pour lancer une coroutine principale.

```python
import asyncio

async def main():
    print("Coucou")

asyncio.run(main())
```

> ⚠️ Disponible à partir de **Python 3.7+**

---

## 🔹 3. Exécuter plusieurs coroutines **concurrentement**

Utilise `asyncio.gather()` pour les lancer **en parallèle** :

```python
async def main():
    await asyncio.gather(coro1(), coro2(), coro3())
```

🔁 Toutes les coroutines démarrent ensemble → **gain de temps**

---

## 🔹 4. Créer des tâches avec `create_task()`

Permet d’**exécuter une coroutine sans attendre immédiatement son résultat**.

```python
task1 = asyncio.create_task(coro1())
task2 = asyncio.create_task(coro2())

await task1
await task2
```

🪄 Avantage : les coroutines démarrent **en même temps**, et on peut attendre leur fin plus tard.

---

## 🔹 5. Utiliser le module `random`

Génère des valeurs aléatoires :

```python
import random

print(random.randint(1, 10))        # Entier aléatoire entre 1 et 10
print(random.choice(['a', 'b']))    # Élément aléatoire d’une liste
print(random.random())              # Float aléatoire entre 0 et 1
```

> Optionnel : pour des valeurs reproductibles → `random.seed(42)`

---

## 🧠 Astuce finale : combinaison `async` + `random`

```python
import asyncio
import random

async def action():
    delay = random.randint(1, 3)
    await asyncio.sleep(delay)
    print(f"Attente de {delay} sec terminée.")

async def main():
    await asyncio.gather(action(), action(), action())

asyncio.run(main())
```

---
