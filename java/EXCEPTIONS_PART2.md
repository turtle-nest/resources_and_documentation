# 🧨 **Exceptions personnalisées en Java**

---

## 🧠 Pourquoi créer ses propres exceptions ?

Java fournit déjà beaucoup d’exceptions standards (`NullPointerException`, `IOException`, etc.), mais il peut être utile de **créer tes propres exceptions** lorsque :

* tu veux **donner plus de sens** à une erreur spécifique dans ton application
* tu veux **simplifier le traitement** d’erreurs métier récurrentes
* tu veux **clarifier le code** pour toi ou d'autres développeurs

---

## ✅ Exemple de cas métier

Tu développes un site de réservation de billets. Tu pourrais créer des exceptions comme :

* `SeatAlreadyReservedException`
* `InvalidDateRangeException`
* `NotEnoughBalanceException`

---

## 🔧 Comment créer une **exception vérifiée** (checked) ?

Une **exception vérifiée** oblige le développeur à la **gérer avec `try/catch` ou `throws`**.

### ✅ Étapes :

1. Créer une classe qui **hérite de `Exception`**
2. Ajouter un constructeur avec un message

### ✍️ Exemple :

```java
public class InvalidInputException extends Exception {
    public InvalidInputException(String message) {
        super(message);
    }
}
```

### 💡 Utilisation :

```java
public class Calculator {
    public static int divide(int a, int b) throws InvalidInputException {
        if (b == 0) {
            throw new InvalidInputException("Division par zéro interdite !");
        }
        return a / b;
    }
}
```

---

## ⚠️ Comment créer une **exception non vérifiée** (unchecked) ?

Les **exceptions non vérifiées** ne sont **pas obligatoires à gérer**, mais elles peuvent interrompre ton programme si non traitées.

### ✅ Étapes :

1. Créer une classe qui **hérite de `RuntimeException`**
2. Ajouter un constructeur

### ✍️ Exemple :

```java
public class NegativeValueException extends RuntimeException {
    public NegativeValueException(String message) {
        super(message);
    }
}
```

### 💡 Utilisation :

```java
public class Square {
    public static double area(double side) {
        if (side < 0) {
            throw new NegativeValueException("La valeur ne peut pas être négative !");
        }
        return side * side;
    }
}
```

---

## 🧪 Exemple complet avec test

```java
public class Program {
    public static void main(String[] args) {
        try {
            int result = Calculator.divide(10, 0);
            System.out.println(result);
        } catch (InvalidInputException e) {
            System.out.println("Erreur : " + e.getMessage());
        }

        double aire = Square.area(-5); // non vérifiée, pas de try/catch requis
        System.out.println(aire);
    }
}
```

---

## 🔍 Résumé

| Type d’exception | Classe parente     | Obligatoire à gérer ? | Exemple de classe        |
| ---------------- | ------------------ | --------------------- | ------------------------ |
| **Checked**      | `Exception`        | ✅ Oui                 | `InvalidInputException`  |
| **Unchecked**    | `RuntimeException` | ❌ Non                 | `NegativeValueException` |

---

## 🧩 Bonnes pratiques

* Préfère des **noms explicites** : `FileTooLargeException`, `EmptyNameException`, etc.
* Étends **`Exception`** pour forcer la gestion (`try/catch`)
* Étends **`RuntimeException`** si l’erreur est rare mais fatale (ex : fail-fast)

---
