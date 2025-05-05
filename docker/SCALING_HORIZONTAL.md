# 🧾 Cours — Scaling Horizontal avec Docker, Nginx et Docker Compose

---

## 📍 Objectif du cours

Tu vas apprendre à **doubler (ou multiplier) un service back-end** pour améliorer :

* Les **performances**
* La **disponibilité**
* La **scalabilité**

Ce processus s'appelle le **scaling horizontal** : on **ajoute des copies identiques** du même service, au lieu d’augmenter la puissance d’un seul serveur.

---

## 🧠 Pourquoi faire du scaling horizontal ?

Imagine un serveur de restaurant :

* Si un serveur est débordé → attente
* Si tu **ajoutes d’autres serveurs**, les clients sont servis plus vite ✅

Sur le web, c’est pareil :

* Si ton **API Flask** reçoit trop de requêtes, elle ralentit
* En ajoutant **plusieurs copies**, tu répartis les requêtes entre elles

> 🎯 C’est le rôle d’un **load balancer** comme Nginx, qui distribue équitablement les requêtes entre les API disponibles.

---

## 🔁 Le rôle du Reverse Proxy dans le scaling

Tu as déjà mis en place un proxy Nginx dans les exercices précédents. On va maintenant :

* Lancer **plusieurs conteneurs `back-end`** identiques
* Laisser **Nginx les contacter à tour de rôle (Round Robin)**

Tu ne modifies **rien dans le code** de l’API ni dans Nginx. Juste la **commande Docker** change.

---

## ⚙️ Étapes techniques du scaling horizontal

---

### ✅ 1. Copier ton projet existant

Depuis `task5`, crée une copie :

```bash
cp -r task5 task6
cd task6
```

---

### ✅ 2. Créer un fichier avec la commande de scaling

L’exercice demande de fournir un fichier contenant la commande utilisée.

```bash
echo "docker-compose up --scale back-end=2" > 2-api-servers.txt
```

Vérifie que le fichier se termine bien par une **nouvelle ligne** (très important pour la validation automatique) :

```bash
cat -A 2-api-servers.txt  # doit se terminer par un "$"
```

---

### ✅ 3. Lancer plusieurs instances de l’API

Utilise la commande suivante pour construire les images et lancer 2 serveurs Flask :

```bash
docker-compose up --scale back-end=2 --build
```

Cela créera automatiquement :

* `task6-back-end-1`
* `task6-back-end-2`

🎉 Les deux conteneurs répondent à `http://back-end:5252` (Docker les résout automatiquement).

---

## 🔁 Round Robin en action

Chaque requête `/api/hello` est redirigée par le proxy **alternativement** vers un des deux serveurs `back-end`.

Tu peux observer ça dans les logs des conteneurs :

```bash
task6-back-end-1 | "GET /api/hello HTTP/1.0"
task6-back-end-2 | "GET /api/hello HTTP/1.0"
```

En rechargeant ta page web plusieurs fois, tu verras les requêtes **alterner** entre les serveurs.

---

## ✅ Tu veux aller plus loin ?

Tu peux tester avec **plus de serveurs** :

```bash
docker-compose up --scale back-end=5 --build
```

Tu verras alors :

```
task6-back-end-1 | GET /api/hello
task6-back-end-2 | GET /api/hello
task6-back-end-3 | GET /api/hello
task6-back-end-4 | GET /api/hello
task6-back-end-5 | GET /api/hello
```

---

## 🧾 Résumé de la fiche de cours

| Concept                         | Explication                                             |
| ------------------------------- | ------------------------------------------------------- |
| **Scaling horizontal**          | Ajouter plusieurs instances identiques d’un service     |
| **Load balancer (Nginx)**       | Répartit les requêtes entre les instances               |
| **Round Robin**                 | Chaque instance reçoit les requêtes à tour de rôle      |
| **Docker Compose `--scale`**    | Permet de lancer plusieurs conteneurs d’un même service |
| **Fichier `2-api-servers.txt`** | Contient la commande exacte pour lancer le scaling      |

---

## 🛠 Commandes clés à retenir

```bash
# Créer le fichier demandé :
echo "docker-compose up --scale back-end=2" > 2-api-servers.txt

# Lancer avec 2 conteneurs back-end
docker-compose up --scale back-end=2 --build

# Lancer avec 5 conteneurs back-end
docker-compose up --scale back-end=5 --build
```

---
