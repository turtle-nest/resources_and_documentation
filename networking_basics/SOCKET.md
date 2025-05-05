# 🧪 Comprendre la relation IP + Port = Socket

## 🧭 Objectif du tuto

Ce tutoriel t’apprend :

* Ce qu’est une adresse **IP**
* Ce qu’est un **port**
* Ce qu’est une **socket**
* Comment ils fonctionnent ensemble dans les communications réseau

---

## 🧩 1. Qu’est-ce qu’une **adresse IP** ?

Une **adresse IP** (Internet Protocol) est une **adresse logique** utilisée pour **identifier un appareil** sur un réseau.

🔸 Exemple :

* IPv4 : `192.168.1.5`
* IPv6 : `2001:0db8:85a3::8a2e:0370:7334`

📌 **C’est comme l’adresse d’un immeuble**.

---

## 🚪 2. Qu’est-ce qu’un **port** ?

Un **port** est un **numéro** associé à une application ou un service sur un appareil connecté à Internet.

🔸 Exemple :

* Port 22 → SSH
* Port 80 → HTTP
* Port 443 → HTTPS

📌 **C’est comme le numéro d’appartement dans l’immeuble.**

Chaque application réseau "écoute" ou "parle" via un port spécifique.

---

## 🔌 3. Qu’est-ce qu’une **socket** ?

Une **socket** est une combinaison de :

* **Adresse IP**
* **Numéro de port**

💡 Formule :

```
socket = IP + port
```

🔸 Exemple :

```
192.168.1.5:80 → socket pour le serveur web local
```

📌 **C’est comme dire : immeuble + appartement = une destination unique.**

---

## 🧶 4. Comment cela fonctionne ?

### Exemple concret :

Tu ouvres ton navigateur et tapes `http://example.com` :

1. Ton ordinateur trouve l’**adresse IP** de `example.com` (ex: `93.184.216.34`)
2. Il **se connecte au port 80** (HTTP par défaut)
3. Cela crée une **socket client** (ton IP + port aléatoire) et une **socket serveur** (`93.184.216.34:80`)

Ils communiquent via cette **paire de sockets**.

---

## 📚 Résumé visuel

| Élément    | Exemple          | Rôle                                     |
| ---------- | ---------------- | ---------------------------------------- |
| Adresse IP | `192.168.1.5`    | Identifie une machine                    |
| Port       | `80`             | Identifie un service ou application      |
| Socket     | `192.168.1.5:80` | Point d'accès unique à un service réseau |

---

## 🛠️ Bonus : Commandes utiles

* Voir toutes les connexions actives :

```bash
netstat -tunap
```

* Écouter les ports ouverts :

```bash
ss -tuln
```

---

## 🧠 À retenir

* L’**IP** désigne l’appareil
* Le **port** désigne le service
* La **socket** désigne la **connexion unique**

➡️ C’est la socket qui permet à deux processus réseau de **parler entre eux**, comme deux interlocuteurs qui se téléphonent en connaissant le numéro et l’extension.

---
