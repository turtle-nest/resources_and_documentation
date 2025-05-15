# 🧾 FICHE DE RÉVISION – MOCK INTERVIEW (SQL, Python, API, Networking, Async)

---

## 🟦 1. SQL – Requêtes, jointures, agrégation

### ✅ Points clés :

* **SELECT, INSERT, UPDATE, DELETE**
* **JOIN** : relier plusieurs tables
* `GROUP BY`, `HAVING`, `ORDER BY`
* Agrégats : `SUM()`, `AVG()`, `COUNT()`, `MAX()`
* `NULL`, `IS NULL`, `LEFT JOIN` vs `INNER JOIN`
* Structure relationnelle (1NF à 3NF)
* `CREATE TABLE`, types (`INTEGER`, `TEXT`, `REAL`, etc.)

### 💬 Questions fréquentes :

| Question                                          | Attendu                                                     |
| ------------------------------------------------- | ----------------------------------------------------------- |
| Différence entre `WHERE` et `HAVING` ?            | `WHERE` filtre les lignes, `HAVING` filtre les groupes      |
| LEFT JOIN vs INNER JOIN ?                         | `LEFT` garde tout à gauche, `INNER` ne garde que les matchs |
| Requête pour total par utilisateur ?              | `SELECT name, SUM(...) FROM ... GROUP BY name;`             |
| Peut-on avoir des clés étrangères ?               | Oui, via `FOREIGN KEY(user_id) REFERENCES users(id)`        |
| Comment afficher les utilisateurs sans commande ? | `LEFT JOIN` + `WHERE o.id IS NULL`                          |

---

## 🟨 2. Python – Syntaxe, structures, POO, exceptions

### ✅ Points clés :

* Types : `int`, `str`, `list`, `dict`, `set`, `tuple`
* Fonctions (`def`, `*args`, `**kwargs`, `return`)
* Exceptions (`try / except / finally`, `raise`)
* POO : `class`, `__init__`, `self`, méthodes
* Typage : `List[int]`, `Dict[str, float]`, `Union[...]`
* Lecture/écriture de fichiers + JSON (`with open`, `json.load`)
* Blocs `if __name__ == "__main__"` pour exécution directe

### 💬 Questions fréquentes :

| Question                                  | Attendu                                     |
| ----------------------------------------- | ------------------------------------------- |
| Différence `list` / `tuple` ?             | `list` = modifiable, `tuple` = immuable     |
| `is` vs `==` ?                            | `is` compare l'identité, `==` les valeurs   |
| Que fait `try / except / finally` ?       | Gère les erreurs, assure un bloc de fin     |
| C’est quoi `self` ?                       | Référence à l’objet courant dans une classe |
| Que retourne une fonction sans `return` ? | `None`                                      |

---

## 🟥 3. API – REST, HTTP, Flask, JSON

### ✅ Points clés :

* API REST = interface web basée sur HTTP
* Méthodes HTTP : `GET`, `POST`, `PUT`, `DELETE`
* Codes HTTP : `200`, `201`, `204`, `400`, `401`, `404`, `500`
* `Content-Type: application/json`
* Utiliser `requests` (client) ou `Flask` (serveur)
* API = **stateless**, data échangée en **JSON**
* `@app.route`, `request.get_json()`, `jsonify()`

### 💬 Questions fréquentes :

| Question                          | Attendu                              |
| --------------------------------- | ------------------------------------ |
| Différence entre GET et POST ?    | `GET` lit, `POST` crée               |
| Que signifie 201 ?                | Ressource créée avec succès          |
| Format d’échange d’une API REST ? | JSON                                 |
| Qu’est-ce qu’un endpoint ?        | Une URL qui représente une ressource |
| C’est quoi `stateless` ?          | Aucune mémoire entre les requêtes    |

---

## 🟩 4. Networking – Bases système, commandes, OSI

### ✅ Points clés :

* Protocole TCP : fiable, ordonné
* UDP : rapide mais sans garantie
* DNS : transforme un nom de domaine en IP
* IP = adresse machine, Port = point d’accès à un service
* Modèle OSI (7 couches, connaître les 4 premières)
* Commandes utiles : `ping`, `curl`, `telnet`, `netstat`, `nc`, `dig`

### 💬 Questions fréquentes :

| Question                       | Attendu                                   |
| ------------------------------ | ----------------------------------------- |
| TCP vs UDP ?                   | TCP = fiable ; UDP = rapide, non fiable   |
| C’est quoi un port ?           | Un point d’entrée logique pour un service |
| DNS ?                          | Traduit un nom en adresse IP              |
| Commande pour tester un port ? | `telnet`, `curl`, `nc`                    |
| Que fait `ping` ?              | Vérifie si une machine répond (ICMP)      |

---

## 🌀 5. Async Python – `async`, `await`, `asyncio`

### ✅ Points clés :

* `async def` : définit une fonction asynchrone
* `await` : attend une coroutine
* `asyncio.run()` : lance un programme asynchrone
* `asyncio.sleep()` : temporisation non bloquante
* `asyncio.gather()` : exécute plusieurs tâches en parallèle
* Asynchrone = utile pour I/O (réseau, fichiers), pas pour calcul pur

### 💬 Questions fréquentes :

| Question                                           | Attendu                                                     |
| -------------------------------------------------- | ----------------------------------------------------------- |
| C’est quoi une coroutine ?                         | Une fonction `async` qu'on peut suspendre et reprendre      |
| Différence thread vs async ?                       | Thread = multi-processus / Async = monothread, non bloquant |
| Que fait `await` ?                                 | Attend le résultat d’une coroutine                          |
| Que fait `gather()` ?                              | Lance plusieurs tâches en parallèle                         |
| Peut-on `await` en dehors d’une fonction `async` ? | Non                                                         |

---

## 🧠 Conseils pour l’entretien :

* Sois clair et structuré quand tu expliques une requête ou un script
* Si tu ne sais pas, dis-le simplement et propose une piste
* Prévois une intro rapide pour te présenter + projet préféré
* Prépare une **question pertinente à poser à la fin**

---
