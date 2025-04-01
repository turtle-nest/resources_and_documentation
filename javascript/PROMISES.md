# 🧠 Cours complet : Les Promises en JavaScript

---

## 📌 1. Qu’est-ce qu’une Promise ? Pourquoi et comment l’utiliser ?

### 🔹 Définition

Une **Promise** est un objet JavaScript qui représente l'**aboutissement (ou l'échec)** d'une opération asynchrone, et permet d'exécuter du code en conséquence.

```js
const maPromesse = new Promise((resolve, reject) => {
  // traitement async
});
```

### 🔹 Pourquoi utiliser des Promises ?

Avant les Promises, JavaScript utilisait les **callbacks** pour gérer l’asynchrone, ce qui menait à des situations de **callback hell** (imbriqués, illisibles).

Les Promises apportent :

- Une **gestion plus claire** de l’asynchrone
- Une **chaîne de traitements** plus lisible
- Une **gestion centralisée des erreurs**

---

## 📦 2. Les états d’une Promise

Une Promise a 3 **états** :

| État          | Description |
|---------------|-------------|
| `pending`     | En attente |
| `fulfilled`   | Résolue avec succès |
| `rejected`    | Échouée avec une erreur |

```js
const promesse = new Promise((resolve, reject) => {
  if (toutVaBien) {
    resolve('Succès');
  } else {
    reject('Erreur');
  }
});
```

---

## ✅ 3. Utiliser `then()`, `catch()` et `finally()`

### 🔸 `.then()`

Exécute une fonction lorsque la promesse est **résolue** avec succès :

```js
promesse.then((resultat) => {
  console.log('Succès :', resultat);
});
```

### 🔸 `.catch()`

Exécute une fonction si la promesse **échoue** :

```js
promesse
  .then(result => console.log(result))
  .catch(erreur => console.error('Erreur :', erreur));
```

### 🔸 `.finally()`

Exécuté **quoi qu’il arrive**, succès ou échec :

```js
promesse
  .then(result => console.log(result))
  .catch(erreur => console.error(erreur))
  .finally(() => console.log("Terminé"));
```

---

## 🧰 4. Les méthodes statiques de l'objet `Promise`

### 📘 `Promise.resolve(valeur)`

Retourne une promesse **immédiatement résolue**.

```js
Promise.resolve(42).then(console.log); // 42
```

### 📕 `Promise.reject(erreur)`

Retourne une promesse **immédiatement rejetée**.

```js
Promise.reject("Oups").catch(console.error);
```

### 📚 `Promise.all([...])`

Attend que **toutes** les promesses soient résolues.

```js
Promise.all([p1, p2, p3]).then(values => {
  // Toutes sont résolues
}).catch(error => {
  // Une au moins est rejetée
});
```

### 📖 `Promise.race([...])`

Résout ou rejette **dès que la première** promesse est terminée.

```js
Promise.race([p1, p2]).then(console.log);
```

### 📕 `Promise.allSettled([...])`

Attend que **toutes** les promesses soient terminées (résolues ou rejetées).

```js
Promise.allSettled([p1, p2]).then(results => {
  console.log(results);
});
```

### 📗 `Promise.any([...])` *(ES2021)*

Renvoie la **première promesse résolue**, ignore les rejets.

```js
Promise.any([p1, p2]).then(result => console.log(result));
```

---

## 🧪 5. Try / Throw / Catch dans un contexte async

Tu peux **générer manuellement une erreur** avec `throw` :

```js
function verifier(age) {
  if (age < 18) {
    throw new Error("Interdit aux mineurs !");
  }
  return "Bienvenue";
}
```

Et la gérer avec `try...catch` :

```js
try {
  const message = verifier(16);
  console.log(message);
} catch (err) {
  console.error(err.message); // Interdit aux mineurs !
}
```

---

## ⏳ 6. Le mot-clé `await` et les fonctions `async`

### 🔹 `async`

Permet de déclarer une fonction **asynchrone**, qui retourne toujours une Promise.

```js
async function direBonjour() {
  return "Bonjour";
}
```

Tu peux l’utiliser comme une Promise :

```js
direBonjour().then(console.log); // Bonjour
```

### 🔹 `await`

Permet de **mettre en pause l’exécution** de la fonction jusqu’à ce qu’une Promise soit résolue :

```js
async function attendreMessage() {
  const message = await Promise.resolve("Salut !");
  console.log(message); // "Salut !"
}
```

### ⚠️ À savoir

- `await` **ne peut être utilisé que dans une fonction `async`**.
- Si la promesse échoue, on peut capturer l’erreur avec `try...catch`.

```js
async function fetchData() {
  try {
    const data = await fetch("https://api.exemple.com");
    const json = await data.json();
    console.log(json);
  } catch (err) {
    console.error("Erreur :", err);
  }
}
```

---

## 🔁 Exemple concret combinant tout

```js
async function chargerUtilisateur() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    if (!response.ok) throw new Error("Problème réseau");
    const user = await response.json();
    console.log("Nom :", user.name);
  } catch (e) {
    console.error("Erreur :", e.message);
  } finally {
    console.log("Requête terminée");
  }
}
```

---

## 🧠 Résumé des notions essentielles

| Concept | Explication rapide |
|--------|---------------------|
| `Promise` | Objet qui gère l’asynchrone |
| `resolve/reject` | Résolution ou rejet manuel |
| `then/catch/finally` | Gestion des résultats ou erreurs |
| `Promise.all()` | Attend toutes les promesses |
| `async/await` | Syntaxe moderne lisible pour l’asynchrone |
| `try/catch` | Gérer les erreurs dans une fonction async |
| `throw` | Générer une erreur manuellement |

---

## 🧰 Bonus : outils utiles

- Outils de test : `fetch`, `setTimeout`, `axios`, etc.
- Pour debugger : `console.log()`, `DevTools > Network`, `Breakpoints`.

---

## 📘 Conclusion

Les **Promises** sont au cœur de la programmation asynchrone moderne en JavaScript. Elles permettent une gestion propre, robuste et lisible du temps d’attente, des appels réseaux, des erreurs, et des traitements consécutifs.

Tu maîtrises maintenant :
- la syntaxe de base,
- les différentes méthodes de `Promise`,
- la gestion des erreurs avec `throw`, `try...catch`,
- et surtout `async/await` qui rend le code **fluide et naturel** à lire.
