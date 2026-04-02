# Devops-ecv

Dépôt d’exercices DevOps (ECV) centré sur **GitHub Actions**.

## Que contient ce dépôt ?
Ce dépôt regroupe plusieurs workflows servant d’exemples/exercices pour valider :
- les déclencheurs (`push`, `workflow_dispatch`)
- l’exécution de jobs simples
- la lecture d’informations de contexte GitHub (`github.event...`)
- l’installation d’outils (Node/Python)
- la gestion d’artefacts
- l’usage de **secrets** + appel API externe
- un déploiement **GitHub Pages**

## Où regarder pour corriger
1. Onglet **Actions** du dépôt : historique des runs, statut, temps d’exécution.
2. Dans chaque run : ouvrir les logs des jobs/steps pour vérifier les sorties attendues.
3. Certains workflows sont lançables manuellement : **Actions → (workflow) → Run workflow**.

## Workflows (dossier `.github/workflows/`)

### 1) `first-workflow.yml` — Mon premier workflow
**Déclencheur :** `push` sur `main`  
**Attendu :** un job qui affiche `Hello, World!` dans les logs.

### 2) `commit-message.yml` — Afficher le message du commit
**Déclencheurs :**
- `push` sur `main`
- `workflow_dispatch`

**Attendu :** affichage du message du commit via `github.event.head_commit.message`.

### 3) `setup-environnement.yml` — Installer les outils
**Déclencheur :** `push` sur `main`

**Attendu :**
- `checkout` du dépôt
- installation **Node.js v18**
- installation **Python 3.10**
- affichage des versions (`node -v`, `python --version`)

### 4) `artifacts-exemple.yml` — Gestion des artefacts
**Déclencheurs :**
- `push` sur `main`
- `workflow_dispatch`

**Attendu :**
- génération d’un fichier `output.txt`
- upload en artefact
- téléchargement dans un job suivant
- `cat ./artifacts/output.txt` affiche le contenu

### 5) `generate-image.yml` — Générer une image + publier sur GitHub Pages
**Déclencheurs :**
- `push` sur `main`
- `workflow_dispatch`

**But :**
- récupérer le message du dernier commit
- appeler l’API **DynaPictures** pour générer une image contenant ce message
- sauvegarder l’image dans `images/`
- générer `images/index.html` (galerie)
- déployer `images/` sur **GitHub Pages**

**Secrets requis pour un run “vert” :**
- `DYNAPICTURES_UID` : identifiant du design DynaPictures
- `DYNAPICTURES` : token API (Bearer)

## GitHub Pages
Quand `generate-image.yml` réussit, le contenu du dossier `images/` est publié (galerie via `index.html`).
