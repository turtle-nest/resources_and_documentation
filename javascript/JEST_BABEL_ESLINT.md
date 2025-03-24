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

Voici **étape par étape** comment configurer **Jest** pour tester ton code, et **ESLint** pour analyser ton style de code (avec les règles demandées dans ton projet Holberton).

---

## 🧪 1. **Configurer Jest pour tester ton code**

### 📦 Installation (dans le dossier du projet)
Si ce n’est pas déjà fait :
```bash
npm install --save-dev jest babel-jest @babel/core @babel/preset-env
```

---

### ⚙️ Crée le fichier `babel.config.js` à la racine du dossier (`ES6_basic`) :

```js
module.exports = {
  presets: [['@babel/preset-env', { targets: { node: 'current' } }]],
};
```

---

### ✅ Test d’un fichier — crée `0-constants.test.js`

```js
import { taskFirst, taskNext } from './0-constants.js';

test('taskFirst returns expected value', () => {
  expect(taskFirst()).toBe('I prefer const when I can.');
});

test('taskNext returns expected value', () => {
  expect(taskNext()).toBe('But sometimes let is okay');
});
```

---

### 🧪 Lance tes tests avec :

```bash
npm test
```

---

## 🧹 2. **Configurer ESLint pour analyser ton code**

### 📦 Installation :
```bash
npm install --save-dev eslint
```

---

### ⚙️ Crée le fichier `.eslintrc.js` (dans le même dossier que `0-constants.js`) :

```js
module.exports = {
  env: {
    browser: false,
    es2021: true,
    node: true,
    jest: true,
  },
  extends: ['eslint:recommended'],
  parserOptions: {
    ecmaVersion: 12,
    sourceType: 'module',
  },
  rules: {
    // Tu peux ajouter ici les règles spécifiques à Holberton si elles sont données
  },
};
```

---

### 📂 Si tu veux analyser ton code :

```bash
npx eslint 0-constants.js
```

---

## 📄 Exemple complet de `package.json`

```json
{
  "type": "module",
  "scripts": {
    "dev": "node 0-main.js",
    "test": "jest",
    "lint": "eslint ."
  },
  "devDependencies": {
    "@babel/core": "^7.26.10",
    "@babel/preset-env": "^7.26.9",
    "babel-jest": "^29.7.0",
    "eslint": "^9.23.0",
    "jest": "^29.7.0"
  }
}
```

- `npm test` → pour exécuter tes tests
- `npm run lint` → pour analyser tous les fichiers `.js` du dossier

---

