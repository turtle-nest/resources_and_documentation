# 🎨 Introduction au CSS

**CSS** (Cascading Style Sheets) est le langage utilisé pour **styliser** les éléments HTML. Il permet de définir les couleurs, polices, espacements, animations, tailles et positions des éléments sur une page web.

---

## 1. 🏷️ Sélecteurs, propriétés et valeurs

- **Sélecteurs** : ciblent les éléments HTML.
- **Propriétés** : indiquent ce que l’on souhaite modifier.
- **Valeurs** : précisent le style appliqué.

Exemple :
```css
p {
  color: red;
  font-size: 16px;
}
```

- Ici, `p` est le **sélecteur**,
- `color` et `font-size` sont des **propriétés**,
- `red` et `16px` sont les **valeurs**.

---

## 2. 📦 Différence entre éléments en *bloc* et *inline*

| Type        | Comportement |
|-------------|--------------|
| **Block**   | Prend toute la largeur disponible, commence sur une nouvelle ligne (ex : `<div>`, `<p>`, `<h1>`) |
| **Inline**  | N'occupe que la largeur de son contenu, reste sur la même ligne (ex : `<span>`, `<a>`) |

⚠️ On peut forcer un élément à changer de type avec `display: block;` ou `display: inline;`.

---

## 3. 🌐 Comment assurer la cohérence sur tous les navigateurs (CSS Reset)

Les navigateurs appliquent par défaut des styles différents. Pour éviter les écarts :

- **CSS Reset** : supprime tous les styles par défaut.
  ```css
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  ```

- **Normalize.css** : conserve certains styles utiles tout en harmonisant le rendu entre navigateurs.

---

## 4. 🧪 Comment définir des variables CSS

Depuis CSS3, on peut créer des **variables CSS personnalisées** :

```css
:root {
  --main-color: #3498db;
  --padding: 1rem;
}

button {
  background-color: var(--main-color);
  padding: var(--padding);
}
```

- `:root` : cible l’élément racine (`<html>`).
- `--main-color` : variable.
- `var()` : appelle la variable.

👉 Utile pour les thèmes, la cohérence et la maintenance du code.

---

## 5. 📄 Différences entre CSS *inline*, *embedded* et *external*

| Type       | Exemple | Avantages | Inconvénients |
|------------|---------|-----------|----------------|
| **Inline** | `<p style="color:red">` | Rapide pour test | Pas réutilisable, pollue le HTML |
| **Embedded** | `<style>` dans le `<head>` | Centralisé dans la page | Pas partagé entre pages |
| **External** | Fichier `.css` lié avec `<link>` | Réutilisable, maintenable | Nécessite un chargement externe |

💡 Bonnes pratiques : privilégier le CSS **externe**.

---

## 6. 🧱 Comment fonctionnent les grilles avec `float`

Avant **Flexbox** et **Grid**, on utilisait `float` :

```css
.col {
  float: left;
  width: 33.33%;
}
```

- On devait aussi *"clear"* les `float` :
```css
.row::after {
  content: "";
  display: block;
  clear: both;
}
```

Aujourd’hui, il est préférable d’utiliser **Flexbox** ou **Grid Layout**.

---

## 7. 🔤 Différence entre les *icon webfonts* et les *icônes SVG*

| Type         | Icônes Webfonts (ex : Font Awesome) | Icônes SVG |
|--------------|--------------------------------------|-------------|
| Format       | Police d’icônes                      | Vecteurs (Scalable Vector Graphics) |
| Avantages    | Facile à intégrer via classe CSS     | Personnalisable, léger, accessible |
| Inconvénients| Moins accessible, pas stylisable finement | Demande plus de code parfois |

💡 **Préférence actuelle : SVG**, surtout en inline (`<svg>...</svg>`).

---

## 8. 🎯 Différence entre *pseudo-classes* et *pseudo-éléments*

| Terme | Syntaxe | Utilité |
|-------|---------|---------|
| **Pseudo-classe** | `:hover`, `:focus`, `:nth-child()` | Cible un **état** ou une **relation** |
| **Pseudo-élément** | `::before`, `::after`, `::first-letter` | Cible une **partie d’un élément** |

Exemples :
```css
a:hover {
  color: red;
}

p::first-line {
  font-weight: bold;
}
```

---

## 9. 🌈 Comment faire des dégradés en arrière-plan

```css
div {
  background: linear-gradient(to right, #ff7e5f, #feb47b);
}
```

- `linear-gradient` : dégradé linéaire.
- `to right`, `to bottom`, `45deg` : direction.

Autre exemple :
```css
background: radial-gradient(circle, red, blue);
```

---

## 10. 🎞️ Comment animer des éléments avec CSS

### 1. Transitions simples :
```css
button {
  background-color: blue;
  transition: background-color 0.3s ease;
}
button:hover {
  background-color: red;
}
```

### 2. Animations complexes avec `@keyframes` :
```css
@keyframes slide {
  0% { transform: translateX(0); }
  100% { transform: translateX(100px); }
}

.box {
  animation: slide 1s ease-in-out infinite;
}
```

---

## 11. 🔄 Comment transformer les éléments (2D, 3D)

```css
/* 2D */
div {
  transform: rotate(45deg) scale(1.2) translateX(50px);
}

/* 3D */
div {
  transform: rotateY(180deg) perspective(500px);
  transform-style: preserve-3d;
}
```

Liste de transformations :
- `rotate()`
- `scale()`
- `translate()`
- `skew()`

---

## 12. 🧪 Que sont les *vendor prefixes* ?

Certains navigateurs nécessitent des préfixes spécifiques :

| Préfixe | Navigateur |
|---------|------------|
| `-webkit-` | Chrome, Safari |
| `-moz-`    | Firefox |
| `-ms-`     | Internet Explorer |
| `-o-`      | Opera |

Exemple :
```css
.box {
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  transform: rotate(45deg);
}
```

⚠️ Moins courant aujourd’hui grâce aux standards modernes, mais encore utile dans certains cas.

---

## ✅ Conclusion

Le CSS est un **langage puissant** pour transformer une simple structure HTML en une interface utilisateur visuellement riche et interactive. Voici un résumé des points essentiels :

- Maîtriser les **sélecteurs et propriétés** est fondamental.
- Utiliser la bonne méthode de **stylisation** (préférence pour le CSS externe).
- Connaître les outils modernes : **variables CSS, animations, transformations, dégradés**.
- Penser à l’**accessibilité**, la **cohérence inter-navigateurs** et la **sémantique visuelle**.

---
