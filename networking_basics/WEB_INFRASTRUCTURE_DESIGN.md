# Web infrastructure design

## 🧱 1. Protocoles de base et adressage réseau

### 🔹 Qu’est-ce qu’un protocole ?

Un protocole est un ensemble de règles définissant **comment les données sont transmises** sur un réseau. Ils permettent l'interopérabilité entre machines.

**Exemples :**

* **IP (Internet Protocol)** : assure l’adressage et le routage des paquets.
* **TCP (Transmission Control Protocol)** : garantit la livraison fiable des données.
* **UDP (User Datagram Protocol)** : rapide mais non fiable (ex. : streaming, jeux en ligne).
* **HTTP/HTTPS** : protocoles d'échange entre client (navigateur) et serveur Web.

### 🔹 Adresse IP

Une **adresse IP** (v4 ou v6) est une **identité numérique unique** pour chaque machine connectée à un réseau.

**Types :**

* **Publique** : visible depuis Internet.
* **Privée** : utilisée en interne (ex. : 192.168.0.1).

---

## 🌐 2. Noms de domaine et DNS

### 🔹 DNS (Domain Name System)

Le DNS agit comme un **annuaire d’Internet** : il traduit les noms de domaine (ex. `google.com`) en adresses IP.

### 🔹 Types d’enregistrements DNS :

* **A Record** : associe un nom de domaine à une adresse IPv4.
* **AAAA Record** : pour les adresses IPv6.
* **CNAME** : alias d’un autre nom de domaine (ex. `www` vers `domain.com`).
* **MX** : redirection des e-mails.
* **TXT** : informations libres (souvent pour la sécurité, SPF, etc.).
* **NS** : serveurs de nom autoritaires.
* **SOA** : informations de base sur la zone DNS (version, TTL...).
* **Round Robin DNS** : distribue la charge entre plusieurs IP pour un même nom.

### 🔹 Domaines :

* **Root domain** : `example.com`.
* **Subdomain** : `www.example.com`, `api.example.com`.

---

## 🖥️ 3. Serveurs et Web servers

### 🔹 Serveur (hardware)

Un **serveur** est un ordinateur conçu pour fournir des services (Web, mail, base de données...) à d'autres machines (clients).

### 🔹 Serveur Web (software)

Un **serveur Web** gère les **requêtes HTTP/HTTPS** et sert des **fichiers HTML, CSS, JS, etc.**

**Exemples de serveurs Web :**

* **Apache**
* **Nginx**
* **Caddy**

**Fonctionnement :**

1. Le navigateur fait une requête HTTP.
2. Le serveur Web traite la requête.
3. Il renvoie la ressource demandée.

---

## ⚖️ 4. Load balancing

Un **load balancer** répartit les requêtes entre plusieurs serveurs pour :

* éviter la surcharge,
* garantir une haute disponibilité,
* améliorer la vitesse de réponse.

**Algorithmes de répartition :**

* Round Robin
* Least Connections
* IP Hash

**Exemples :**

* Nginx (avec module `upstream`)
* HAProxy
* AWS ELB
* F5 Big-IP

---

## 📊 5. Monitoring

Surveiller l’infrastructure est crucial pour :

* anticiper les pannes,
* identifier les goulots d’étranglement,
* améliorer les performances.

### 🔹 Deux niveaux de monitoring :

* **Application monitoring** : suivi du code, erreurs HTTP, temps de réponse.
* **Server monitoring** : CPU, mémoire, disque, réseau...

### 🔹 Outils populaires :

* **New Relic** : monitoring applicatif (temps de chargement, erreurs).
* **DataDog** : monitoring complet avec dashboards personnalisés.
* **Uptime Robot** : vérifie si un site est en ligne.
* **Nagios** : open source, plus classique.
* **WaveFront** : hautement technique, utilisé chez les géants du Web.

---

## ✅ En résumé

| Composant         | Rôle                                             |
| ----------------- | ------------------------------------------------ |
| **IP, TCP, UDP**  | Acheminer et structurer les données              |
| **DNS**           | Traduire les noms en adresses IP                 |
| **Serveur Web**   | Répondre aux requêtes HTTP                       |
| **Load balancer** | Répartir la charge entre serveurs                |
| **Monitoring**    | Surveiller la santé et la performance du système |

---

## 🧑‍💻 Pourquoi c’est essentiel pour toi, développeur ?

Comprendre l’infrastructure Web permet de :

* concevoir des applications **scalables** et **fiables**,
* diagnostiquer des erreurs réseau ou serveur,
* **collaborer efficacement avec les DevOps** et SRE,
* anticiper les choix techniques dès la conception (ex. : monolithes vs microservices).
