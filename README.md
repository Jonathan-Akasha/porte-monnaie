# Comptes · Âkasha

App personnelle de suivi de comptes avec registre busking.
100% locale, authentification biométrique, PWA installable.

## 📦 Contenu du dossier

```
index.html           → l'application
manifest.json        → métadonnées PWA (icône, couleurs, etc.)
sw.js                → service worker (fonctionnement hors-ligne)
icon.svg             → icône source vectorielle
icon-192.png         → icône 192×192 (Android)
icon-512.png         → icône 512×512 (Android, splash screen)
apple-touch-icon.png → icône 180×180 (iPhone)
favicon.png          → favicon navigateur
```

## 🚀 Déploiement sur GitHub Pages

### 1. Créer le dépôt

- Va sur github.com, crée un nouveau dépôt (public ou privé, GitHub Pages marche sur les deux avec un compte Pro)
- Nom suggéré : `comptes` ou `akasha-comptes`
- Upload tous les fichiers de ce dossier à la racine du dépôt

### 2. Activer GitHub Pages

- Dans le dépôt → **Settings** → **Pages** (menu de gauche)
- **Source** : `Deploy from a branch`
- **Branch** : `main` (ou `master`), dossier `/ (root)`
- Sauvegarder

GitHub te donne une URL du type `https://tonpseudo.github.io/comptes/` — vérifie que ça marche avant de passer à l'étape suivante.

### 3. Connecter ton domaine âkasha.fr

**Dans ton dépôt GitHub** :
- Settings → Pages → **Custom domain** → entre `compteur.âkasha.fr`
- Coche **Enforce HTTPS** (attendre quelques minutes après l'étape DNS)

**Chez ton registrar de domaine** (là où tu as acheté âkasha.fr), crée un enregistrement DNS :

```
Type    Nom       Valeur
CNAME   compteur  tonpseudo.github.io
```

Remplace `tonpseudo` par ton pseudo GitHub. Propagation DNS : de quelques minutes à 24h.

⚠️ **Note sur le â accentué** : certains registrars veulent le domaine en punycode : `xn--kasha-fva.fr`. Si le champ refuse le `â`, utilise cette version.

### 4. Installer sur ton écran d'accueil

Une fois `https://compteur.âkasha.fr` accessible :

**iPhone (Safari)** : bouton Partager ⬆️ → "Sur l'écran d'accueil"
**Android (Chrome)** : menu ⋮ → "Installer l'application" ou "Ajouter à l'écran d'accueil"

L'app s'ouvre en plein écran, sans barre de navigateur, avec l'icône porte-monnaie.

### 5. Premier lancement

1. Création d'un code PIN à 4 chiffres (demandé deux fois pour confirmation)
2. L'app propose d'activer l'empreinte digitale → accepte
3. Chaque ouverture suivante : empreinte directement, PIN en secours

## 🔐 Sur la sécurité

- **Toutes les données** (comptes, busking, PIN, identifiant biométrique) restent **dans le navigateur du téléphone** (localStorage). Rien n'est envoyé nulle part.
- **L'empreinte** passe par WebAuthn — le capteur biométrique du téléphone signe une clé cryptographique. Ton empreinte elle-même ne quitte jamais le capteur du tél.
- **Sauvegarde** : pense à utiliser l'export JSON (Réglages → Exporter) de temps en temps. Si tu changes de téléphone ou effaces les données du site, tu perds tout sinon.

## ✏️ Pour modifier l'app plus tard

Il suffit de mettre à jour le(s) fichier(s) sur GitHub, GitHub Pages redéploie automatiquement en 1-2 minutes. Le service worker (sw.js) met en cache — pour forcer la mise à jour, change le numéro de version à la ligne `const CACHE = 'comptes-akasha-v1'` dans sw.js (mets v2, v3, etc.) à chaque modification importante.
