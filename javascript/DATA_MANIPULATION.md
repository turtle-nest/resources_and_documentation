# 📘 Cours : **Data Manipulation en JavaScript**

## 🎯 Objectif  
Comprendre et maîtriser les principales structures et méthodes de manipulation de données en JavaScript : les **méthodes d’Array**, les **typed arrays** et les structures de données **Set, Map et WeakMap**.

---

## 1️⃣ **Comment utiliser `map`, `filter` et `reduce` sur les tableaux (arrays)**

Les **tableaux** (`Array`) sont des collections ordonnées d’éléments accessibles par indice. Trois méthodes très puissantes permettent de **transformer** ou **réduire** ces données :

### 🔹 `map()`

Crée un **nouveau tableau** contenant le résultat de l’application d’une fonction à **chaque élément** du tableau d’origine.

```javascript
const numbers = [1, 2, 3, 4];
const squared = numbers.map(n => n * n);
// [1, 4, 9, 16]
```

### 🔹 `filter()`

Crée un **nouveau tableau** avec **seulement les éléments** qui passent un test donné (fonction de filtrage).

```javascript
const numbers = [1, 2, 3, 4];
const even = numbers.filter(n => n % 2 === 0);
// [2, 4]
```

### 🔹 `reduce()`

Applique une fonction **réductrice** à chaque élément pour réduire le tableau à **une seule valeur** (accumulateur).

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, val) => acc + val, 0);
// 10
```

> 🔍 Ces méthodes sont **immutables** : elles ne modifient pas le tableau original.

🔗 [Documentation MDN - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

---

## 2️⃣ **Typed Arrays (Tableaux typés)**

Les **typed arrays** sont des objets qui permettent de **travailler avec des données binaires brutes** (raw binary data). Ils sont utilisés lorsqu’on doit **optimiser les performances** ou manipuler des flux de données (comme des images, des buffers audio, etc.).

### 🧱 Composition

Les tableaux typés reposent sur deux éléments :
- **`ArrayBuffer`** : un bloc mémoire brut.
- **Vues typées** (`Int8Array`, `Uint8Array`, `Float32Array`, etc.) : des interprétations de ce buffer sous différents types.

### 🔹 Exemple de création :

```javascript
const buffer = new ArrayBuffer(8); // 8 octets
const view = new Uint8Array(buffer);

view[0] = 255;
console.log(view[0]); // 255
```

> Chaque type (`Int8Array`, `Float64Array`, etc.) détermine la **taille et le format** des données manipulées.

🔗 [Documentation MDN - Typed Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Typed_arrays)

---

## 3️⃣ **Structures de données : Set, Map et WeakMap**

Ces structures permettent de stocker des **collections de valeurs** de manière plus efficace et spécifique que les tableaux ou objets classiques.

---

### 🟢 **Set**

Un `Set` est une **collection d’éléments uniques** (pas de doublons).

```javascript
const mySet = new Set();
mySet.add(1);
mySet.add(2);
mySet.add(2); // ignoré

console.log(mySet); // Set(2) {1, 2}
```

#### Propriétés :
- Ordre d’insertion respecté
- Méthodes : `add()`, `delete()`, `has()`, `clear()`
- Iterable avec `for...of`

🔗 [Documentation MDN - Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

---

### 🟣 **Map**

Un `Map` est une collection **clé-valeur** avec des **clés de tout type** (objets, fonctions, etc.).

```javascript
const map = new Map();
map.set("name", "Alice");
map.set(42, "answer");
map.set({ id: 1 }, "user");

console.log(map.get("name")); // Alice
```

#### Avantages :
- Les clés peuvent être de **n’importe quel type**
- L’ordre d’insertion est conservé
- Méthodes : `set()`, `get()`, `has()`, `delete()`, `clear()`

🔗 [Documentation MDN - Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

---

### ⚫ **WeakMap**

Un `WeakMap` est une **collection clé-valeur** où les **clés doivent être des objets**, et les références sont **faibles** (permettent le garbage collection).

```javascript
const wm = new WeakMap();
const obj = {};

