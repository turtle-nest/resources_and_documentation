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

# 🎓 Cours : `join()`, `startsWith()` et `slice()`

---

## 🔹 1. `join()` — méthode des tableaux

### 📌 Définition :
`join()` est une méthode des **tableaux** qui permet de **fusionner tous les éléments** d’un tableau en **une seule chaîne de caractères**, en les séparant par un **séparateur** que tu choisis.

### 🧱 Syntaxe :
```javascript
array.join(separator)
```

- `separator` est **optionnel**. Par défaut, c’est une **virgule (`,`)**.

---

### 🎯 Exemples :
```javascript
const fruits = ['pomme', 'banane', 'kiwi'];

console.log(fruits.join());         // "pomme,banane,kiwi"
console.log(fruits.join(' - '));    // "pomme - banane - kiwi"
console.log(fruits.join(''));       // "pommebananekiwis"
```

---

### 💡 Astuce :
Très utile pour convertir un tableau en chaîne, par exemple pour afficher une liste ou générer une URL.

---

## 🔹 2. `startsWith()` — méthode des chaînes

### 📌 Définition :
`startsWith()` permet de **tester si une chaîne commence** par un certain texte (préfixe). Elle retourne un **booléen** (`true` ou `false`).

### 🧱 Syntaxe :
```javascript
string.startsWith(searchString[, position])
```

- `searchString` : la chaîne à rechercher.
- `position` : position facultative à partir de laquelle commencer la recherche (par défaut 0).

---

### 🎯 Exemples :
```javascript
const phrase = "Bonjour tout le monde";

console.log(phrase.startsWith("Bon"));     // true
console.log(phrase.startsWith("jour"));    // false
console.log(phrase.startsWith("tout", 7)); // true
```

---

### 💡 Astuce :
Très utile pour filtrer des chaînes de texte ou des éléments dans un tableau.

---

## 🔹 3. `slice()` — méthode des chaînes ET des tableaux

### 📌 Définition :
`slice()` retourne une **copie d’une portion** de chaîne ou de tableau, **sans modifier l’original**.

### 🧱 Syntaxe pour une chaîne :
```javascript
string.slice(beginIndex[, endIndex])
```

- `beginIndex` : indice de début (inclus).
- `endIndex` : indice de fin (exclu). Si absent, va jusqu’à la fin.

---

### 🧱 Syntaxe pour un tableau :
```javascript
array.slice(begin[, end])
```

---

### 🎯 Exemples avec des chaînes :
```javascript
const mot = "banane";

console.log(mot.slice(1));      // "anane"
console.log(mot.slice(0, 3));   // "ban"
console.log(mot.slice(-2));     // "ne"
```

---

### 🎯 Exemples avec des tableaux :
```javascript
const nombres = [10, 20, 30, 40];

console.log(nombres.slice(1));     // [20, 30, 40]
console.log(nombres.slice(1, 3));  // [20, 30]
console.log(nombres.slice(-2));   // [30, 40]
```

---

### 💡 Astuce :
- Avec les chaînes : utile pour **supprimer un préfixe ou suffixe**
- Avec les tableaux : permet de **copier** ou **extraire** une partie du tableau

---

## ✅ Résumé rapide

| Méthode       | Type       | Usage principal                             |
|---------------|------------|---------------------------------------------|
| `join()`      | Tableau    | Fusionne les éléments en une chaîne         |
| `startsWith()`| Chaîne     | Vérifie le début d’une chaîne               |
| `slice()`     | Chaîne / Tableau | Extrait une portion sans modifier l’original |

---

# 🧠 Cours : `push()` en JavaScript

---

## 🔹 Qu’est-ce que `.push()` ?

La méthode **`push()`** est une **méthode native des tableaux** en JavaScript. Elle permet **d’ajouter un ou plusieurs éléments à la fin d’un tableau**.

C’est l’équivalent d’un "append" dans d’autres langages comme Python.

---

## 🧱 Syntaxe

```javascript
array.push(element1, element2, ..., elementN)
```

- Tu peux ajouter **un ou plusieurs éléments** à la fois.
- La méthode retourne **la nouvelle longueur** du tableau après l’ajout.

---

## 🎯 Exemples

