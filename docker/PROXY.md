# 🧾 Fiche de cours — Les Proxies HTTP et Reverse Proxies avec Nginx

---

## 📌 1. Définition : c’est quoi un proxy HTTP ?

Un **proxy HTTP** est un **intermédiaire** entre un client (ex. : navigateur) et un ou plusieurs serveurs.

### 🔁 Deux types de proxy principaux :

| Type de proxy     | Rôle                                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Proxy direct**  | Le client envoie une requête au proxy, qui la transmet à Internet (ex : filtrage, sécurité)                                     |
| **Reverse proxy** | Le client pense parler à un seul serveur, mais le proxy **redirige vers un ou plusieurs serveurs internes** (API, front-end...) |

---

## 🧠 2. Pourquoi utiliser un *reverse proxy* ?

* 🔒 **Sécurité** : seuls les ports du proxy sont ouverts, les autres services sont **inaccessibles depuis l’extérieur**
* 🌐 **Simplification** : une **seule URL d’entrée** (ex. `http://localhost`), même si plusieurs services tournent derrière
* 🔁 **Redirection intelligente** : vers des services différents selon le chemin (ex. `/api/hello`)
* ⚙️ **Scalabilité** : plus facile de répartir les requêtes (load balancing)
* 🔁 **Cache / compression** : le proxy peut améliorer les performances

---

## 📦 3. Utilisation dans Docker avec Nginx

### ⚙️ 3.1 Architecture typique

```
 Navigateur
     ↓
[ http://localhost ]  ← EXPOSED:80
     ↓
   [ Proxy Nginx ]
     ↓             ↓
[ Front-end ]   [ Back-end ]
 (port 9000)     (port 5252)
```

### 🧩 Chaque service est un conteneur Docker :

| Service   | Port Interne | Exposé ? | Rôle                       |
| --------- | ------------ | -------- | -------------------------- |
| proxy     | 80           | ✅ oui    | Reçoit toutes les requêtes |
| front-end | 9000         | ❌ non    | Sert les fichiers HTML/JS  |
| back-end  | 5252         | ❌ non    | Sert les réponses API      |

---

## 📝 4. Configuration d’un reverse proxy Nginx

### Exemple de fichier `proxy.conf`

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://front-end:9000/softy-pinko-front-end/;
    }

    location /api {
        proxy_pass http://back-end:5252;
    }
}
```

### Explications :

* `listen 80` → Le serveur écoute sur le port 80
* `location /` → Toute URL sans `/api` va vers le front-end
* `location /api` → Toute URL qui commence par `/api` va vers le back-end
* `proxy_pass` → Spécifie vers **quel service rediriger la requête**

---

## 🔧 5. Configuration dans Docker Compose

### Exemple `docker-compose.yml`

```yaml
services:
  back-end:
    build: ./back-end
    expose:
      - "5252"

  front-end:
    build: ./front-end
    expose:
      - "9000"
    depends_on:
      - back-end

  proxy:
    build: ./proxy
    ports:
      - "80:80"
    depends_on:
      - front-end
      - back-end
```

💡 Remarques :

* `expose` rend les ports visibles en **interne** (entre conteneurs)
* `ports` rend le port visible **depuis l’extérieur**
* Le proxy est le **seul à être exposé**

---

## 💻 6. Code JavaScript côté front-end

Avant (sans proxy) :

```js
url: "http://localhost:5252/api/hello"
```

Après (avec proxy) :

```js
url: "/api/hello"
```

➡️ **C’est le proxy qui redirige**, plus besoin de connaître les ports internes.

---

## 🧪 7. Test de fonctionnement

* Ouvre le navigateur :

  * Front-end accessible via `http://localhost`
  * Contenu dynamique s'affiche via le proxy (`/api/hello`)
* Tu **ne peux plus accéder** directement à :

  * `http://localhost:9000`
  * `http://localhost:5252`

🛡️ **C’est voulu** : la sécurité et l’organisation passent **par un point d’entrée unique**.

---

## ✅ En résumé

| Avantage                                    | Description                                  |
| ------------------------------------------- | -------------------------------------------- |
| Un seul port exposé                         | Tout passe par le proxy                      |
| Plus besoin de connaître les ports internes | Le proxy route automatiquement               |
| Sécurité renforcée                          | Seul le proxy est visible depuis l'extérieur |
| Prêt pour le scale-up                       | Facile d'ajouter des serveurs derrière       |

---
