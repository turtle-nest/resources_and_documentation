# 🧠 Cours complet : Manipulation du DOM en JavaScript

---

## 🧱 1. Qu’est-ce que le DOM ?

Le **DOM (Document Object Model)** est une représentation **structurée en arbre** d’un document HTML ou XML. Chaque élément HTML devient un **nœud** que l'on peut manipuler avec JavaScript.

Grâce au DOM, on peut :
- Sélectionner des éléments,
- Modifier leur contenu ou style,
- Réagir aux événements,
- Ajouter, supprimer ou déplacer des éléments dynamiquement.

---

## 🔍 2. Comment sélectionner des éléments HTML en JavaScript ?

### 🔹 Méthodes de sélection modernes :

| Méthode                         | Sélectionne...                      |
|----------------------------------|-------------------------------------|
| `document.querySelector()`      | Le **premier** élément correspondant à un **sélecteur CSS** |
| `document.querySelectorAll()`   | **Tous** les éléments correspondants à un **sélecteur CSS** |

```js
const titre = document.querySelector("h1");
const tousLesParagraphes = document.querySelectorAll("p");
```

### 🔹 Méthodes classiques :

| Méthode                         | Type de sélecteur   |
|----------------------------------|---------------------|
| `getElementById("id")`          | Un **ID unique**    |
| `getElementsByClassName("nom")` | Une **classe**      |
| `getElementsByTagName("tag")`   | Un **nom de balise**|

```js
const monElement = document.getElementById("titre");
const paragraphes = document.getElementsByTagName("p");
```

---

## 🆔 3. Différences entre ID, classe et nom de balise

| Sélecteur | Caractéristiques | Utilisation |
|-----------|------------------|-------------|
| ID (`#id`) | Unique par page | Pour un seul élément |
| Classe (`.classe`) | Réutilisable sur plusieurs éléments | Pour styliser ou cibler des groupes |
| Balise (`div`, `p`) | Cible tous les éléments de ce type | Moins spécifique, plus global |

---

## 🎨 4. Comment modifier le style d’un élément HTML ?

Accès via la propriété `.style` :

```js
const titre = document.querySelector("h1");
titre.style.color = "blue";
titre.style.fontSize = "2em";
```

💡 Pour modifier plusieurs styles en une fois : créer une classe CSS et l’ajouter avec `.classList.add("ma-classe")`.

```js
titre.classList.add("important");
```

---

## ✏️ 5. Comment obtenir et modifier le contenu d’un élément ?

### 🔹 Lire le contenu

- `textContent` : texte brut (sans HTML)
- `innerText` : texte visible (moins fiable)
- `innerHTML` : contenu HTML

```js
const paragraphe = document.querySelector("p");
console.log(paragraphe.textContent);
```

### 🔹 Modifier le contenu

```js
paragraphe.textContent = "Texte mis à jour.";
paragraphe.innerHTML = "<strong>Texte en gras</strong>";
```

---

## 🔄 6. Comment modifier la structure du DOM ?

### 🔹 Créer un élément :

```js
const nouveauParagraphe = document.createElement("p");
nouveauParagraphe.textContent = "Je suis nouveau !";
```

### 🔹 Ajouter au DOM :

```js
document.body.appendChild(nouveauParagraphe);
```

### 🔹 Supprimer un élément :

```js
const element = document.querySelector(".a-supprimer");
element.remove();
```

### 🔹 Remplacer un élément :

```js
const ancien = document.querySelector("#ancien");
const nouveau = document.createElement("div");
nouveau.textContent = "Remplacement";
ancien.replaceWith(nouveau);
```

---

## 🌐 7. Comment faire une requête avec `XMLHttpRequest` ?

**Ancienne méthode**, encore parfois utilisée.

```js
const xhr = new XMLHttpRequest();
xhr.open("GET", "https://api.example.com/data");
xhr.onload = function () {
  if (xhr.status === 200) {
    console.log(JSON.parse(xhr.responseText));
  }
};
xhr.send();
```

---

## 🧪 8. Comment faire une requête avec `fetch()` (moderne)

**Fetch API** est plus simple et moderne :

```js
fetch("https://api.example.com/data")
  .then(response => {
    if (!response.ok) throw new Error("Erreur");
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error("Erreur :", error));
```

Avec `async/await` :

```js
async function getData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
```

---

## 🎧 9. Comment écouter les événements DOM ?

### 🔹 Méthode : `addEventListener()`

```js
const bouton = document.querySelector("button");
bouton.addEventListener("click", () => {
  alert("Clique détecté !");
});
```

---

## 🧑‍💻 10. Écouter les événements utilisateur courants

| Événement        | Déclenché quand…                  |
|------------------|-----------------------------------|
| `click`          | L'utilisateur clique              |
| `input`          | L'utilisateur tape dans un champ  |
| `submit`         | Soumission d’un formulaire        |
| `change`         | Changement de valeur (checkbox...)|
| `keydown`        | Touche enfoncée                   |
| `mousemove`      | Mouvement de la souris            |

Exemple :

```js
const input = document.querySelector("input");
input.addEventListener("input", (e) => {
  console.log("Valeur :", e.target.value);
});
```

---

## 📚 Bonus : manipuler les classes CSS dynamiquement

```js
element.classList.add("visible");
element.classList.remove("cache");
element.classList.toggle("actif");
```

---

## ✅ Résumé du cours

| Concept                        | Description |
|-------------------------------|-------------|
| DOM                           | Représentation objet d'une page HTML |
| Sélection                     | `querySelector`, `getElementById`, etc. |
| Modification de contenu/style | `textContent`, `innerHTML`, `.style` |
| Ajout/suppression éléments    | `createElement`, `appendChild`, `.remove()` |
| Requêtes HTTP                 | `XMLHttpRequest`, `fetch`, `async/await` |
| Écoute d'événements           | `addEventListener()` |
| Gestion des classes           | `.classList.add/remove/toggle()` |

---

## 💡 Exercices suggérés

- Crée une todo-list dynamique avec `addEventListener`, `createElement`, et `remove()`.
- Fais un petit client météo qui utilise `fetch()` pour afficher la météo en fonction d’un champ texte.
- Ajoute un bouton qui change dynamiquement le thème (dark/light) via les classes CSS.

---
