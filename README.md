# Palier — maintenance observée

Application statique, locale et hors ligne pour tester progressivement un apport calorique compatible avec une stabilité du poids à activité comparable. Aucune dépendance JavaScript externe, aucun compte, aucune télémétrie.

## Utilisation

1. Ouvrir l’application ; saisir le profil puis confirmer le premier palier calorique proposé (modifiable).
2. Chaque matin : poids du jour, calories/macros/pas/activité de la veille. Les champs inconnus restent vides.
3. L’application observe les tendances et propose, sans appliquer automatiquement, de nouveaux paliers.
4. Exporter régulièrement **Réglages → Sauvegarde JSON**. IndexedDB reste sur le navigateur/appareil utilisé : un autre iPhone ou Safari n’aura pas automatiquement les données.

Le guide détaillé d’utilisation et de configuration est disponible dans [GUIDE_UTILISATION.md](GUIDE_UTILISATION.md).

## Publication sur GitHub Pages

1. Créer un dépôt GitHub, puis déposer **le contenu du dossier maintenance-calorique à la racine** du dépôt (ne pas déposer seulement le ZIP).
2. Dans **Settings → Pages → Build and deployment**, choisir **Deploy from a branch**, branche **main**, dossier **/(root)**, puis **Save**.
3. Ouvrir l’URL indiquée par GitHub Pages en HTTPS. Lors d’une nouvelle version du code, incrémenter CACHE dans sw.js (par exemple palier-shell-v2) pour actualiser l’app shell. Ne jamais effacer la base IndexedDB pendant une mise à jour.

Pour un essai local : `python3 -m http.server 8000` dans ce dossier, puis `http://localhost:8000`. Un fichier ouvert directement avec `file://` n’installe pas la PWA et ne teste pas le service worker.

## iPhone

Safari → URL GitHub Pages → Partager → **Ajouter à l’écran d’accueil** → ouvrir l’icône Palier. Safari et l’app installée peuvent avoir des espaces de stockage distincts selon leur contexte ; commence la saisie dans l’app installée et garde une sauvegarde JSON. Une exportation JSON permet de migrer ou de restaurer les données.

## Architecture

- `index.html`, `styles.css`, `app.js` : interface mobile et interactions.
- `engine.js` : moteur déterministe et seuils opérationnels.
- `db.js` : IndexedDB version 2, validation, fusion et restauration.
- `charts.js` : SVG natif sans réseau.
- `manifest.webmanifest`, `sw.js`, `icons/` : PWA et app shell hors ligne.
- `tests/engine.test.js` : tests du moteur et des formats de sauvegarde.

Le document [METHODOLOGIE.md](METHODOLOGIE.md) décrit précisément le protocole et les sources. [AUDIT.md](AUDIT.md) consigne l’audit du prototype, les contrôles et les limites.

## Tests automatisés

Node.js 20+ : `npm test`. Aucun `npm install` n’est nécessaire. Le jeu de données de test est fictif et n’est jamais chargé dans l’application utilisateur.

