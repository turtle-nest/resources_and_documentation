# 🔁 Python Asynchrone : Coroutines et Exécution Concurrente

## 🧠 Introduction

L’exécution asynchrone permet de **gérer plusieurs tâches en parallèle**, sans avoir besoin de créer des threads ou des processus multiples. C’est particulièrement utile pour les **tâches liées à des entrées/sorties (I/O)**, comme :

- Les appels HTTP
- Les requêtes à des bases de données
- Les accès aux fichiers

---

## ⚙️ Concepts de base

### 📌 Coroutine
Une **coroutine** est une fonction spéciale qui peut **suspendre son exécution** (avec `await`) pour permettre à d'autres coroutines de s'exécuter, puis **reprendre là où elle s'était arrêtée**.

> ⚠️ Une coroutine doit être définie avec `async def`.

### 📌 Event Loop (boucle d’événements)
L’**event loop** est le cœur du module `asyncio`. Elle :
- planifie les tâches,
- exécute les callbacks,
- gère les opérations I/O.

### 📌 async / await
- `async def`: pour définir une coroutine.
- `await`: pour **attendre le résultat d’une autre coroutine**, sans bloquer l’event loop.

---

## 📘 Exemple simple

```python
import asyncio

async def dire_bonjour():
    await asyncio.sleep(1)
    print("Bonjour")

async def dire_monde():
    await asyncio.sleep(1)
    print("Monde")

async def main():
    await dire_bonjour()
    await dire_monde()

asyncio.run(main())
```

🕒 Durée d’exécution : **2 secondes** (les coroutines sont attendues l’une après l’autre)

---

## ⚡ Exécution Concurrente avec `asyncio.gather`

Pour exécuter plusieurs coroutines **en même temps** :

```python
async def main():
    await asyncio.gather(dire_bonjour(), dire_monde())
```

🕒 Résultat : "Bonjour" et "Monde" s’affichent **quasiment en même temps**, et le programme prend **1 seconde**.

---

## 🌍 Exemple concret : télécharger des pages web

```python
import aiohttp
import asyncio

async def recuperer_page(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    urls = ["https://example.com", "https://example.org", "https://example.net"]
    taches = [recuperer_page(url) for url in urls]
    pages = await asyncio.gather(*taches)
    for url, page in zip(urls, pages):
        print(f"Contenu depuis {url} : {len(page)} octets")

asyncio.run(main())
```

🚀 Ici, les **trois pages sont téléchargées en parallèle**, ce qui est **bien plus rapide** qu’un téléchargement séquentiel.

---

## 🔄 Coroutines vs Multi-threading

### ✅ Avantages des coroutines (async/await)
- **Légères** : Des milliers de coroutines peuvent tourner sans problème.
- **Prévisibles** : Les changements de contexte sont explicites (grâce à `await`).
- **Moins de bugs de concurrence** : Pas de course critique si bien conçu.

### ❌ Inconvénients
- Ne conviennent **pas aux tâches CPU-intensives**.
- Nécessitent que toutes les bibliothèques soient compatibles avec `async`.

---

### ✅ Avantages des threads
- **Parallélisme réel** sur plusieurs cœurs.
- Compatibles avec **beaucoup de bibliothèques existantes**.

### ❌ Inconvénients
- **Surcharge mémoire** plus importante.
- Risques de **race conditions**, **deadlocks**, etc.
- Le GIL de CPython empêche le vrai parallélisme pour les tâches CPU-bound.

---

## 🧩 Conclusion

| Tâche                    | Meilleur choix        |
|-------------------------|-----------------------|
| Requêtes réseau         | `asyncio` / coroutines|
| Téléchargement fichiers | `asyncio` / coroutines|
| Calcul lourd (CPU)      | `threading` ou `multiprocessing` |
| Mélange des deux        | Mixte : async + threads |

---

## 🔍 À retenir

- Utilise `async` pour définir une coroutine, `await` pour en appeler une autre.
- `asyncio.gather` permet de paralléliser facilement plusieurs tâches.
- `aiohttp` est une excellente librairie pour les requêtes HTTP asynchrones.
- Pour du traitement lourd, préfère les threads ou processus séparés.

---