### 🔸 Ajouter un élément
```javascript
const fruits = ['pomme', 'banane'];
fruits.push('kiwi');

console.log(fruits); // ["pomme", "banane", "kiwi"]
```

### 🔸 Ajouter plusieurs éléments
```javascript
const nombres = [1, 2];
const nouvelleLongueur = nombres.push(3, 4, 5);

console.log(nombres);         // [1, 2, 3, 4, 5]
console.log(nouvelleLongueur); // 5
```

---

## 🔎 Différence avec `unshift()`

| Méthode     | Ajoute où ?    | Exemples |
|-------------|----------------|----------|
| `push()`    | **À la fin**   | `[1, 2].push(3) → [1, 2, 3]` |
| `unshift()` | **Au début**   | `[1, 2].unshift(0) → [0, 1, 2]` |

---

## ⚠️ Attention

- `push()` **modifie directement le tableau** d'origine (c’est une méthode *mutative*).
- Si tu veux créer un **nouveau tableau**, utilise l’opérateur **spread** `[...tableau, nouvelElement]`.

```javascript
const original = [1, 2];
const nouveau = [...original, 3];

console.log(original); // [1, 2]
console.log(nouveau);  // [1, 2, 3]
```

---

## ✅ Résumé

| Point clé              | Détail                                      |
|------------------------|---------------------------------------------|
| Type                   | Méthode de tableau                          |
| Rôle                   | Ajouter à la **fin** du tableau             |
| Retourne               | La **nouvelle longueur** du tableau         |
| Altère le tableau ?    | **Oui**                                     |
| Alternatives           | `unshift()` (début), `[...arr, x]` (copie) |

---

## ✅ Objectif
Créer une fonction `groceriesList` qui retourne une **`Map`** avec des paires (nom, quantité) de produits alimentaires :

| Nom       | Quantité |
|-----------|----------|
| Apples    | 10       |
| Tomatoes  | 10       |
| Pasta     | 1        |
| Rice      | 1        |
| Banana    | 5        |

---

### 🔸 `Map` en JavaScript :
Une **Map** est une structure de données **clé → valeur** introduite par ES6.

Contrairement aux objets `{}`, une `Map` :
- Peut avoir **des clés de tout type**
- **Garde l’ordre d’insertion**
- Est **plus performante** pour certaines opérations

### 🔸 Création d’une Map :
Tu peux initialiser une `Map` à partir d’un tableau contenant des sous-tableaux `[clé, valeur]`.

```javascript
new Map([
  ['clé1', valeur1],
  ['clé2', valeur2]
])
```

---

# 🎓 Cours JavaScript : `.set()` et la structure `Map`

---

## 🔹 Qu’est-ce qu’une `Map` ?

La **`Map`** est une **structure de données introduite en ES6 (ECMAScript 2015)**. C’est un objet spécial qui associe des **clés à des valeurs**, un peu comme un objet `{}`, mais avec **plus de souplesse** et de **performances améliorées**.

---

## 🧱 Syntaxe de base de `.set()`

```javascript
map.set(clé, valeur)
```

- `clé` : n’importe quel type de données (chaîne, nombre, objet, etc.)
- `valeur` : valeur associée à la clé
- **Retourne** la Map elle-même (ce qui permet le chaînage)

---

## 🧪 Exemple simple

```javascript
const map = new Map();

map.set('pomme', 3);
map.set('banane', 5);
map.set('kiwi', 1);

console.log(map);
// Map { 'pomme' => 3, 'banane' => 5, 'kiwi' => 1 }
```

---

## 🔁 Clés de tout type

Contrairement à un objet `{}`, une `Map` accepte **n’importe quel type de clé** :

```javascript
const map = new Map();

map.set('nom', 'Alice');         // chaîne
map.set(42, 'réponse');          // nombre
map.set(true, 'oui');            // booléen
map.set({ id: 1 }, 'objet clé'); // objet

console.log(map.get(42));        // "réponse"
```

---

## 🔄 Mise à jour d'une valeur

Si tu fais un `.set()` sur une clé **déjà existante**, la valeur est **mise à jour** :

```javascript
map.set('pomme', 10); // modifie la quantité de pommes
```

---

## 🔗 Chaînage

