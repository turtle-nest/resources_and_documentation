# Cookie 🍪

La propriété `document.cookie` permet d'accéder et de manipuler les cookies associés au document en cours dans un navigateur web.

**Syntaxe :**

- **Lecture des cookies :**

  
```javascript
  let tousLesCookies = document.cookie;
  ```


  Cette instruction récupère une chaîne contenant tous les cookies accessibles pour le document, chaque paire clé-valeur étant séparée par un point-virgule.

- **Écriture d'un cookie :**

  
```javascript
  document.cookie = "nom=valeur";
  ```


  Cette commande définit ou met à jour un cookie avec le nom et la valeur spécifiés.

**Attributs optionnels lors de la définition d'un cookie :**

Lors de la création ou de la mise à jour d'un cookie, il est possible d'inclure des attributs supplémentaires pour contrôler son comportement :

- **`expires`** : Spécifie la date d'expiration du cookie. Si cet attribut n'est pas défini, le cookie sera supprimé à la fermeture du navigateur.

  
```javascript
  document.cookie = "nom=valeur; expires=Fri, 31 Dec 2025 23:59:59 GMT";
  ```


- **`path`** : Indique le chemin pour lequel le cookie est valide. Par défaut, il est défini sur le chemin de la page qui a créé le cookie.

  
```javascript
  document.cookie = "nom=valeur; path=/";
  ```


- **`domain`** : Spécifie le domaine pour lequel le cookie est valide. Par défaut, il est défini sur le domaine de la page qui a créé le cookie.

  
```javascript
  document.cookie = "nom=valeur; domain=exemple.com";
  ```


- **`secure`** : Indique que le cookie ne doit être envoyé au serveur que lors de requêtes sécurisées (HTTPS).

  
```javascript
  document.cookie = "nom=valeur; secure";
  ```


- **`HttpOnly`** : Empêche l'accès au cookie via JavaScript, le rendant accessible uniquement par le serveur. Notez que cet attribut ne peut être défini que par le serveur lors de l'envoi de l'en-tête HTTP `Set-Cookie`. 

**Considérations de sécurité :**

- **Accès JavaScript** : Les cookies définis avec l'attribut `HttpOnly` ne sont pas accessibles via JavaScript, ce qui protège contre certaines attaques de type cross-site scripting (XSS). 

- **Transmission sécurisée** : L'utilisation de l'attribut `secure` garantit que le cookie est uniquement envoyé sur des connexions sécurisées, protégeant ainsi les informations sensibles pendant la transmission.

- **Restrictions d'accès** : Les attributs `path` et `domain` permettent de restreindre les pages et les domaines pouvant accéder au cookie, offrant un contrôle supplémentaire sur sa portée.

**Remarques :**

- La gestion des cookies via `document.cookie` présente certaines limitations, notamment le fait que tous les cookies sont accessibles sous forme d'une seule chaîne de caractères, ce qui peut rendre leur manipulation complexe.

- Les cookies sont soumis à des restrictions de taille et de nombre, variant selon les navigateurs. Il est donc recommandé de ne pas stocker de grandes quantités de données dans les cookies.

- Pour des opérations plus avancées sur les cookies, l'utilisation de l'API Cookie Store est recommandée, offrant une gestion asynchrone et plus flexible des cookies. 

En résumé, `document.cookie` est un outil puissant pour gérer les cookies côté client, mais son utilisation nécessite une attention particulière aux aspects de sécurité et aux limitations inhérentes à sa conception.