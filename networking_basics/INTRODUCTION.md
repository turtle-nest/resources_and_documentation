# 🌐 Introduction aux Réseaux Informatiques

Les réseaux informatiques permettent à des machines de communiquer entre elles afin d’échanger des données, des fichiers ou des services. Cela va du réseau local de la maison jusqu’à l’Internet mondial. Pour comprendre cette communication, on utilise souvent un modèle de référence : **le modèle OSI**.

---

## 1. 📦 Le modèle OSI

### Qu’est-ce que le modèle OSI ?

Le modèle **OSI (Open Systems Interconnection)** est un **modèle de référence** en 7 couches qui décrit **comment les données circulent dans un réseau**, de l’utilisateur jusqu’au matériel.

### Combien de couches ?

Il contient **7 couches**, chacune ayant un rôle spécifique dans la transmission des données.

### Organisation du modèle OSI (de haut en bas) :

| N° | Couche             | Rôle principal                                    |
| -- | ------------------ | ------------------------------------------------- |
| 7  | Application        | Interface avec les applications (HTTP, FTP, etc.) |
| 6  | Présentation       | Encodage, chiffrement, compression                |
| 5  | Session            | Gestion des connexions et synchronisation         |
| 4  | Transport          | Transmission fiable (TCP) ou rapide (UDP)         |
| 3  | Réseau             | Adressage IP et routage des paquets               |
| 2  | Liaison de données | Adresse MAC, détection d’erreurs                  |
| 1  | Physique           | Câbles, ondes, bits transmis physiquement         |

---

## 2. 🏠 Qu’est-ce qu’un LAN (Local Area Network) ?

### Définition

Un **LAN** est un **réseau local**, typiquement à l’intérieur d’un **bâtiment ou d’un logement**.

### Usage typique

* Partage de fichiers, imprimantes, Internet
* Réseaux domestiques, d’entreprise, ou scolaires

### Taille géographique

* **Petite** : quelques mètres à quelques centaines de mètres

---

## 3. 🛰️ Qu’est-ce qu’un WAN (Wide Area Network) ?

### Définition

Un **WAN** est un **réseau étendu**, qui relie plusieurs LANs entre eux à grande distance.

### Usage typique

* Interconnexion entre agences d’une entreprise
* Internet est le plus grand WAN

### Taille géographique

* **Très grande** : ville, pays, voire monde entier

---

## 4. 🌍 Qu’est-ce qu’Internet ?

**Internet** est l’**interconnexion mondiale** de réseaux (LAN, MAN, WAN) utilisant **le protocole IP**. C’est une infrastructure décentralisée qui permet l’échange de données à l’échelle planétaire.

---

## 5. 🌐 Qu’est-ce qu’une adresse IP ?

### Définition

Une **adresse IP (Internet Protocol)** est un **identifiant unique** pour chaque appareil sur un réseau. Elle permet de **localiser et communiquer** avec un hôte.

### Les 2 types d’adresse IP

1. **Publique** : visible sur Internet, attribuée par un fournisseur d’accès
2. **Privée** : utilisée dans les réseaux locaux (ex : 192.168.x.x)

---

## 6. 🖥️ Qu’est-ce que localhost ?

`localhost` fait référence à **l’adresse IP 127.0.0.1**. C’est un alias pour parler de **la machine elle-même**, souvent utilisée pour tester des services localement.

---

## 7. 🧩 Qu’est-ce qu’un sous-réseau (subnet) ?

Un **sous-réseau** est une division logique d’un réseau IP. Il permet de **segmenter un réseau** pour une meilleure sécurité et une meilleure gestion.

Exemple : 192.168.1.0/24 désigne un sous-réseau de 256 adresses.

---

## 8. 🧮 Pourquoi IPv6 a été créé ?

IPv4 (avec ses **4 milliards d’adresses**) devient insuffisant. IPv6 a été conçu pour :

* Fournir **beaucoup plus d’adresses** (≈ 340 sextillions)
* Améliorer la **sécurité et l’efficacité**
* Supprimer le besoin du NAT (traduction d’adresse)

---

## 9. 📡 TCP et UDP : les deux protocoles de transport

### Les deux protocoles de transfert de données pour IP :

1. **TCP (Transmission Control Protocol)**
2. **UDP (User Datagram Protocol)**

### Différence principale :

| Protocole | Fiabilité           | Vitesse     | Utilisation typique            |
| --------- | ------------------- | ----------- | ------------------------------ |
| TCP       | Fiable (ack, ordre) | Plus lent   | Web, email, FTP                |
| UDP       | Moins fiable        | Plus rapide | Streaming, jeux en ligne, VoIP |

---

## 10. 🧱 Qu’est-ce qu’un port ?

Un **port** est un **point de communication** logique sur une machine. Il permet d’identifier une application parmi plusieurs sur un même appareil.

### Ports à mémoriser :

| Service | Port TCP |
| ------- | -------- |
| SSH     | 22       |
| HTTP    | 80       |
| HTTPS   | 443      |

---

## 11. 🛠️ Quel outil permet de vérifier la connectivité réseau ?

L’outil le plus courant est **`ping`**, qui utilise le protocole ICMP. Il permet de vérifier :

* Si une machine est joignable
* Le temps de réponse

---

# 📌 Conclusion

Ce cours te donne une vision claire du fonctionnement des réseaux, depuis la transmission des données jusqu’à l’adressage IP et les protocoles. Comprendre cela est essentiel pour tout développeur, administrateur ou technicien réseau.