La méthode `.set()` retourne la Map, donc tu peux enchaîner les appels :

```javascript
const map = new Map()
  .set('tomate', 2)
  .set('carotte', 3)
  .set('poireau', 1);
```

---

## 📘 Comparaison avec un objet `{}`

| Caractéristique         | `Map`                   | Objet `{}`              |
|-------------------------|-------------------------|--------------------------|
| Type de clé             | **Tous types**          | Uniquement chaînes/symboles |
| Ordre d'insertion       | **Préservé**            | Non garanti             |
| Taille (`size`)         | `.size`                 | `Object.keys(obj).length` |
| Méthode d’ajout         | `.set(clé, valeur)`     | `obj[clé] = valeur`     |
| Itérable directement    | ✅ Oui                  | ❌ Non, sauf avec `Object.entries()` |

---

## 🛠️ Méthodes associées utiles

| Méthode      | Rôle |
|--------------|------|
| `.set(k, v)` | Ajoute ou met à jour une entrée |
| `.get(k)`    | Récupère la valeur associée à `k` |
| `.has(k)`    | Vérifie si la clé `k` existe |
| `.delete(k)` | Supprime l’entrée de clé `k` |
| `.clear()`   | Vide complètement la Map |
| `.size`      | Nombre d’éléments dans la Map |

---

## ✅ Résumé

- `.set()` est la méthode principale pour **ajouter ou modifier une entrée** dans une `Map`.
- Elle accepte **n’importe quel type de clé**.
- Elle retourne la `Map` elle-même (permettant le chaînage).
- Les `Map` sont **plus puissantes et flexibles** que les objets `{}` classiques pour les structures associatives.

---

## Comprendre la **différence entre** :

- `export default`
- `export` (aussi appelé **named export**)

Et comment les **importer correctement**.

---

## 🟢 1. **`export default`** — Exportation par défaut

### 📌 Définition :
C’est **l’élément principal** exporté par un fichier.  
Un seul `export default` est autorisé **par fichier**.

### ✅ Exemple :

```js
// utils.js
export default function uploadPhoto() {
  return 'photo uploaded';
}
```

### ✅ Import :

```js
// autre fichier
import uploadPhoto from './utils.js';
```

📌 ➤ On peut lui donner **le nom qu’on veut** (mais par convention on garde le même).

---

## 🟠 2. **`named export`** — Exportation nommée

### 📌 Définition :
Permet d’**exporter plusieurs éléments** dans le même fichier (fonctions, constantes, classes…).

### ✅ Exemple :

```js
// utils.js
export function createUser() {
  return 'user created';
}

export const API_URL = 'https://...';
```

### ✅ Import :

```js
// autre fichier
import { createUser, API_URL } from './utils.js';
```

📌 ➤ **Les noms doivent correspondre exactement** à ceux utilisés lors de l’export.

---

## 🔁 Combiner les deux (⚠️ possible mais à utiliser avec modération)

```js
// utils.js
export default function uploadPhoto() {
  return 'photo';
}

export function createUser() {
  return 'user';
}
```

### ✅ Import combiné :

```js
import uploadPhoto, { createUser } from './utils.js';
```

---

## ❌ Erreurs fréquentes

| Mauvais code | Pourquoi c’est faux ? |
|--------------|------------------------|
| `import { uploadPhoto }` d’un `export default` | ❌ On ne met pas `{}` pour un `default` |
| `import createUser from './utils.js'` si c’est un `named export` | ❌ Pas de `default` → il faut des `{}` |

---

## 📌 Récapitulatif visuel

| Export             | Syntaxe export                        | Syntaxe import                          |
|--------------------|----------------------------------------|------------------------------------------|
| `default`          | `export default function ...`          | `import nom from './...'`               |
| `named`            | `export function nom() {}`             | `import { nom } from './...'`           |
| `les deux combinés`| `export default` + `export { ... }`   | `import defaut, { nom } from './...'`   |

---

## 🎯 À retenir

- ✔️ `export default` → un seul par fichier, sans `{}` à l'import
- ✔️ `named export` → plusieurs possibles, avec `{}` à l'import
- ❗ Tu ne peux pas utiliser deux `export default` dans un même fichier

---
