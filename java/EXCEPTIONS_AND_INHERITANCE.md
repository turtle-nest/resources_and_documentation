# 🧰 TUTORIEL COMPLET – CLASSES, HÉRITAGE & EXCEPTIONS EN JAVA

Voici un **tutoriel complet en français** qui réunit toutes ces notions :

* ✅ les **classes et objets**
* 🛠️ les **constructeurs et méthodes**
* 🧱 les **getters/setters**
* 🧨 la **gestion des exceptions**
* 🧬 l’**héritage** et la **surcharge de méthodes**
* 📦 les **packages**
* ✅ les **exceptions personnalisées**

Ce cours est conçu comme un **guide de référence structuré**, progressif et clair. 
---

## 📌 1. Les classes et objets

Une **classe** est un modèle pour créer des **objets**. Elle regroupe :

* des **attributs** (état de l’objet)
* des **méthodes** (comportement de l’objet)

### Exemple minimal :

```java
public class Person {
    String name;
    int age;

    public void sayHello() {
        System.out.println("Bonjour, je m'appelle " + name);
    }
}
```

---

## ⚙️ 2. Constructeur

Le **constructeur** initialise un objet lors de sa création avec `new`.

```java
public Person(String name, int age) {
    this.name = name;
    this.age = age;
}
```

---

## 🧱 3. Getters et Setters (accès contrôlé)

### Pourquoi ?

* Encapsulation : protéger les données
* Validation : imposer des règles

```java
private String title;

public String getTitle() {
    return title;
}

public void setTitle(String title) {
    if (title.length() < 3) {
        throw new IllegalArgumentException("Titre invalide");
    }
    this.title = title;
}
```

---

## 🧨 4. Exceptions en Java

Java distingue :

| Type                    | Héritage                   | Obligation de gestion |
| ----------------------- | -------------------------- | --------------------- |
| **Checked** exception   | `extends Exception`        | ✅ try/catch ou throws |
| **Unchecked** exception | `extends RuntimeException` | ❌ facultatif          |

### Créer une exception personnalisée :

```java
public class InvalidBookException extends Exception {
    public InvalidBookException(String message) {
        super(message);
    }
}
```

### Lever une exception :

```java
if (price <= 0) {
    throw new InvalidBookException("Prix invalide");
}
```

---

## 📦 5. Packages

Les **packages** permettent d’organiser le code.

### Exemple :

```java
package exceptions;

public class InvalidBookException extends Exception {
    ...
}
```

### Pour utiliser une classe d’un package :

```java
import exceptions.InvalidBookException;
```

---

## 🧬 6. Héritage (`extends`) et redéfinition (`@Override`)

### Héritage :

```java
public class GoldEditionBook extends Book {
    ...
}
```

### Redéfinir une méthode :

```java
@Override
public double getPrice() {
    return super.getPrice() * 1.3;
}
```

---

## 🧪 Exemple complet : Livre, validations, édition spéciale

### 📘 Classe `Book`

```java
public class Book {
    private String title;
    private String author;
    private double price;

    public Book(String title, String author, double price)
        throws InvalidBookException, InvalidAuthorException {
        setTitle(title);
        setAuthor(author);
        setPrice(price);
    }

    public void setTitle(String title) throws InvalidBookException {
        if (title == null || title.length() < 3) {
            throw new InvalidBookException("Titre invalide");
        }
        this.title = title;
    }

    public void setAuthor(String author) throws InvalidAuthorException {
        if (author == null || author.trim().split("\\s+").length < 2) {
            throw new InvalidAuthorException("Nom d'auteur invalide");
        }
        this.author = author;
    }

    public void setPrice(double price) throws InvalidBookException {
        if (price <= 0) {
            throw new InvalidBookException("Prix invalide");
        }
        this.price = price;
    }

    public double getPrice() {
        return this.price;
    }

    public String getTitle() {
        return this.title;
    }

    public String getAuthor() {
        return this.author;
    }
}
```

---

### 🥇 Classe `GoldEditionBook` (héritée)

```java
public class GoldEditionBook extends Book {
    public GoldEditionBook(String title, String author, double price)
        throws InvalidBookException, InvalidAuthorException {
        super(title, author, price);
    }

    @Override
    public double getPrice() {
        return super.getPrice() * 1.3;
    }
}
```

---

### 💥 Exceptions personnalisées

```java
// exceptions/InvalidBookException.java
package exceptions;

public class InvalidBookException extends Exception {
    public InvalidBookException(String message) {
        super(message);
    }
}
```

```java
// exceptions/InvalidAuthorException.java
package exceptions;

public class InvalidAuthorException extends Exception {
    public InvalidAuthorException(String message) {
        super(message);
    }
}
```

---

## 🧪 Programme principal

```java
import exceptions.InvalidBookException;
import exceptions.InvalidAuthorException;

public class Program {
    public static void main(String[] args) {
        try {
            Book b = new Book("1984", "George Orwell", 20);
            Book gold = new GoldEditionBook("1984", "George Orwell", 20);

            System.out.println("Livre : " + b.getTitle() + " - " + b.getPrice());
            System.out.println("Édition Gold : " + gold.getTitle() + " - " + gold.getPrice());

        } catch (InvalidBookException | InvalidAuthorException e) {
            System.out.println("Erreur : " + e.getMessage());
        }
    }
}
```

---

## 🧠 Bonnes pratiques à retenir

| Bonne pratique                       | Pourquoi ?                                    |
| ------------------------------------ | --------------------------------------------- |
| Utiliser `private` + getters/setters | Encapsulation et validation                   |
| Valider les entrées dans les setters | Éviter les objets dans un état invalide       |
| Utiliser `@Override`                 | Pour redéfinir clairement une méthode héritée |
| Lever des exceptions précises        | Pour déboguer facilement                      |
| Organiser le code en `packages`      | Pour la lisibilité et la maintenabilité       |

---
