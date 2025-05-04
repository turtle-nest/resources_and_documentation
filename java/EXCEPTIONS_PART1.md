# ☂️ **Les exceptions en Java**

*Gérer les erreurs de manière sûre et élégante*

---

## ✅ Qu'est-ce qu'une exception ? Pourquoi les utiliser ?

Une **exception** est un **événement anormal** qui interrompt le déroulement normal d’un programme.

Exemples d’exception :

* division par zéro
* accès à un index inexistant dans un tableau
* ouverture d’un fichier qui n’existe pas
* conversion invalide de chaînes de caractères

💡 En Java, **tout est objet**, même les erreurs : les exceptions sont des objets qui héritent de la classe `Throwable`.

---

## 🎯 Pourquoi attraper (catch) une exception ?

Catcher une exception permet de :

* **éviter que le programme ne plante brutalement**
* **afficher un message clair à l’utilisateur**
* **prendre une action de secours ou de récupération**
* **libérer les ressources correctement** (fichiers, connexions, etc.)

---

## 🛠️ Comment gérer les exceptions ?

### 🔹 Bloc `try` / `catch`

```java
try {
    int result = 10 / 0; // Exception ici
} catch (ArithmeticException e) {
    System.out.println("Erreur : division par zéro !");
}
```

➡️ Si une exception se produit dans le bloc `try`, elle est interceptée par le `catch`.

---

### 🔹 Bloc `finally`

Le bloc `finally` s’exécute **toujours**, qu’une exception soit levée ou non.

```java
try {
    int[] tab = {1, 2};
    System.out.println(tab[5]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Index invalide !");
} finally {
    System.out.println("Nettoyage terminé !");
}
```

---

## 💣 Lancer une exception (`throw`)

Tu peux **lancer une exception manuellement** avec le mot-clé `throw` :

```java
public void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("L'âge ne peut pas être négatif.");
    }
    this.age = age;
}
```

---

## 🧾 Déclarer une exception (`throws`)

Utilise `throws` pour indiquer qu’une méthode **peut propager une exception** :

```java
public void lireFichier(String nom) throws IOException {
    FileReader reader = new FileReader(nom);
}
```

➡️ Cela oblige le **code appelant à gérer ou relancer** l’exception.

---

## 🧨 Exceptions prédéfinies (built-in)

Java propose des centaines d’exceptions standards, dont :

| Exception                        | Quand elle se produit                          |
| -------------------------------- | ---------------------------------------------- |
| `ArithmeticException`            | Division par zéro                              |
| `NullPointerException`           | Référence sur objet nul                        |
| `ArrayIndexOutOfBoundsException` | Index de tableau invalide                      |
| `IllegalArgumentException`       | Argument invalide passé à une méthode          |
| `IOException`                    | Erreur d'entrée/sortie (fichier, réseau, etc.) |
| `NumberFormatException`          | Conversion de String vers nombre invalide      |

---

## 🧹 Nettoyage après une exception

Le bloc `finally` est **idéal pour les opérations de nettoyage**, comme :

* fermer un fichier ou une connexion
* libérer une ressource mémoire
* remettre un état initial

```java
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("file.txt"));
    // lire le fichier
} catch (IOException e) {
    System.out.println("Erreur de lecture");
} finally {
    if (reader != null) {
        reader.close(); // important !
    }
}
```

---

## ✔️ Exception vérifiée (checked) vs non vérifiée (unchecked)

### ✅ Checked Exception

* Obligatoire à **gérer (try/catch)** ou **déclarer (`throws`)**
* Hérite de `Exception` mais **pas** de `RuntimeException`
* Exemples : `IOException`, `SQLException`

```java
public void ouvrirFichier(String nom) throws IOException {
    new FileReader(nom);
}
```

---

### ❌ Unchecked Exception

* **Pas obligatoire à gérer**
* Hérite de `RuntimeException`
* Exemples : `NullPointerException`, `ArithmeticException`

```java
int x = 5 / 0; // ArithmeticException, mais pas besoin de catch obligatoire
```

---

## 🧠 Résumé en tableau

| Notion        | Description clé                                   |
| ------------- | ------------------------------------------------- |
| `try`         | Bloc contenant le code à risque                   |
| `catch`       | Capture et gère une exception                     |
| `finally`     | Exécuté **toujours**, même si une erreur survient |
| `throw`       | Lancer une exception manuellement                 |
| `throws`      | Déclarer une exception potentielle                |
| **Checked**   | Exception à **gérer ou déclarer obligatoirement** |
| **Unchecked** | Exception **non obligatoire** à attraper          |

---

## 🧪 Exemple complet

```java
import java.io.*;

public class Exemple {
    public static void main(String[] args) {
        try {
            lireFichier("inexistant.txt");
        } catch (IOException e) {
            System.out.println("Erreur : " + e.getMessage());
        } finally {
            System.out.println("Fin du programme.");
        }
    }

    public static void lireFichier(String nom) throws IOException {
        FileReader fr = new FileReader(nom);
    }
}
```

---
