# Install Jest, Babel, and ESLint

Voici une **fiche claire et structurée** pour installer **Jest**, **Babel** et **ESLint** dans un projet Node.js sur ton Mac :

---

## 🛠️ Fiche d'installation : Jest, Babel et ESLint

### 📁 Pré-requis :
- Node.js 20.x installé ✅
- Un projet Node.js initialisé (`npm init -y`)

---

### 1. 📦 **Installer Jest**
Dans le répertoire du projet :
```bash
npm install --save-dev jest
```

#### ➕ Ajouter un script dans `package.json`
```json
"scripts": {
  "test": "jest"
}
```

---

### 2. 🔧 **Installer Babel pour Jest**
Toujours dans le même dossier :
```bash
npm install --save-dev babel-jest @babel/core @babel/preset-env
```

#### ➕ Créer un fichier de config Babel : `.babelrc`
```json
{
  "presets": ["@babel/preset-env"]
}
```

---

### 3. 🧹 **Installer ESLint**
```bash
npm install --save-dev eslint
```

#### ➕ Initialiser la configuration ESLint :
```bash
npx eslint --init
```
Suivre les instructions dans le terminal :
- Choisir la syntaxe (JavaScript, module, etc.)
- Définir l’environnement (Node.js)
- Style de code (standard, Airbnb, etc.)
- Format du fichier de configuration (`.eslintrc.json` ou autre)

---

### ✅ Vérification
- Lancer les tests :  
  ```bash
  npm test
  ```
- Lancer ESLint sur un fichier :
  ```bash
  npx eslint yourFile.js
  ```

---
