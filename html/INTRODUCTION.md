# 🌐 Introduction au HTML

**HTML** (HyperText Markup Language) est le langage de balisage utilisé pour structurer le contenu d’une page web. Il permet de décrire les différents éléments qui composent une page : titres, paragraphes, liens, images, vidéos, etc.

---

## 1. 🧭 Quelles bonnes pratiques faut-il suivre en HTML ?

Voici quelques **guidelines essentielles** à respecter :

- ✅ Respecter la **sémantique** : utiliser les balises appropriées pour le type de contenu (ex. `<article>` pour un article, `<nav>` pour une navigation).
- ✅ Toujours utiliser une **structure claire et hiérarchique** (ex : titres `<h1>` à `<h6>`, sections, etc.).
- ✅ Fermer toutes les balises, même celles qui sont auto-fermantes (`<img />`, `<br />`).
- ✅ Indenter proprement le code HTML (2 ou 4 espaces).
- ✅ Ajouter des attributs `alt` aux images pour l’**accessibilité**.
- ✅ Ne pas surcharger avec trop de `<div>` inutiles (syndrome du “divitis”).
- ✅ Valider le code HTML avec [le validateur du W3C](https://validator.w3.org/).

---

## 2. 🧱 Comment créer le squelette d’une page HTML5 ?

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Titre de la page</title>
</head>
<body>
  <header>
    <h1>Bienvenue</h1>
  </header>

  <main>
    <p>Contenu principal</p>
  </main>

  <footer>
    <p>© 2025</p>
  </footer>
</body>
</html>
```

Ce squelette inclut :
- la déclaration `<!DOCTYPE html>` (pour le HTML5),
- la balise `<html>` avec l’attribut `lang`,
- les sections standard : `<head>`, `<body>`.

---

## 3. 🧩 Comment utiliser les balises sémantiques pour structurer une page web ?

Les balises sémantiques donnent un **sens** au contenu. En voici quelques-unes essentielles :

| Balise       | Rôle |
|--------------|------|
| `<header>`   | En-tête de page ou de section |
| `<main>`     | Contenu principal de la page |
| `<footer>`   | Pied de page ou de section |
| `<article>`  | Contenu autonome (ex : un article de blog) |
| `<nav>`      | Liens de navigation |
| `<section>`  | Regroupe un thème ou une fonctionnalité |
| `<aside>`    | Informations complémentaires (ex : pub, sidebar) |

Utiliser ces balises améliore l’**accessibilité**, le **SEO** et la **maintenabilité** du code.

---

## 4. 🧱 Quand utiliser `<div>` vs `<span>` ?

| Élément | Usage | Type |
|---------|-------|------|
| `<div>` | Conteneur de **bloc** (structure, mise en page) | Bloc |
| `<span>`| Conteneur **inline** (texte, mots à styliser) | Inline |

Exemple :
```html
<div class="carte">
  <h2>Nom</h2>
  <p><span class="important">Attention :</span> ceci est important.</p>
</div>
```

---

## 5. 🧠 Quelle est la valeur sémantique de certaines balises ?

| Balise      | Signification sémantique |
|-------------|--------------------------|
| `<header>`  | Introduction d'une page ou section |
| `<main>`    | Zone principale, unique par page |
| `<footer>`  | Informations de bas de page |
| `<article>` | Contenu indépendant, exportable |
| `<nav>`     | Ensemble de liens de navigation |
| `<section>` | Partie cohérente du contenu |
| `<aside>`   | Complément (notes, pub, liens, etc.) |

---

## 6. 🧢 Comment utiliser les titres et pourquoi respecter leur hiérarchie ?

Les balises de titre (`<h1>` à `<h6>`) doivent suivre une hiérarchie logique :

- `<h1>` : titre principal de la page (1 seul !)
- `<h2>` : sous-titres de sections
- `<h3>` : sous-sous-titres, etc.

Exemple :
```html
<h1>Mon Portfolio</h1>
  <h2>Projets</h2>
    <h3>Projet 1</h3>
```

**Pourquoi ?**  
Cela facilite :
- l’accessibilité (ex. lecteurs d’écran),
- l’indexation SEO,
- la compréhension du contenu par l’utilisateur.

---

## 7. 🔢 Comment faire des listes en HTML ?

Trois types principaux :

- **Liste non ordonnée** (`<ul>` + `<li>`) :
  ```html
  <ul>
    <li>Pomme</li>
    <li>Banane</li>
  </ul>
  ```

- **Liste ordonnée** (`<ol>` + `<li>`) :
  ```html
  <ol>
    <li>Étape 1</li>
    <li>Étape 2</li>
  </ol>
  ```

- **Liste de définitions** (`<dl>`, `<dt>`, `<dd>`) :
  ```html
  <dl>
    <dt>HTML</dt>
    <dd>Langage de balisage</dd>
  </dl>
  ```

---

## 8. 🖼️ Quelles différences entre SVG, GIF, PNG et JPG ?

| Format | Utilisation | Avantages | Inconvénients |
|--------|-------------|-----------|---------------|
| SVG    | Icônes, logos, graphiques vectoriels | Infini en taille, modifiable par CSS/JS | Pas pour les photos |
| GIF    | Animations simples | Large support, animé | Qualité basse, 256 couleurs |
| PNG    | Images avec transparence | Sans perte, fond transparent | Poids plus élevé |
| JPG    | Photos, visuels complexes | Compression élevée, léger | Perte de qualité |

---

## 9. 📊 Comment structurer des données dans un tableau ?

```html
<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Âge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
```

**Balises importantes :**
- `<table>` : le tableau,
- `<thead>`, `<tbody>`, `<tfoot>` : sections du tableau,
- `<tr>` : ligne,
- `<td>` : cellule,
- `<th>` : cellule d’en-tête.

---

## 10. 🎥 Comment intégrer une vidéo dans une page ?

```html
<video controls width="640" height="360">
  <source src="video.mp4" type="video/mp4">
  Votre navigateur ne supporte pas la vidéo HTML5.
</video>
```

Options :
- `autoplay`, `loop`, `muted`, `poster`, `controls`.

---

## 11. 🔊 Comment intégrer un fichier audio ?

```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  Votre navigateur ne supporte pas l’audio HTML5.
</audio>
```

---

## 12. 🔗 Comment intégrer du contenu externe ?

Utilise la balise `<iframe>` :

```html
<iframe src="https://www.youtube.com/embed/xyz" width="560" height="315" allowfullscreen></iframe>
```

Autres exemples :
- Google Maps
- Slides, documents, tweets, etc.

---

## 13. 🏗️ Comment bien structurer une page HTML ?

Structure recommandée :

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Ma page</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li><a href="#">Accueil</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <section>
        <h2>Présentation</h2>
        <p>Texte ici...</p>
      </section>

      <article>
        <h2>Dernier article</h2>
        <p>Contenu d’un article de blog</p>
      </article>

      <aside>
        <p>Newsletter, pub, etc.</p>
      </aside>
    </main>

    <footer>
      <p>© 2025 - Mon Site</p>
    </footer>
  </body>
</html>
```

---

## ✅ Conclusion

HTML est la **base incontournable** de toute page web. Maîtriser sa structure, ses balises sémantiques et les bonnes pratiques permet de créer des sites lisibles, accessibles, bien organisés et efficaces.
