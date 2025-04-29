# 📚 Pagination : Tutoriel Complet (Python et Concepts Généraux)

---

## 1. Introduction : Qu'est-ce que la pagination ?

La **pagination** est une technique utilisée pour diviser un **grand ensemble de données** en **petits morceaux** (des *pages*).  
Cela permet :
- De **réduire la charge réseau** et **améliorer les performances**,
- De **rendre l'affichage plus lisible** pour l'utilisateur,
- D'**optimiser les APIs REST** en ne retournant qu'un sous-ensemble de données par requête.

On parle de pagination dans :
- Les interfaces graphiques (*UI* : tables, listes défilantes...),
- Les **APIs** (REST, GraphQL...),
- Les bases de données (avec `LIMIT`/`OFFSET` en SQL par exemple).

---

## 2. Différentes stratégies de pagination

🔹 **Offset-based pagination** (simple, classique)  
🔹 **Cursor-based pagination** (plus robuste aux suppressions/insertions)  
🔹 **Keyset pagination** (optimisée pour gros volumes)  
🔹 **HATEOAS pagination** (pagination + métadonnées hypermédia)

Nous allons explorer cela en pratique en Python.

---

## 3. Pagination simple avec `page` et `page_size`

**Problème** : Tu veux accéder à une page de données en fonction de deux paramètres :
- `page` : le numéro de la page (1-indexé en général),
- `page_size` : combien d'éléments tu veux par page.

---

### Exemple simple en Python :

```python
def paginate(dataset, page=1, page_size=10):
    """Paginate a dataset using page and page_size parameters."""
    assert isinstance(page, int) and page > 0
    assert isinstance(page_size, int) and page_size > 0

    start = (page - 1) * page_size
    end = start + page_size

    return dataset[start:end]
```

### Exemple d'utilisation :

```python
data = list(range(1, 101))  # Un dataset de 1 à 100
print(paginate(data, page=1, page_size=10))  # [1, 2, ..., 10]
print(paginate(data, page=3, page_size=15))  # [31, 32, ..., 45]
```

---

### Limites de cette approche
- **Suppression ou insertion** d’éléments casse la cohérence de la pagination.
- **Pas d'informations** sur le nombre total de pages, d'éléments restants, etc.

---

## 4. Pagination avec métadonnées hypermédia (HATEOAS)

Selon l'approche **HATEOAS** (*Hypermedia As The Engine Of Application State*), chaque réponse d'API contient :
- Les données paginées,
- **Des liens** pour accéder à la page suivante, précédente, etc.,
- **Des informations** sur la pagination (nombre total, page actuelle, etc.).

🔗 [Voir HATEOAS sur Wikipédia](https://en.wikipedia.org/wiki/HATEOAS)

---

### Exemple enrichi en Python :

```python
def hypermedia_paginate(dataset, page=1, page_size=10):
    """Paginate dataset and return hypermedia metadata."""
    assert isinstance(page, int) and page > 0
    assert isinstance(page_size, int) and page_size > 0

    total_items = len(dataset)
    total_pages = (total_items + page_size - 1) // page_size

    data = paginate(dataset, page, page_size)

    metadata = {
        'page_size': page_size,
        'page': page,
        'data': data,
        'total_items': total_items,
        'total_pages': total_pages,
        'next_page': page + 1 if page < total_pages else None,
        'prev_page': page - 1 if page > 1 else None
    }
    return metadata
```

### Exemple d'utilisation :

```python
result = hypermedia_paginate(list(range(1, 51)), page=2, page_size=10)
print(result)
```

**Sortie** :

```json
{
  "page_size": 10,
  "page": 2,
  "data": [11, 12, ..., 20],
  "total_items": 50,
  "total_pages": 5,
  "next_page": 3,
  "prev_page": 1
}
```

---

### Avantages de HATEOAS
- Améliore **l'autonomie du client** (il sait comment naviguer sans redemander au serveur),
- Permet de construire des **API auto-descriptives**,
- Plus **résilient** aux évolutions du backend.

---

## 5. Pagination résiliente aux suppressions : **Deletion-Resilient Pagination**

🔹 Le problème : Quand on supprime un élément dans une liste, l'offset change.  
🔹 La solution : Utiliser un **curseur** ou **identifiant unique** plutôt qu'un offset simple.

---

### Idée générale :
- Chaque page se termine sur un **dernier identifiant** (`last_id`).
- La page suivante commence **après ce dernier id**.
- **Suppression** ou **insertion** d'un élément **ne casse pas** la pagination.

---

### Exemple en Python :

Supposons un dataset trié par ID :

```python
def deletion_resilient_paginate(dataset, last_id=None, page_size=10):
    """Deletion-resilient pagination using last seen id."""
    if last_id is None:
        start_index = 0
    else:
        start_index = next((i + 1 for i, item in enumerate(dataset) if item > last_id), len(dataset))

    end_index = start_index + page_size
    page_data = dataset[start_index:end_index]

    next_last_id = page_data[-1] if page_data else None

    return {
        'page_data': page_data,
        'next_last_id': next_last_id
    }
```

---

### Exemple d'utilisation :

```python
dataset = list(range(1, 101))  # 1 à 100

page1 = deletion_resilient_paginate(dataset)
print(page1)

page2 = deletion_resilient_paginate(dataset, last_id=page1['next_last_id'])
print(page2)
```

---

**Pourquoi c'est résilient ?**
- Si un élément est supprimé, cela **n'affecte pas** la position du `last_id`.
- Le curseur `last_id` **pointe directement** sur l'élément suivant, peu importe les modifications du dataset.

---

## 6. Résumé final

| Approche                     | Avantages                          | Inconvénients                       |
|-------------------------------|------------------------------------|-------------------------------------|
| Pagination simple (page/size) | Facile à comprendre et implémenter | Fragile aux suppressions/insertions |
| Hypermedia HATEOAS            | API riche, navigation facile       | Plus complexe à construire          |
| Deletion-resilient (cursor)   | Robuste aux suppressions           | Moins intuitif pour débutants       |

---

# 🔥 Conclusion

👉 La pagination est **essentielle** pour la **scalabilité** et la **performance** des applications.  
👉 Selon ton besoin :
- Utilise **page/page_size** pour une pagination rapide.
- Utilise **hypermedia/HATEOAS** pour construire une API plus solide et navigable.
- Utilise **cursor-based** si tu dois gérer beaucoup de suppressions ou un grand nombre de mises à jour.

---

Veux-tu que je te prépare aussi :
- Un **exemple Flask** avec une API REST paginée ?
- Ou un **exemple Django** avec la pagination native de Django REST Framework ?
