# Basics

---

## 🌟 Qu’est-ce que ES6 ?

**ES6** (ECMAScript 6 ou ECMAScript 2015) est une mise à jour majeure du langage **JavaScript**, publiée en 2015. Elle introduit de nombreuses fonctionnalités visant à rendre le code **plus concis, lisible, modulaire et puissant**.

C’est cette version qui a marqué le passage d’un JavaScript plus basique à un JavaScript **moderne**, très utilisé aujourd’hui dans le développement web (notamment avec React, Vue, Node.js, etc.).

---

## 🚀 Nouvelles fonctionnalités introduites par ES6

Voici les **principales nouveautés** apportées par ES6 :

- `let` et `const` pour la déclaration de variables
- Les **fonctions fléchées** (arrow functions)
- Les **valeurs par défaut** pour les paramètres de fonction
- Le **template string** (chaînes de caractères avec interpolation)
- Le **destructuring** (extraction des valeurs d’un objet ou d’un tableau)
- Les **objets littéraux** simplifiés
- Le **rest operator** (`...args`) et le **spread operator** (`...array`)
- Les **promesses** (`Promise`)
- Les **modules** (`import` / `export`)
- Les **classes**
- Les **boucles for-of**
- Les **symboles** et les **itérateurs**

---

## 🔁 Différence entre une constante et une variable

- `let` → permet de **déclarer une variable** qui peut être modifiée plus tard.
- `const` → permet de **déclarer une constante**, c’est-à-dire une **valeur qui ne changera pas** (assignation unique).

```javascript
let age = 25;
age = 26; // OK

const name = "Alice";
name = "Bob"; // ❌ Erreur : on ne peut pas réassigner une const
```

⚠️ Attention : si `const` pointe vers un **objet ou un tableau**, les **valeurs internes** peuvent changer, mais pas la **référence**.

```javascript
const user = { name: "Alice" };
user.name = "Bob"; // ✅ Modifiable
```

---

## 📦 Les variables à portée de bloc (block-scoped)

Avec `let` et `const`, les variables ont une **portée limitée au bloc `{}`** dans lequel elles sont déclarées. Contrairement à `var`, qui est **function-scoped**.

```javascript
{
  let a = 10;
  const b = 20;
}
// console.log(a); ❌ Erreur : a n'existe pas ici
```

Cela permet d’éviter les **effets de bord** et de rendre le code plus sûr et lisible.

---

## 🏹 Les fonctions fléchées (arrow functions) et les paramètres par défaut

### Fonctions fléchées (arrow functions)

Elles permettent une **syntaxe plus courte** pour écrire des fonctions anonymes.

```javascript
// Fonction classique
function add(x, y) {
  return x + y;
}

// Fonction fléchée équivalente
const add = (x, y) => x + y;
```

### Particularité : le `this`

Les fonctions fléchées ne créent pas leur propre contexte `this`. Elles héritent du `this` de l’environnement parent. Cela évite certains bugs classiques.

```javascript
const user = {
  name: "Alice",
  sayHello: function () {
    setTimeout(() => {
      console.log(`Bonjour, je suis ${this.name}`); // this = user
    }, 1000);
  },
};
```

### Paramètres par défaut

Tu peux définir des valeurs par défaut pour les paramètres d’une fonction :

```javascript
const greet = (name = "invité") => {
  console.log(`Bonjour, ${name}`);
};

greet(); // Bonjour, invité
```

---

## 📚 Les paramètres rest et spread

### Rest parameters `...`

Permet de **regrouper** un nombre **illimité de paramètres** dans un tableau :

```javascript
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3); // 6
```

### Spread operator `...`

Permet de **décomposer** un tableau ou un objet :

```javascript
const arr = [1, 2, 3];
const newArr = [...arr, 4]; // [1, 2, 3, 4]

const obj = { name: "Alice" };
const newObj = { ...obj, age: 30 }; // { name: "Alice", age: 30 }
```

---

## 🧵 L’interpolation de chaînes (template strings)

Les **template literals** permettent d’**insérer des variables** ou expressions dans une chaîne, avec une syntaxe très lisible :

```javascript
const name = "Bob";
const age = 30;

console.log(`Je m'appelle ${name} et j'ai ${age} ans.`);
```

Fini les longues concaténations avec `+` !

---

## 🧱 Création d’objets et propriétés raccourcies

### Syntaxe raccourcie :

Si le nom de la propriété est le même que le nom de la variable, on peut **écrire plus court** :

```javascript
const name = "Alice";
const age = 25;

const user = { name, age };
console.log(user); // { name: "Alice", age: 25 }
```

### Méthodes dans un objet (raccourci ES6) :

```javascript
const user = {
  greet() {
    console.log("Bonjour !");
  },
};
```

---

## 🔄 Les itérateurs et la boucle for-of

### for-of

Permet de **parcourir les éléments** d’un tableau, d’un `Set`, d’un `Map` ou tout objet **itérable** :

```javascript
const fruits = ["pomme", "banane", "orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

> Avantage : `for-of` est plus simple que `forEach` ou `for` pour accéder directement aux valeurs.

### Itérateurs

Un **itérateur** est un objet qui implémente la méthode `.next()`, qui retourne un objet `{ value, done }`.

Exemple simple d’un itérateur personnalisé :

```javascript
function createIterator() {
  let i = 0;
  return {
    next: () => {
      if (i < 3) {
        return { value: i++, done: false };
      } else {
        return { done: true };
      }
    },
  };
}

const it = createIterator();
console.log(it.next()); // { value: 0, done: false }
console.log(it.next()); // { value: 1, done: false }
```

---

## 📘 Résumé

| Fonctionnalité      | Description courte                                    |
|---------------------|--------------------------------------------------------|
| `let` / `const`     | Déclarations avec portée de bloc (`const` non modifiable) |
| Arrow functions     | Syntaxe courte, `this` hérité                          |
| Template strings    | Chaînes avec `${}` pour interpolation                  |
| Rest/Spread         | `...args` pour capturer / étendre des tableaux/objets |
| Objet ES6           | Syntaxe raccourcie pour les propriétés et méthodes    |
| For-of              | Parcourt les **valeurs** directement                  |
| Paramètres par défaut | Permet de donner une valeur par défaut aux paramètres |

---
