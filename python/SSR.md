# Le Server-Side Rendering

## 🌐 1. Comprendre le **Server-Side Rendering (SSR)**

### 🔹 Définition

Le **Server-Side Rendering (SSR)** est une technique où le **contenu HTML est généré par le serveur** avant d’être envoyé au navigateur du client. C’est le serveur qui assemble les données et les templates HTML pour former une page complète.

### 🔹 Comparaison avec le **Client-Side Rendering (CSR)**

| Aspect | SSR | CSR |
|--------|-----|-----|
| Lieu de rendu | Serveur | Navigateur |
| Temps de rendu initial | Rapide (HTML complet) | Plus lent (JS charge la page) |
| SEO | Très bon (HTML déjà prêt) | Moins bon si mal configuré |
| Dynamisme | Moins interactif sans JS | Très interactif |
| Exemple techno | Flask + Jinja, Django | React, Vue, Angular |

---

## ✅ 2. Avantages du SSR en développement web

- ✅ **Meilleur SEO** : les moteurs de recherche lisent directement le contenu HTML.
- ✅ **Chargement initial rapide** : la page s’affiche dès réception.
- ✅ **Simplicité** : moins de logique côté client.
- ✅ **Sécurité** : moins d'exposition de la logique métier.

SSR est idéal pour les sites **éditoriaux, blogs, e-commerces, tableaux de bord d'administration**, etc.

---

## 🧪 3. Implémenter le SSR avec Flask

### 🔸 Installation de Flask

```bash
pip install flask
```

### 🔸 Exemple de base

**app.py**
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html", name="Alice")

if __name__ == "__main__":
    app.run(debug=True)
```

**templates/index.html**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Bienvenue</title>
</head>
<body>
  <h1>Bonjour {{ name }} !</h1>
</body>
</html>
```

📌 Ici, **Flask génère dynamiquement** le HTML côté serveur grâce au moteur de templates **Jinja**.

---

## 🧩 4. Utiliser le moteur de template **Jinja2**

### 🔸 Syntaxe de base

| Fonction | Syntaxe |
|----------|---------|
| Variable | `{{ variable }}` |
| Condition | `{% if condition %}` |
| Boucle | `{% for item in liste %}` |
| Inclusions | `{% include 'fichier.html' %}` |

### 🔸 Exemple

```html
<ul>
  {% for user in users %}
    <li>{{ user }}</li>
  {% endfor %}
</ul>
```

---

## 📁 5. Lire et afficher des données depuis JSON, CSV, SQLite

### a. Lire un fichier JSON

**data.json**
```json
[
  { "name": "Alice" },
  { "name": "Bob" }
]
```

**app.py**
```python
import json

@app.route("/json")
def json_data():
    with open("data.json") as f:
        users = json.load(f)
    return render_template("json.html", users=users)
```

---

### b. Lire un fichier CSV

```python
import csv

@app.route("/csv")
def csv_data():
    with open("data.csv") as f:
        reader = csv.DictReader(f)
        users = list(reader)
    return render_template("csv.html", users=users)
```

---

### c. Lire une base SQLite

```python
import sqlite3

@app.route("/db")
def db_data():
    conn = sqlite3.connect("mydb.db")
    cursor = conn.cursor()
    cursor.execute("SELECT name FROM users")
    users = cursor.fetchall()
    conn.close()
    return render_template("db.html", users=users)
```

---

## 🔄 6. Gérer le contenu dynamique et les entrées utilisateur

### 🔸 Formulaire HTML

**form.html**
```html
<form method="POST" action="/greet">
  <input type="text" name="username">
  <button type="submit">Envoyer</button>
</form>
```

### 🔸 Traitement côté Flask

```python
from flask import request

@app.route("/greet", methods=["POST"])
def greet():
    name = request.form.get("username")
    return render_template("greet.html", name=name)
```

---

## 🔐 Bonus : sécuriser les données

- Toujours **valider et nettoyer les données** envoyées par l'utilisateur.
- Utiliser `escape()` pour éviter les injections HTML si nécessaire.
- Toujours préférer les **paramètres SQL sécurisés** avec SQLite ou SQLAlchemy.

---

## ✅ Conclusion

Le Server-Side Rendering avec Flask en Python est une approche **puissante, rapide et simple** pour créer des applications web dynamiques. En résumé :

- 📌 Le SSR génère les pages côté serveur, parfait pour le SEO et la rapidité initiale.
- 📌 Flask + Jinja permet de générer du HTML dynamique proprement.
- 📌 On peut intégrer facilement des données de différentes sources (JSON, CSV, BDD).
- 📌 La gestion des formulaires se fait facilement via `request.form`.

---
