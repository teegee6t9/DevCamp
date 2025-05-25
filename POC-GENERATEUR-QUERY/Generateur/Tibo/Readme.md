# Preuve de Concept — Générateur de Géocaches (Fichier dans Répertoire)


##Liens page ajouter/editer/supprimer :

[Ajouter](http://172.105.106.183/service.geocache/generateur/ajouter-geocache.html)
[Editer](http://172.105.106.183/service.geocache/generateur/editer-geocache.html)
[Supprimer](http://172.105.106.183/service.geocache/generateur/supprimer-geocache.html)


Ce projet démontre comment utiliser un répertoire de fichiers comme source de données dans une application web, en construisant une API REST avec Node.js et Express. Les géocaches sont stockées dans un fichier local `data/geocaches.json`, manipulé directement en lecture et écriture.

Chaque géocache contient les champs suivants : un identifiant auto-incrémenté (`id`), un `nom`, un `proprietaire`, ainsi que ses coordonnées `latitude` et `longitude`.

L’API expose plusieurs routes pour manipuler ces géocaches :

- `GET /geocache/liste` retourne toutes les géocaches.
- `GET /geocache/:id` permet de récupérer une géocache précise. Une expression régulière est utilisée dans cette route pour s’assurer que l’ID soit bien un entier.
- `POST /geocache/ajouter` permet d’ajouter une nouvelle géocache. Exemple de requête JSON utilisée :

```json
{
  "nom": "Cache du phare",
  "proprietaire": "alex",
  "latitude": 47.2,
  "longitude": -70.5
}
```

Réponse obtenue :

```json
{
  "id": 4,
  "nom": "Cache du phare",
  "proprietaire": "alex",
  "latitude": 47.2,
  "longitude": -70.5
}
```

- `PUT /geocache/editer/4` permet de modifier une géocache existante. Exemple de corps envoyé :

```json
{
  "nom": "Cache du port"
}
```

Résultat obtenu :

```json
{
  "id": 4,
  "nom": "Cache du port",
  "proprietaire": "alex",
  "latitude": 47.2,
  "longitude": -70.5
}
```

- `DELETE /geocache/effacer/4` supprime la géocache avec l’identifiant 4. Réponse obtenue :

```json
{
  "message": "Geocache 4 effacée."
}
```

Les modifications sont directement enregistrées dans le fichier geocaches.json, ce qui permet une persistance sans base de données.

Concernant la question "Peut-on utiliser POST au lieu de DELETE ?", la réponse est non : bien que techniquement possible, cela va à l'encontre des bonnes pratiques REST. DELETE est le verbe approprié pour une suppression.

Pour tester l’API, lance node app.js après npm install, puis utilise les fichiers HTML fournis :

    - ajouter-geocache.html pour ajouter

    - editer-geocache.html pour modifier

    - supprimer-geocache.html pour supprimer

Ces pages utilisent fetch() pour envoyer les requêtes. Aucun outil externe n’est nécessaire. Le projet répond aux exigences : API REST, usage d’un fichier comme source, route avec regex, et démonstration via HTML.
