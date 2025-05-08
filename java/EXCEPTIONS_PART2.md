# 🧨 Tutoriel : Exceptions personnalisées en Java

---

## 🔍 1. Pourquoi créer ses propres exceptions ?

Java propose déjà de nombreuses exceptions standard (comme `NullPointerException`, `IOException`, etc.). Pourtant, dans un projet réel, il peut être utile de créer **ses propres exceptions personnalisées**, notamment pour :

* **Nommer précisément** les erreurs spécifiques à ton domaine métier (ex. `CompteInexistantException`)
* **Rendre le code plus clair** et lisible pour toi et tes coéquipiers
* **Séparer la logique métier des erreurs techniques**
* Permettre un **traitement d’erreurs ciblé** (grâce au nom de la classe)

💡 C’est aussi une **bonne pratique recommandée** dans tous les projets Java bien structurés.

---

## 🛠️ 2. Comment créer une **exception personnalisée** ?

Une **exception personnalisée** est simplement une **classe Java** qui **hérite d'une classe d’exception existante**, comme :

* `Exception` → pour une **exception vérifiée** (*checked*)
* `RuntimeException` → pour une **exception non vérifiée** (*unchecked*)

---

## ✅ 3. Créer une **exception vérifiée** (checked)

Les **checked exceptions** doivent être **gérées** (`try/catch`) ou **déclarées** avec `throws`.

### ✍️ Exemple :

```java
public class SoldeInsuffisantException extends Exception {
    public SoldeInsuffisantException(String message) {
        super(message);
    }
}
```

### 💡 Utilisation :

```java
public class Banque {
    public void retirer(double montant) throws SoldeInsuffisantException {
        if (montant > 1000) {
            throw new SoldeInsuffisantException("Montant trop élevé !");
        }
        System.out.println("Retrait autorisé.");
    }
}
```

---

## ❌ 4. Créer une **exception non vérifiée** (unchecked)

Les **unchecked exceptions** ne sont **pas obligatoires** à gérer avec `try/catch`. Elles sont souvent utilisées pour les erreurs **programmatiques** (ex : division par zéro, argument invalide...).

### ✍️ Exemple :

```java
public class ValeurNegativeException extends RuntimeException {
    public ValeurNegativeException(String message) {
        super(message);
    }
}
```

### 💡 Utilisation :

```java
public class MathUtils {
    public static int racineCarree(int x) {
        if (x < 0) {
            throw new ValeurNegativeException("Impossible de calculer la racine d’un nombre négatif !");
        }
        return (int) Math.sqrt(x);
    }
}
```

---

## 🧪 5. Utiliser une exception personnalisée

Tu peux utiliser tes exceptions comme n'importe quelle autre :

```java
public class Program {
    public static void main(String[] args) {
        try {
            Banque banque = new Banque();
            banque.retirer(1500);
        } catch (SoldeInsuffisantException e) {
            System.out.println("Erreur : " + e.getMessage());
        }

        int result = MathUtils.racineCarree(9); // ok
        System.out.println("Résultat : " + result);

        result = MathUtils.racineCarree(-1); // déclenche exception non vérifiée
    }
}
```

📝 Résultat :

```
Erreur : Montant trop élevé !
Résultat : 3
Exception in thread "main" ValeurNegativeException: Impossible de calculer...
```

---

## 📌 6. Bonnes pratiques à suivre

✅ Recommandées :

* Nom explicite en `PascalCase`, finissant souvent par `Exception`
* Ajouter au minimum un **constructeur avec message**
* Hériter de `Exception` pour les erreurs métier **attendues**
* Hériter de `RuntimeException` pour les erreurs **de logique programmative**
* Éviter les exceptions vides (sans message)

❌ À éviter :

* Utiliser `Exception` ou `Throwable` de manière générique
* Lancer des exceptions sans message
* Abuser des checked exceptions pour tout (cela rend le code verbeux)

---

## 📚 Résumé

| Exception                   | Classe parente     | Gérée obligatoirement ?   | Usage typique                         |
| --------------------------- | ------------------ | ------------------------- | ------------------------------------- |
| `SoldeInsuffisantException` | `Exception`        | ✅ Oui (`try` ou `throws`) | Erreur métier attendue                |
| `ValeurNegativeException`   | `RuntimeException` | ❌ Non                     | Vérification de logique ou invalidité |

---

## ✅ Exemple final de structure

```java
// Fichier : SoldeInsuffisantException.java
public class SoldeInsuffisantException extends Exception {
    public SoldeInsuffisantException(String message) {
        super(message);
    }
}

// Fichier : Banque.java
public class Banque {
    public void retirer(double montant) throws SoldeInsuffisantException {
        if (montant > 1000) {
            throw new SoldeInsuffisantException("Montant trop élevé !");
        }
    }
}

// Fichier : Program.java
public class Program {
    public static void main(String[] args) {
        try {
            new Banque().retirer(1500);
        } catch (SoldeInsuffisantException e) {
            System.out.println("Erreur bancaire : " + e.getMessage());
        }
    }
}
```

---
