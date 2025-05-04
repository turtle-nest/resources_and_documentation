# 📘 Fiche Tutoriel Java : Méthodes, Conditions, Boucles et Contrôle de Flux

---

## 🧮 1. Opérateurs en Java

### 🔢 **Opérateurs arithmétiques**
| Opérateur | Signification | Exemple (`a = 10`, `b = 3`) |
|-----------|---------------|-----------------------------|
| `+`       | Addition       | `a + b → 13`                |
| `-`       | Soustraction   | `a - b → 7`                 |
| `*`       | Multiplication | `a * b → 30`                |
| `/`       | Division       | `a / b → 3` (division entière) |
| `%`       | Modulo         | `a % b → 1`                 |

---

### 🧮 **Opérateurs relationnels**
| Opérateur | Signification        | Exemple |
|-----------|----------------------|---------|
| `==`      | Égal à               | `a == b` |
| `!=`      | Différent de         | `a != b` |
| `>`       | Supérieur à          | `a > b`  |
| `<`       | Inférieur à          | `a < b`  |
| `>=`      | Supérieur ou égal    | `a >= b` |
| `<=`      | Inférieur ou égal    | `a <= b` |

---

### 🔁 **Opérateurs logiques**
| Opérateur | Signification      | Exemple                        |
|-----------|--------------------|--------------------------------|
| `&&`      | ET logique          | `(a > 5 && b < 5)`             |
| `||`      | OU logique          | `(a > 5 || b > 5)`             |
| `!`       | NON logique (négation) | `!(a == b)`                |

---

### 📐 **Ordre de priorité**
1. Parenthèses `()`
2. Post-incrément `a++`, pré-incrément `++a`
3. Multiplication, division, modulo
4. Addition, soustraction
5. Relationnels (`<`, `>`, `==`, `!=`)
6. Logiques (`&&`, `||`)

---

## 🔀 2. Structures conditionnelles

### ✅ **`if`, `else if`, `else`**
```java
if (age < 18) {
    System.out.println("Mineur");
} else if (age < 65) {
    System.out.println("Adulte");
} else {
    System.out.println("Senior");
}
```

### 🔄 **`switch`**
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Lundi");
        break;
    case 2:
        System.out.println("Mardi");
        break;
    default:
        System.out.println("Autre jour");
}
```
> 🔹 Le mot-clé `break` permet d'éviter que tous les `case` suivants s'exécutent.

---

## 🔁 3. Boucles en Java

### 🔄 **`while`**
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

### 🔂 **`do while`**
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

### 🔁 **`for`**
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

---

## 🧭 4. Contrôle de flux

### 🛑 **`break`**
Interrompt une boucle ou un `switch`.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    System.out.println(i);
}
```

### 🔄 **`continue`**
Passe à l’itération suivante sans terminer l’itération en cours.

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;
    System.out.println(i);
}
```

---

## 🔧 5. Déclarer des méthodes dans une classe

```java
public class Calculatrice {

    public int addition(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calculatrice calc = new Calculatrice();
        System.out.println(calc.addition(3, 4));
    }
}
```

| Élément            | Description                         |
|--------------------|-------------------------------------|
| `public`           | Visibilité accessible depuis d'autres classes |
| `int addition(...)`| Méthode qui retourne un entier       |
| `this.addition()`  | Appel interne                        |
| `new Calculatrice()` | Création d'une instance             |

---

## ☎️ 6. Appeler une méthode publique depuis une autre classe

### Exemple sur deux classes :

```java
// Fichier Utilisateur.java
public class Utilisateur {
    public void direBonjour() {
        System.out.println("Bonjour !");
    }
}
```

```java
// Fichier Main.java
public class Main {
    public static void main(String[] args) {
        Utilisateur u = new Utilisateur();
        u.direBonjour();
    }
}
```

---

## ✅ En résumé

| Notion | À retenir |
|--------|-----------|
| **Opérateurs** | Arithmétiques, relationnels, logiques, précédence |
| **Conditions** | if, else, else if, switch |
| **Boucles** | while, do while, for |
| **Contrôle** | break (arrêt), continue (saut) |
| **Méthodes** | Déclarées dans une classe, appelées depuis d’autres |
| **Encapsulation** | Une méthode `public` peut être appelée si on a une instance |

---
