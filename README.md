# Super JSON Database

Une base de données JSON super rapide, simple et puissante ⚡️

## Fonctionnalités

- 💾 Persistance des données sur disque
- 🗜 Compression des données pour réduire la taille du fichier
- 🚀 Cache en mémoire pour des accès ultra-rapides
- 🔍 Accès aux propriétés imbriquées avec une notation par points
- ⏰ Sauvegarde automatique configurable
- 📂 Snapshots automatiques pour sauvegarder l'état de la base à intervalles réguliers
- 🔒 Accès concurrents gérés avec un verrou
- 🔔 Événements émis lors des opérations clés
- 🔢 Opérations arithmétiques sur les valeurs numériques
- 🗃 Manipulation aisée des tableaux

## Installation

```bash
npm install super-json-database
```

## Exemple d'utilisation

```js
const Database = require("super-json-database");
const db = new Database("./db.json", {
    compress: true, // activer la compression des données
    cache: true, // activer le cache en mémoire
    snapshots: {
        enabled: true, // activer les snapshots
        interval: 24 * 60 * 60 * 1000, // intervalle de 24h entre chaque snapshot
        folder: './backups/' // dossier où sauvegarder les snapshots
    }
});

// Écouter les événements
db.on('save', () => {
    console.log('La base de données a été sauvegardée sur le disque');
});

db.on('change', (key, value) => {
    console.log(`La clé "${key}" a été modifiée avec la valeur:`, value);
});

// Définir des données
db.set("user.name", "John");
db.set("user.age", 30);

// Récupérer des données
db.get("user"); // { name: 'John', age: 30 }

// Vérifier l'existence d'une clé
db.has("user.name"); // true

// Supprimer des données
db.delete("user.age");

// Ajouter des éléments à un tableau
db.push("fruits", "apple");
db.push("fruits", "banana");

// Effectuer des opérations arithmétiques
db.add("counter", 1);
db.subtract("counter", 1);

// Récupérer toutes les données
db.all();

// Vider la base de données
db.clear();
```

## API

### `new Database(filePath, options)`

- `filePath` - Le chemin vers le fichier JSON de la base de données
- `options` - Les options de la base de données:
  - `compress` - Activer la compression des données (défaut: `false`) 
  - `cache` - Activer le cache en mémoire (défaut: `false`)
  - `snapshots` - Configurer les snapshots automatiques
    - `enabled` - Activer les snapshots (défaut: `false`)
    - `interval` - L'intervalle en ms entre chaque snapshot (défaut: `86400000` ms (24h))
    - `folder` - Le dossier où sauvegarder les snapshots (défaut: `./backups/`)

### Événements

- `save` - Émis lorsque la base de données est sauvegardée sur le disque
- `change` - Émis lorsqu'une clé est modifiée. Passe en paramètre la `clé` et la nouvelle `valeur`
- `delete` - Émis lorsqu'une clé est supprimée. Passe en paramètre la `clé` supprimée

### Méthodes

- `get(key)` - Récupère la valeur associée à la clé
- `set(key, value)` - Définit la valeur d'une clé
- `has(key)` - Vérifie si une clé existe
- `delete(key)` - Supprime une clé et sa valeur
- `clear()` - Vide la base de données
- `add(key, number)` - Additionne un nombre à une valeur
- `subtract(key, number)` - Soustrait un nombre à une valeur
- `push(key, element)` - Ajoute un élément à un tableau
- `all()` - Récupère toutes les données de la base

## Licence

MIT
