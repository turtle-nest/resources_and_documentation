# 📘 **Cours complet de révision SQL**

## 🔹 1. Introduction à SQL

### ➤ Définition
**SQL (Structured Query Language)** est un langage normalisé pour interagir avec les bases de données relationnelles. Il permet :
- la **création** de structures,
- la **manipulation** des données,
- l’**interrogation** des données,
- la **gestion des accès**.

---

## 🔹 2. Les catégories de commandes SQL

| **Catégorie** | **Acronyme** | **Commandes** |
|---------------|--------------|----------------|
| Définition     | **DDL**      | `CREATE`, `ALTER`, `DROP` |
| Manipulation   | **DML**      | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| Contrôle       | **DCL**      | `GRANT`, `REVOKE` |
| Transaction    | **TCL**      | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

## 🔹 3. Création de base de données et tables (DDL)

### ➤ Créer une base
```sql
CREATE DATABASE nom_de_base;
```

### ➤ Créer une table
```sql
CREATE TABLE employes (
  id INT PRIMARY KEY,
  nom VARCHAR(50),
  age INT,
  salaire DECIMAL(10,2)
);
```

### ➤ Modifier une table
```sql
ALTER TABLE employes ADD email VARCHAR(100);
```

### ➤ Supprimer une table
```sql
DROP TABLE employes;
```

---

## 🔹 4. Manipulation de données (DML)

### ➤ Insérer des données
```sql
INSERT INTO employes (id, nom, age, salaire) VALUES (1, 'Alice', 30, 3000.00);
```
Ou plusieurs lignes :
```sql
INSERT INTO employes VALUES 
(2, 'Bob', 28, 3200.00),
(3, 'Claire', 35, 4000.00);
```

### ➤ Lire des données (requête SELECT)
```sql
SELECT nom, salaire FROM employes WHERE age > 30;
```

### ➤ Mettre à jour des données
```sql
UPDATE employes SET salaire = 3500.00 WHERE id = 2;
```

### ➤ Supprimer des données
```sql
DELETE FROM employes WHERE age < 30;
```

---

## 🔹 5. Clauses importantes dans SELECT

| **Clause** | **Utilité** |
|------------|-------------|
| `WHERE` | Filtrer les lignes |
| `ORDER BY` | Trier les résultats |
| `GROUP BY` | Grouper les résultats |
| `HAVING` | Filtrer après le groupement |
| `DISTINCT` | Éliminer les doublons |
| `LIMIT` (ou `FETCH`) | Limiter le nombre de résultats |

### ➤ Exemple combiné
```sql
SELECT nom, AVG(salaire) 
FROM employes 
WHERE age > 25 
GROUP BY nom 
HAVING AVG(salaire) > 3000 
ORDER BY nom ASC;
```

---

## 🔹 6. Les opérateurs SQL

### ➤ Comparaison
`=`, `!=`, `<`, `>`, `<=`, `>=`

### ➤ Logiques
`AND`, `OR`, `NOT`

### ➤ Plage et motifs
- `BETWEEN ... AND ...`
- `LIKE 'A%'` (commence par A)
- `IN (...)`
- `IS NULL` / `IS NOT NULL`

---

## 🔹 7. Contraintes d'intégrité

| **Contrainte** | **Utilité** |
|----------------|-------------|
| `PRIMARY KEY` | Identifie de façon unique une ligne |
| `FOREIGN KEY` | Référence une clé primaire d’une autre table |
| `UNIQUE` | Empêche les doublons |
| `NOT NULL` | Empêche les valeurs nulles |
| `CHECK` | Imposer des conditions personnalisées |
| `DEFAULT` | Valeur par défaut si non spécifiée |

---

## 🔹 8. Les jointures (JOIN)

| **Type** | **Explication** |
|----------|------------------|
| `INNER JOIN` | Donne uniquement les lignes correspondantes |
| `LEFT JOIN` | Toutes les lignes de la table de gauche + correspondances |
| `RIGHT JOIN` | Toutes les lignes de la table de droite + correspondances |
| `FULL OUTER JOIN` | Toutes les lignes des deux tables, avec ou sans correspondance |
| `SELF JOIN` | Jointure d’une table avec elle-même |

### ➤ Exemple de `INNER JOIN`
```sql
SELECT e.nom, d.nom
FROM employes e
INNER JOIN departements d ON e.dept_id = d.id;
```

---

## 🔹 9. Fonctions SQL

### ➤ Fonctions d’agrégation
- `COUNT(*)`
- `SUM(colonne)`
- `AVG(colonne)`
- `MAX(colonne)`
- `MIN(colonne)`

### ➤ Fonctions de chaîne
- `CONCAT()`
- `UPPER()`, `LOWER()`
- `SUBSTRING()`

### ➤ Fonctions numériques
- `ROUND()`
- `FLOOR()`, `CEIL()`

---

## 🔹 10. Transactions (TCL)

### ➤ Exemple
```sql
BEGIN;
UPDATE comptes SET solde = solde - 100 WHERE id = 1;
UPDATE comptes SET solde = solde + 100 WHERE id = 2;
COMMIT;
```

- `ROLLBACK` pour annuler
- `SAVEPOINT` pour marquer un état intermédiaire

---

## 🔹 11. Vues (Views)

### ➤ Créer une vue
```sql
CREATE VIEW vue_employes_ages AS
SELECT nom, age FROM employes WHERE age > 30;
```

### ➤ Utiliser une vue
```sql
SELECT * FROM vue_employes_ages;
```

---

## 🔹 12. Index

Permet d’accélérer les recherches :
```sql
CREATE INDEX idx_nom ON employes(nom);
```

---

## 🔹 13. Bonnes pratiques SQL

- Toujours spécifier `WHERE` en `UPDATE` / `DELETE`
- Utiliser des alias (`AS`) pour la lisibilité
- Utiliser des clés primaires et étrangères
- Préférer `INNER JOIN` à `WHERE` pour les jointures explicites

---

## ✅ **Quiz rapide final (5 questions)**

1. Que retourne `SELECT COUNT(*) FROM employes;` ?  
2. Quelle clause utilise-t-on pour filtrer des groupes ?  
3. Quelle est la différence entre `HAVING` et `WHERE` ?  
4. Quelle jointure permet de voir toutes les lignes de deux tables, même sans correspondance ?  
5. Peut-on faire un `JOIN` sur une table avec elle-même ? Comment ?
