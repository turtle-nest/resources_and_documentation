# 🌐 SQL Injection – Cours Complet

---

## 🧠 1. Définition de la SQL Injection

La **SQL Injection (ou injection SQL)** est une **faille de sécurité** exploitant une mauvaise gestion des entrées utilisateurs dans les requêtes SQL. Elle permet à un attaquant d’injecter du code SQL malveillant, capable de :

- Lire ou modifier des données sensibles.
- Bypasser l’authentification.
- Supprimer des tables.
- Prendre le contrôle du serveur de base de données.

### 📌 Exemple simple d’injection
```sql
-- Requête vulnérable
SELECT * FROM users WHERE username = 'admin' AND password = '1234';
```

Si un attaquant entre :
```sql
admin' -- 
```

La requête devient :
```sql
SELECT * FROM users WHERE username = 'admin' -- ' AND password = '1234';
```

Le reste de la requête est commenté (`--`) → l’accès est accordé **sans mot de passe**.

---

## ⚠️ 2. Types de SQL Injection

### 🔹 2.1. Injection Classique (In-band)
L’attaquant insère du SQL directement visible dans les réponses.

### 🔹 2.2. Blind SQL Injection
Aucune erreur SQL n’est retournée, mais l’attaquant obtient des résultats par **observation indirecte** (temps de réponse, logique conditionnelle, etc.).

### 🔹 2.3. Out-of-Band
Des canaux secondaires (ex: e-mail, requêtes HTTP) sont utilisés pour extraire les données si les canaux habituels sont fermés.

---

## 🧪 3. Exemples d'attaques courantes

### 🔸 Authentification contournée
```sql
' OR '1'='1
```

### 🔸 Suppression de table
```sql
'; DROP TABLE users; --
```

### 🔸 Récupération d'informations
```sql
' UNION SELECT credit_card_number, NULL FROM payments; --
```

---

## 🛡️ 4. Bonnes pratiques pour se protéger

---

### ✅ 4.1. Utiliser des requêtes paramétrées (prepared statements)

**La règle d’or** : **ne jamais concaténer directement** les entrées utilisateurs dans une requête SQL.

#### 🔧 Python avec SQLAlchemy (ORM)
```python
user = session.query(User).filter(User.username == input_username).first()
```

#### 🔧 Python avec SQLite (paramétrage manuel)
```python
cursor.execute("SELECT * FROM users WHERE username = ? AND password = ?", (username, password))
```

---

### ✅ 4.2. Échapper les caractères spéciaux

Utiliser des fonctions de la bibliothèque ou de l’ORM pour échapper les entrées utilisateur **si les requêtes paramétrées ne sont pas possibles** (cas très rare).

---

### ✅ 4.3. Utiliser les ORM (Object Relational Mappers)

Des outils comme **SQLAlchemy**, **Django ORM**, **Doctrine (PHP)** gèrent automatiquement les requêtes et les paramètres → **très forte protection** contre les injections.

---

### ✅ 4.4. Filtrer et valider les données en entrée

- N’acceptez **que** ce qui est **attendu** (ex: noms d'utilisateur sans symboles).
- Utiliser des **expressions régulières**, des **schémas de validation JSON**, ou des bibliothèques comme **Cerberus**, **Pydantic**, etc.

---

### ✅ 4.5. Limiter les droits d’accès à la base de données

Créer un **utilisateur de base de données limité**, avec uniquement les **droits nécessaires** :
- Jamais de droits de DROP ou ALTER pour l’utilisateur de production.
- Lecture seule pour les zones publiques.

---

### ✅ 4.6. Masquer les messages d'erreur SQL

Ne jamais afficher les erreurs SQL en production :
- Configurer le framework pour masquer les **traces**.
- Utiliser des **messages d’erreur génériques** côté utilisateur.

---

### ✅ 4.7. Mettre en place des mécanismes de sécurité supplémentaires

- **WAF (Web Application Firewall)** : bloque les requêtes suspectes automatiquement.
- **Surveillance des logs** pour détecter des patterns inhabituels.
- **Taux de limitation (rate limiting)** pour éviter les attaques par force brute.

---

## 🧰 5. Outils de test et détection

### 🔎 Outils d’audit et d’analyse

- **sqlmap** : outil automatisé de test d’injection SQL.
- **Burp Suite** : proxy d’interception pour tester manuellement.
- **OWASP ZAP** : scanner de sécurité open source.

---

## 📚 6. Références & Ressources

- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [Cheat Sheet SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [SQLMap GitHub](https://github.com/sqlmapproject/sqlmap)

---

## 📌 7. Résumé : Checklist anti-injection SQL

✅ Utiliser un ORM ou des requêtes préparées  
✅ Jamais de concaténation directe d’entrée utilisateur  
✅ Validation et nettoyage de toutes les entrées  
✅ Droits limités à la base de données  
✅ Masquer les erreurs SQL en production  
✅ Mettre en place des outils de surveillance  
✅ Tester régulièrement avec sqlmap, ZAP, etc.

---