wm.set(obj, "données associées");
console.log(wm.get(obj)); // "données associées"
```

#### Spécificités :
- Les clés doivent être des objets
- Pas itérable, pas de méthode `size()`
- Utilisé pour **cacher des données privées** liées à des objets

🔗 [Documentation MDN - WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

---

## 🧠 Résumé des différences

| Structure  | Type de données        | Ordre | Duplicats | Clés/valeurs |
|------------|------------------------|--------|-----------|----------------|
| `Array`    | Indexé, tout type      | Oui    | Oui        | Valeurs       |
| `Set`      | Valeurs uniques        | Oui    | Non        | Valeurs       |
| `Map`      | Clés de tout type      | Oui    | Clés uniques | Clé/Valeur    |
| `WeakMap`  | Clés objets uniquement | Non    | Oui        | Clé/Valeur    |
| TypedArray | Valeurs numériques     | Oui    | Oui        | Valeurs numériques (binaire) |

---

## ✨ En conclusion

JavaScript offre de **nombreuses structures et outils puissants** pour manipuler les données :

- `map`, `filter`, `reduce` : pour transformer ou agréger des tableaux.
- `TypedArray` : pour le traitement **bas niveau** et **optimisé** des données binaires.
- `Set`, `Map`, `WeakMap` : pour des cas spécifiques où **l’unicité**, la **souplesse des clés** ou la **confidentialité** sont nécessaires.

---

# 🌟 Les `Set` et la méthode `every()` en JavaScript

---

## 🔹 Partie 1 : Le type `Set`

### 📌 Qu’est-ce qu’un `Set` ?
Un **`Set`** est une **structure de données introduite avec ES6** (ECMAScript 2015). Il permet de stocker **des valeurs uniques** de tout type (primitif ou objet).

---

### 🧱 Caractéristiques principales :
- Les éléments **ne sont jamais dupliqués**.
- L’ordre d’insertion est conservé.
- Tu peux y ajouter, supprimer, ou vérifier la présence d’un élément.

---

### 📘 Création d’un `Set`
```javascript
const mySet = new Set();
```

Ou à partir d’un tableau :
```javascript
const mySet = new Set([1, 2, 3, 3, 4]);
// Résultat : Set { 1, 2, 3, 4 }
```

---

### 🔧 Méthodes utiles

| Méthode             | Description |
|---------------------|-------------|
| `add(value)`        | Ajoute une valeur |
| `delete(value)`     | Supprime une valeur |
| `has(value)`        | Retourne `true` si la valeur est présente |
| `clear()`           | Vide entièrement le set |
| `size`              | Retourne le nombre d’éléments |

---

### 🎯 Exemples pratiques
```javascript
const numbers = new Set();

numbers.add(1);
numbers.add(2);
numbers.add(2); // ignoré

console.log(numbers); // Set { 1, 2 }
console.log(numbers.has(2)); // true
console.log(numbers.size); // 2
numbers.delete(1);
console.log(numbers); // Set { 2 }
```

---

## 🔹 Partie 2 : La méthode `every()`

### 📌 Qu’est-ce que `every()` ?
`every()` est une **méthode d’itération** propre aux **tableaux**. Elle permet de tester si **tous les éléments** d’un tableau passent un test (fonction).

---

### 🧱 Syntaxe
```javascript
array.every(callback(element[, index[, array]])[, thisArg])
```

- `callback` → fonction qui retourne un booléen (`true` ou `false`)
- `every()` retourne `true` **seulement si tous les éléments** passent le test.

---

### 🎯 Exemple simple
```javascript
const ages = [21, 25, 30, 40];

const allAdults = ages.every((age) => age >= 18);
console.log(allAdults); // true
```

Un seul élément qui ne passe pas = résultat `false`.

```javascript
const ages = [21, 17, 30, 40];
const allAdults = ages.every((age) => age >= 18);
console.log(allAdults); // false
```

---

## 🔗 Exemple combiné : `Set` + `every()`
```javascript
const mySet = new Set([1, 2, 3, 4, 5]);
const arr = [2, 4];

const result = arr.every((value) => mySet.has(value));
console.log(result); // true
```

Ici, `every()` vérifie que **chaque élément de `arr` est contenu dans `mySet`** via `set.has()`.

---

## ✅ Résumé

| Notion | À retenir |
|--------|-----------|
| `Set` | Structure de données contenant **des éléments uniques** |
| `add()` / `delete()` / `has()` | Principales méthodes pour manipuler un Set |
| `every()` | Méthode des tableaux, retourne `true` si **tous** les éléments satisfont une condition |
| `Set` + `every()` | Puissant pour vérifier qu’un ensemble de valeurs est inclus dans un autre |

---
