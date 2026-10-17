# Personnages TCG Novel France — GitHub Pages + Firebase

## Fichiers à placer à la racine du dépôt

- `index.html` : l'application web (renommer le HTML fourni en `index.html`).
- `firebase-config.js` : configuration publique de l'application Firebase.
- `firestore.rules` : règles Firestore à copier dans la console Firebase.
- `personnages.csv` : CSV initial, facultatif. Il est chargé automatiquement au premier démarrage si Firestore est vide.
- `oeuvres.json` : JSON des œuvres, facultatif, chargé avec le CSV initial.

Les modifications (choix de photos, rareté, GIF, etc.) sont synchronisées en temps réel dans Cloud Firestore. Le bouton **Exporter…** permet de choisir le format CSV ou Excel et les colonnes à inclure. Le classeur Excel contient un tableau structuré avec filtres, style alterné et largeurs de colonnes adaptées. L'import d'un nouveau CSV fusionne les personnages : les doublons (clé normalisée `personnage + œuvre`) sont ignorés et les choix déjà enregistrés restent dans leur collection dédiée.

## Configuration gratuite

1. Crée un projet sur https://console.firebase.google.com/.
2. Dans **Authentication → Sign-in method**, active **Google**.
3. Dans **Authentication → Settings → Authorized domains**, ajoute le domaine GitHub Pages, par exemple `ton-compte.github.io`.
4. Dans **Firestore Database**, crée une base de données.
5. Dans les paramètres du projet, crée une application Web et copie sa configuration dans `firebase-config.js`.
6. Dans l'onglet **Firestore → Rules**, copie le contenu de `firestore.rules` et publie les règles.
7. Place le CSV initial à la racine sous le nom exact `personnages.csv` (avec au minimum les colonnes `personnage` et `oeuvre`). Le JSON des œuvres peut s'appeler `oeuvres.json`.
8. Envoie les fichiers sur GitHub puis active **Settings → Pages → Deploy from a branch**, branche `main`, dossier `/ (root)`.

## Accès et sécurité

La configuration des règles fournie permet à tout utilisateur connecté avec Google de lire et modifier la base. C'est pratique pour un outil collaboratif ouvert, mais cela ne limite pas les contributeurs à ton groupe. Pour un usage privé, configure une liste d'adresses e-mail autorisées dans les règles Firestore avant de partager le site.

La configuration Firebase côté navigateur n'est pas un mot de passe. La protection des données dépend des règles Firestore. Le plan Spark de Firebase est gratuit dans les limites de quotas indiquées par Firebase ; un usage élevé peut dépasser les quotas gratuits.

## Import et export

- Import : sélectionne un CSV depuis le bouton **Importer CSV + JSON**. Les nouveaux personnages sont ajoutés, les doublons sont ignorés.
- Export : **Exporter…** permet de choisir CSV ou Excel et de sélectionner les colonnes à inclure. ExcelJS est chargé depuis jsDelivr au moment d'un export Excel ; une connexion Internet est requise pour ce format. Le classeur Excel utilise un tableau structuré nommé `Personnages`, avec filtres et lignes alternées.
- Les fichiers de la racine sont une base d'initialisation ; après le premier chargement, Firestore devient la source partagée des modifications.
