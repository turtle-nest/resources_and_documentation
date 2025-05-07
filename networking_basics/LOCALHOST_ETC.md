# 🌐 Tutoriel Réseau : localhost, 0.0.0.0, /etc/hosts et Netcat

---

## 1. 🔁 Qu’est-ce que **localhost / 127.0.0.1** ?

### 📌 Définition :

* **`localhost`** est un nom d’hôte réservé qui fait référence **à la machine elle-même**.
* Il pointe vers l’adresse IP **`127.0.0.1`**, aussi appelée **boucle locale** ou **loopback**.

### 📥 À quoi ça sert ?

* Tester un serveur localement sans connexion Internet
* Développer ou déboguer une application en réseau
* Empêcher certaines communications de sortir de la machine

### 📘 Exemple :

```bash
ping 127.0.0.1
```

Tu pingues **toi-même**. Très utile pour tester si la **pile réseau** fonctionne.

---

## 2. 🌐 Qu’est-ce que **0.0.0.0** ?

### 📌 Définition :

* `0.0.0.0` signifie **“toutes les adresses IP disponibles”** sur la machine.
* Utilisée par un serveur pour **écouter sur toutes les interfaces réseau**.

### 📘 Exemple :

Un serveur qui écoute sur `0.0.0.0:80` acceptera des connexions :

* depuis `localhost`
* depuis l’IP privée (ex: 192.168.1.x)
* depuis l’IP publique (si applicable)

---

## 3. 🗂️ Qu’est-ce que **/etc/hosts** ?

### 📌 Définition :

C’est un fichier système qui associe des **noms d’hôtes à des adresses IP**.

### 📄 Contenu typique :

```text
127.0.0.1   localhost
::1         localhost
192.168.1.50 dev.local
```

### 🧠 À quoi ça sert ?

* Résoudre un nom en IP **sans requête DNS**
* Bloquer un domaine (en le pointant vers `127.0.0.1`)
* Créer des alias locaux pour des machines

### ✏️ Modifier ce fichier :

```bash
sudo nano /etc/hosts
```

---

## 4. 📡 Comment afficher les interfaces réseau actives ?

### 🔧 Avec `ifconfig` (ancien outil, encore courant) :

```bash
ifconfig
```

Affiche toutes les interfaces disponibles et leur configuration.

🔎 Pour ne voir que celles qui sont **actives** :

```bash
ifconfig | grep flags
```

### 🆕 Avec `ip` (remplaçant moderne) :

```bash
ip a
```

---

## 5. 🛠️ Netcat (`nc`) : couteau suisse du réseau

### 📌 Qu’est-ce que `nc` ?

C’est un utilitaire en ligne de commande pour :

* écouter ou établir des connexions TCP/UDP
* faire du débogage réseau
* envoyer/recevoir des fichiers

### 📘 Exemples pratiques :

#### 🔈 Écouter sur un port :

```bash
nc -l 1234
```

#### 🎤 Envoyer un message vers ce port depuis une autre machine :

```bash
echo "Bonjour" | nc 192.168.1.X 1234
```

#### 📂 Transférer un fichier :

Sur le **récepteur** :

```bash
nc -l 1234 > fichier.txt
```

Sur l’**expéditeur** :

```bash
nc 192.168.1.X 1234 < fichier.txt
```

---

## 6. 🧰 Aide rapide sur les commandes avec `man` ou `--help`

### 📖 Afficher le manuel :

```bash
man ifconfig
man nc
man telnet
man cut
```

### 📌 Aide rapide :

```bash
ifconfig --help
nc --help
```

---

## 7. 🧪 Bonus : couper et extraire des champs avec `cut`

### 📘 Exemple :

Extraire le premier champ d’un fichier CSV :

```bash
cut -d ',' -f1 fichier.csv
```

* `-d` : définit le **délimiteur**
* `-f` : spécifie le ou les champs à extraire

---

## 🧠 Résumé

| Élément       | Fonction                                            |
| ------------- | --------------------------------------------------- |
| `127.0.0.1`   | Adresse IP locale (localhost)                       |
| `0.0.0.0`     | Toutes les interfaces réseau disponibles            |
| `/etc/hosts`  | Associe des noms à des IP sans DNS                  |
| `ifconfig`    | Affiche les interfaces réseau                       |
| `nc` (netcat) | Outil pour tester, écouter ou envoyer en TCP/UDP    |
| `cut`         | Permet d’extraire des colonnes ou champs d’un texte |

---
