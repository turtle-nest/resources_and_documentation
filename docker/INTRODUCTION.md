# 🌊 Introduction complète à Docker (pour macOS)

## 🔹 Qu’est-ce que Docker ?

Docker est une **plateforme open-source de conteneurisation** qui permet d’empaqueter une application avec **toutes ses dépendances** (bibliothèques, outils, fichiers de configuration) dans une unité portable appelée **conteneur**. Ce conteneur peut ensuite être exécuté de manière **cohérente** sur n’importe quelle machine, quel que soit le système hôte (Linux, Windows, macOS).

Avec Docker, **"ça marche chez moi" devient "ça marche partout"**.

---

## 🔹 Pourquoi utiliser Docker ?

Voici quelques avantages clés :

* **Portabilité** : les conteneurs s'exécutent de la même manière sur tous les environnements.
* **Légèreté** : contrairement aux machines virtuelles, les conteneurs partagent le noyau du système hôte, ce qui les rend plus rapides à démarrer et moins gourmands en ressources.
* **Isolation** : chaque conteneur est isolé, ce qui évite les conflits de versions ou de configuration.
* **Déploiement simplifié** : un seul fichier `Dockerfile` permet de recréer un environnement complet.
* **Scalabilité** : Docker permet de faire tourner plusieurs instances (conteneurs) d'une même application, facilitant ainsi la montée en charge (scale out).

---

## 🔹 Architecture de ton projet (contexte)

Tu vas créer une **infrastructure conteneurisée** composée de :

* Un **reverse proxy / load balancer** (type NGINX ou HAProxy)
* Deux **serveurs API**
* Un **serveur front-end** servant du contenu statique

Fonctionnement :

* Le **proxy** reçoit toutes les requêtes entrantes.
* Il oriente :

  * les requêtes vers le **front-end** pour du contenu statique
  * ou bien vers les **serveurs API** à l’aide de **l’algorithme de Round Robin**, pour équilibrer la charge.

📌 **Round Robin** : répartit les requêtes en boucle (1 → serveur A, 2 → serveur B, 3 → serveur A, etc.), idéal pour des charges équilibrées et un apprentissage simple de la répartition.

---

## 🔹 Docker sur macOS

Sur un Mac (surtout Apple Silicon), Docker fonctionne **via une machine virtuelle légère** (utilisant HyperKit ou Apple Virtualization Framework) car macOS ne permet pas l’exécution native de conteneurs Linux. Voici comment t’y prendre :

### ➤ Installation rapide

1. Télécharge **Docker Desktop for Mac** :
   👉 [https://docs.docker.com/desktop/install/mac-install/](https://docs.docker.com/desktop/install/mac-install/)

2. Lance l’application Docker Desktop (elle créera automatiquement une VM pour gérer tes conteneurs).

3. Dans ton terminal, vérifie l’installation :

   ```bash
   docker --version
   docker run hello-world
   ```

---

## 🔹 Commandes Docker essentielles (cheatsheet)

📄 Référence officielle : [Docker Cheatsheet PDF](https://docs.docker.com/get-started/docker_cheatsheet.pdf)

| Commande                           | Description                                     |
| ---------------------------------- | ----------------------------------------------- |
| `docker build -t nom_image .`      | Crée une image depuis un Dockerfile             |
| `docker run -d -p 80:80 nom_image` | Lance un conteneur détaché avec mappage de port |
| `docker ps`                        | Liste les conteneurs en cours d'exécution       |
| `docker stop ID`                   | Arrête un conteneur                             |
| `docker exec -it ID bash`          | Accède à un conteneur en ligne de commande      |
| `docker images`                    | Affiche les images disponibles                  |
| `docker rm ID`                     | Supprime un conteneur                           |
| `docker rmi nom_image`             | Supprime une image                              |

---

## 🔹 Dockerfile : recette de ton image

Exemple minimal :

```Dockerfile
# Utiliser une image de base officielle
FROM python:3.9-slim

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers nécessaires
COPY . .

# Installer les dépendances
RUN pip install -r requirements.txt

# Définir la commande de lancement
CMD ["python", "app.py"]
```

---

## 🔹 Docker Compose : orchestration multi-conteneurs

Pour gérer plusieurs services (API, front-end, proxy), Docker Compose est l’outil idéal.

Exemple de fichier `docker-compose.yml` :

```yaml
version: '3'

services:
  proxy:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - api1
      - api2
      - frontend

  api1:
    build: ./api
    container_name: api1

  api2:
    build: ./api
    container_name: api2

  frontend:
    build: ./frontend
```

Lancement :

```bash
docker-compose up --build
```

---

## 🔹 Bonnes pratiques

* Utilise `.dockerignore` comme `.gitignore` pour éviter d’inclure des fichiers inutiles dans ton image.
* Garde tes images légères : utilise des versions slim, nettoie les caches (`apt-get clean`, `pip cache purge`, etc.).
* Déploie par étapes avec `multi-stage builds` pour éviter les fichiers temporaires.
* Sépare bien tes services : un conteneur = un processus principal.

---

## 🔹 Pour aller plus loin

* 🐳 [Play with Docker (en ligne)](https://labs.play-with-docker.com/)
* 📦 [DockerHub : hub.docker.com](https://hub.docker.com/)
* 📚 [Documentation officielle Docker](https://docs.docker.com/)
* 🛠️ [Utiliser Portainer pour gérer tes conteneurs via une interface web](https://www.portainer.io/)

---
