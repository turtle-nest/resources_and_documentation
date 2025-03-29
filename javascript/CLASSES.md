# Classes

---

### ❓ **How to define a Class**

🟩 **Réponse en français :**

En JavaScript, on définit une classe à l’aide du mot-clé `class`. Le **constructeur** est une méthode spéciale appelée automatiquement lors de la création d’un nouvel objet avec `new`. C’est là qu’on initialise les propriétés de l’objet.

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const john = new Person("John", 25);
```

🟦 **Notions en anglais :**

- A class is a blueprint for creating objects.
- `constructor()` is used to initialize object properties.
- You instantiate a class using the `new` keyword.

---

### ❓ **How to add methods to a class**

🟩 **Réponse en français :**

Pour ajouter des méthodes à une classe, on les écrit directement à l’intérieur du corps de la classe, mais en dehors du constructeur. Ces méthodes seront partagées par toutes les instances via le prototype.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Bonjour, je m'appelle ${this.name}`);
  }
}
```

🟦 **Notions en anglais :**

- Methods defined inside the class are automatically added to the prototype.
- This avoids duplicating function definitions in each instance.
- You can also use getters and setters for encapsulation.

---

### ❓ **Why and how to add a static method to a class**

🟩 **Réponse en français :**

Une méthode statique (`static`) est une méthode qui **appartient à la classe elle-même**, et non aux objets créés à partir de cette classe. Elle est utile pour définir des méthodes utilitaires ou des méthodes de création.

```javascript
class MathUtils {
  static square(n) {
    return n * n;
  }
}

console.log(MathUtils.square(4)); // 16
```

🟦 **Notions en anglais :**

- `static` methods can be called on the class, not on instances.
- Common use cases: utility functions, factories, global operations.
- You can't access instance properties (`this.prop`) inside static methods unless passing the object.

---

### ❓ **How to extend a class from another**

🟩 **Réponse en français :**

Pour créer une classe qui hérite d’une autre, on utilise le mot-clé `extends`. La classe enfant peut appeler le constructeur parent avec `super()` et hérite des méthodes de la classe parente.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} fait un bruit`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} aboie`);
  }
}

const dog = new Dog("Rex");
dog.speak(); // Rex aboie
```

🟦 **Notions en anglais :**

- Use `extends` to create a subclass.
- `super()` calls the constructor of the base class.
- Subclasses override or add new behavior.
- JavaScript supports single inheritance via prototype chains.

---

### ❓ **Metaprogramming and symbols**

🟩 **Réponse en français :**

#### 🔧 **Métaprogrammation**

La métaprogrammation consiste à **écrire du code qui manipule d’autres structures de code**. En JavaScript, cela se fait principalement avec :

- `Proxy` : permet d’intercepter les opérations sur les objets.
- `Reflect` : donne un accès aux comportements par défaut (utile avec Proxy).
- `Object.defineProperty()` : permet de personnaliser l’accès aux propriétés.

Exemple avec Proxy :

```javascript
const handler = {
  get(target, prop) {
    return prop in target ? target[prop] : "Propriété inconnue";
  }
};

const user = new Proxy({ name: "Alice" }, handler);
console.log(user.name); // Alice
console.log(user.age);  // Propriété inconnue
```

#### 🧿 **Symboles**

Les symboles (`Symbol`) sont des **identifiants uniques** souvent utilisés pour créer des propriétés non accessibles de façon classique (presque privées) ou pour modifier le comportement natif des objets.

```javascript
const id = Symbol("id");
const obj = {
  [id]: 123,
  name: "Bob"
};

console.log(obj[id]); // 123
```

Certains symboles prédéfinis permettent de personnaliser les comportements :

- `Symbol.iterator` → pour rendre un objet itérable.
- `Symbol.toPrimitive` → pour personnaliser la conversion de type.
- `Symbol.hasInstance` → personnaliser le comportement de `instanceof`.

🟦 **Notions en anglais :**

- **Metaprogramming** allows customizing how objects behave.
- **Proxy** lets you define traps (interceptors) for object operations.
- **Reflect** allows default behavior execution inside Proxies.
- **Symbols** are unique identifiers used to avoid property name collisions.
- Built-in symbols modify object internals like iteration and type coercion.

---
