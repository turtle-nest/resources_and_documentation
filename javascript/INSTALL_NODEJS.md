# Install NodeJS 20.x.x

Voici la bonne méthode pour installer **Node.js 20.x** sur un **Mac Apple Silicon (M1/M2/M3)** :

---

### ✅ **Méthode recommandée avec Homebrew**

#### 1. Installe Homebrew (si ce n’est pas encore fait) :
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Puis ajoute ceci à ton fichier `.zprofile` ou `.zshrc` (si tu utilises Zsh) :
```bash
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Recharge le terminal ou fais :
```bash
source ~/.zprofile
```

#### 2. Installe Node.js version 20
```bash
brew install node@20
```

#### 3. Lier Node.js 20 (si ce n’est pas la version par défaut)
```bash
brew link --force --overwrite node@20
```

---

### ✅ **Vérifie l’installation**
```bash
node -v    # Doit afficher : v20.x.x
npm -v     # Affiche la version de npm associée
```

---

### ❗️Alternative : via le site officiel

Tu peux aussi aller ici :
👉 [https://nodejs.org/en/download](https://nodejs.org/en/download)

Télécharge le **macOS Installer** (pkg) pour la **version 20.x LTS** et installe-le comme une application classique.

---

Souhaites-tu que je t’aide à configurer un environnement spécifique (comme React, Express, etc.) après l’installation ?