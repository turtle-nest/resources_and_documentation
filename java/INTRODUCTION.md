# 🌱 Tutoriel complet pour bien débuter avec Java

## 1. Qu’est-ce que Java ?  
Java est un **langage de programmation orienté objet** développé par Sun Microsystems (racheté ensuite par Oracle). Il est réputé pour sa portabilité grâce à sa devise : *"Write once, run anywhere"*.

---

## 2. Quelles sont les plateformes de développement Java ?

Java se décline en plusieurs **plateformes de développement**, chacune adaptée à des besoins spécifiques :

- **Java SE (Standard Edition)** : Pour le développement d’applications de bureau ou console (base du langage).
- **Java EE (Enterprise Edition)** : Pour les applications web et d'entreprise (serveurs, API REST, etc.).
- **Java ME (Micro Edition)** : Pour les systèmes embarqués ou mobiles.
- **JavaFX** : Pour les interfaces graphiques modernes.
- **Jakarta EE** (successeur de Java EE) : Plateforme pour le développement d'applications serveur.

---

## 3. Quelle est la différence entre JDK et JRE ?

| Élément | Description |
|--------|-------------|
| **JDK (Java Development Kit)** | Contient tout pour développer en Java : compilateur `javac`, outils, bibliothèques, et le JRE. |
| **JRE (Java Runtime Environment)** | Permet **d'exécuter** des programmes Java déjà compilés. Il comprend la JVM et les bibliothèques de base. |

👉 **Si tu veux coder en Java, tu dois installer le JDK.**

---

## 4. Qu’est-ce que le bytecode ?

Quand tu compiles un programme Java (`.java`), il est transformé en **bytecode** (`.class`), un langage intermédiaire indépendant de la machine.

Ce bytecode est **interprété** ou **compilé à la volée** par la JVM (Java Virtual Machine) sur chaque système.

---

## 5. Quel est le rôle de la JVM (Java Virtual Machine) ?

La **JVM** exécute le bytecode Java sur n’importe quelle machine hôte.  
Elle garantit la **portabilité** (même code, différentes plateformes) et assure la **gestion de la mémoire**, le **ramassage des ordures (garbage collection)**, etc.

---

## 6. Comment compiler un fichier Java avec `javac` ?

1. Écris ton code dans un fichier `Hello.java`.
2. Compile avec la commande :
   ```bash
   javac Hello.java
   ```
   Cela génère un fichier `Hello.class`.

---

## 7. Comment exécuter un programme Java compilé ?

Une fois compilé, exécute-le avec la commande :
```bash
java Hello
```
⚠️ N’écris pas `Hello.class`, juste `Hello`.

---

## 8. Comment créer des variables et des constantes ?

```java
int age = 25;                // variable
final double PI = 3.1416;    // constante (mot-clé `final`)
```

- Les noms de variables commencent par une minuscule.
- Les constantes sont souvent en MAJUSCULES avec `_`.

---

## 9. Quels sont les types primitifs en Java ?

| Type     | Taille    | Exemple         |
|----------|-----------|------------------|
| `byte`   | 1 octet   | -128 à 127       |
| `short`  | 2 octets  | -32K à +32K      |
| `int`    | 4 octets  | -2M à +2M        |
| `long`   | 8 octets  | très grand       |
| `float`  | 4 octets  | 3.14f            |
| `double` | 8 octets  | 3.14159265       |
| `char`   | 2 octets  | 'A'              |
| `boolean`| 1 bit     | `true` ou `false`|

---

## 10. Comment lire des données depuis l'entrée standard ?

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
System.out.print("Entrez votre nom : ");
String nom = scanner.nextLine();
```

---

## 11. Comment afficher du texte en Java ?

```java
System.out.print("Bonjour ");         // sans saut de ligne
System.out.println("le monde !");     // avec saut de ligne
System.out.printf("Âge : %d ans\n", 25); // formaté
```

---

## 12. Comment fonctionnent les chaînes de caractères (String) ?

```java
String s = "Bonjour";
int len = s.length();            // longueur
char c = s.charAt(0);            // caractère à l’index 0
String upper = s.toUpperCase(); // "BONJOUR"
```

### Méthodes utiles :

| Méthode             | Fonction                                 |
|---------------------|------------------------------------------|
| `length()`          | Renvoie la longueur de la chaîne         |
| `charAt(int i)`     | Caractère à la position `i`              |
| `toUpperCase()`     | Majuscules                              |
| `toLowerCase()`     | Minuscules                              |
| `substring(a, b)`   | Extrait une sous-chaîne                  |
| `equals()`          | Comparaison de contenu                   |
| `split(String sep)` | Découpe une chaîne en plusieurs morceaux |

---

## 13. Comment manipuler les tableaux ?

### Déclaration et initialisation :
```java
int[] notes = {14, 18, 12};
String[] noms = new String[3];
```

### Parcourir un tableau :
```java
for (int i = 0; i < notes.length; i++) {
    System.out.println(notes[i]);
}

// Ou bien :
for (int note : notes) {
    System.out.println(note);
}
```

---

## 14. Comment découper une chaîne avec `split` ?

```java
String phrase = "Bonjour à tous";
String[] mots = phrase.split(" ");

for (String mot : mots) {
    System.out.println(mot);
}
```

---

## 📌 Pour bien démarrer avec Java, retiens :

- Java est **fortement typé**, chaque variable a un type défini.
- Tout se passe dans des **classes**.
- Les **objets** sont la base du langage (même si on peut faire du Java “procédural” pour apprendre).
- Les **fichiers doivent porter le nom de la classe publique principale**, exemple : `Hello.java` pour `public class Hello`.

---
