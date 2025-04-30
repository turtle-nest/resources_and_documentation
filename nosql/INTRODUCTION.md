# 🧠 **Tutoriel Complet : Introduction à NoSQL et MongoDB**

## 1. 🚀 Qu’est-ce que NoSQL ?

**NoSQL** signifie littéralement "Not Only SQL". Il désigne un ensemble de systèmes de gestion de bases de données qui ne suivent pas le modèle relationnel classique. NoSQL est né pour répondre aux limites des bases relationnelles dans des contextes de données massives, distribuées et non structurées.

Les bases NoSQL :
- ne nécessitent pas de schéma fixe,
- sont souvent distribuées et horizontales (scalables),
- sont conçues pour la haute performance, la flexibilité et la disponibilité.

---

## 2. ⚖️ Différences entre SQL et NoSQL

| Caractéristique       | SQL (relationnel)                      | NoSQL (non relationnel)                          |
|-----------------------|----------------------------------------|--------------------------------------------------|
| Structure             | Tables (lignes et colonnes)            | Documents, graphes, colonnes, paires clé-valeur |
| Schéma                | Fixe (défini à l'avance)               | Flexible ou inexistant                          |
| Langage de requête    | SQL                                     | Propre à chaque système (MongoDB, Riak, etc.)   |
| Relations             | Relations complexes (JOIN)             | Relations rares ou inexistantes                 |
| Scalabilité           | Verticale (puissance machine)          | Horizontale (ajout de machines)                 |
| Transactions          | ACID                                   | BASE (souvent), mais dépend du système          |

---

## 3. 🔒 Qu’est-ce que ACID ?

Les bases relationnelles respectent souvent les propriétés **ACID** :

- **A** (Atomicité) : Une transaction est tout ou rien.
- **C** (Cohérence) : L’état de la base reste valide après la transaction.
- **I** (Isolation) : Les transactions simultanées ne se perturbent pas.
- **D** (Durabilité) : Les données validées sont sauvegardées même en cas de crash.

Les bases NoSQL privilégient souvent le modèle **BASE** :

- **Basically Available** : Toujours disponible, mais éventuellement incohérente.
- **Soft-state** : L’état peut changer avec le temps.
- **Eventually consistent** : La cohérence arrive avec le temps.

---

## 4. 🗂️ Qu’est-ce qu’un stockage de documents ?

Le **document storage** (stockage de documents) est un type de base NoSQL où les données sont stockées sous forme de documents généralement au format **JSON** ou **BSON** (JSON binaire).

Chaque **document** est une structure clé-valeur, semblable à un dictionnaire Python :

```json
{
  "nom": "Alice",
  "âge": 30,
  "compétences": ["Python", "MongoDB"]
}
```

**MongoDB** est le système NoSQL de stockage de documents le plus populaire.

---

## 5. 🔧 Types de bases de données NoSQL

Il existe **4 grandes familles** de bases NoSQL :

1. **Documentaires**  
   Ex : MongoDB, CouchDB  
   → Données structurées comme des documents JSON.

2. **Clé-Valeur**  
   Ex : Redis, Riak, DynamoDB  
   → Données indexées par une clé unique.

3. **Colonnes orientées**  
   Ex : Apache Cassandra, HBase  
   → Données stockées par colonnes, optimisées pour les lectures massives.

4. **Graphes**  
   Ex : Neo4j, OrientDB  
   → Données liées, optimisées pour les relations (réseaux sociaux, etc.).

---

## 6. 🌟 Avantages d’une base NoSQL

- **Scalabilité horizontale** : facile à répartir sur plusieurs serveurs.
- **Haute disponibilité** : architecture distribuée, tolérante aux pannes.
- **Souplesse** : pas besoin de schéma fixe.
- **Performance** : mieux adaptée aux gros volumes de données non structurées.
- **Adaptée au Big Data et au temps réel**.

---

## 7. 🔍 Requêter une base NoSQL (MongoDB)

MongoDB propose des méthodes de requêtes très proches de JavaScript :

```js
// Récupérer tous les documents
db.utilisateurs.find()

// Rechercher un document avec une condition
db.utilisateurs.find({ nom: "Alice" })

// Projection (sélection de champs)
db.utilisateurs.find({ nom: "Alice" }, { age: 1, _id: 0 })
```

Pour des requêtes complexes, on utilise l’**agrégation** :
📚 [Guide MongoDB Aggregation](https://www.mongodb.com/docs/manual/aggregation/)

Exemple :

```js
db.commandes.aggregate([
  { $match: { statut: "livrée" } },
  { $group: { _id: "$client_id", total: { $sum: "$montant" } } }
])
```

---

## 8. ✏️ Insérer, mettre à jour et supprimer des données

### ➕ Insertion

```js
db.utilisateurs.insertOne({
  nom: "Bob",
  age: 25
})

db.utilisateurs.insertMany([
  { nom: "Claire", age: 28 },
  { nom: "David", age: 22 }
])
```

### 🔄 Mise à jour

```js
db.utilisateurs.updateOne(
  { nom: "Bob" },
  { $set: { age: 26 } }
)
```

### ❌ Suppression

```js
db.utilisateurs.deleteOne({ nom: "David" })
db.utilisateurs.deleteMany({ age: { $lt: 25 } })
```

Voir la documentation complète des méthodes ici :  
📚 [MongoDB Method Reference](https://www.mongodb.com/docs/manual/reference/method/)

---

## 9. 🛠️ Utiliser MongoDB avec Python

Avec Python, on utilise souvent la bibliothèque **pymongo**.

### 🔧 Installation

```bash
pip install pymongo
```

### 📄 Connexion à une base MongoDB

```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["ma_base"]
collection = db["utilisateurs"]
```

### ➕ Ajouter un document

```python
collection.insert_one({"nom": "Emma", "âge": 29})
```

### 🔍 Rechercher un document

```python
utilisateur = collection.find_one({"nom": "Emma"})
print(utilisateur)
```

### 🔄 Mettre à jour un document

```python
collection.update_one({"nom": "Emma"}, {"$set": {"âge": 30}})
```

### ❌ Supprimer un document

```python
collection.delete_one({"nom": "Emma"})
```

👉 Tutoriel complet avec exemples :  
📚 [RealPython - Introduction to MongoDB with Python](https://realpython.com/introduction-to-mongodb-and-python/)

---

## 10. 🐚 MongoDB Shell

Le **MongoDB Shell (mongosh)** permet d'interagir en ligne de commande avec votre base :

```bash
mongosh
```

Quelques commandes utiles :

```js
show dbs                  // Liste les bases
use nom_de_base           // Sélectionner une base
db.nom_de_collection.find() // Lire les documents
```

📚 [Guide complet MongoDB Shell](https://www.mongodb.com/docs/mongodb-shell/)

---

## ✅ En résumé

| Élément                              | Description                                          |
|-------------------------------------|------------------------------------------------------|
| **NoSQL**                           | Bases de données non relationnelles                  |
| **Types**                           | Document, clé-valeur, colonnes, graphes              |
| **MongoDB**                         | Base documentaire JSON/BSON                          |
| **pymongo**                         | Client Python pour MongoDB                           |
| **Requêtes**                        | `.find()`, `.insertOne()`, `.updateOne()`, etc.     |
| **Avantages**                       | Scalabilité, flexibilité, performance                |
| **Utilisation**                     | Big Data, web, IoT, mobile, cloud                    |

---
