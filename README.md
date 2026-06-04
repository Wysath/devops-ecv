# Devops-ecv

<!-- Partie 1 : Badges Shields.io -->
![Dernière version](https://img.shields.io/github/v/release/Wysath/devops-ecv?label=version&style=flat-square)
![Contributeurs](https://img.shields.io/github/contributors/Wysath/devops-ecv?style=flat-square)
![Étoiles](https://img.shields.io/github/stars/Wysath/devops-ecv?style=flat-square)
![Dernier commit](https://img.shields.io/github/last-commit/Wysath/devops-ecv?style=flat-square)
![Workflows](https://img.shields.io/badge/workflows-8-blue?style=flat-square)

<!-- Partie 2 : Badges GitHub Actions par workflow -->
[![First Workflow](https://github.com/Wysath/devops-ecv/actions/workflows/first-workflow.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/first-workflow.yml)
[![Commit Message](https://github.com/Wysath/devops-ecv/actions/workflows/commit-message.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/commit-message.yml)
[![Setup Environnement](https://github.com/Wysath/devops-ecv/actions/workflows/setup-environnement.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/setup-environnement.yml)
[![Artifacts Exemple](https://github.com/Wysath/devops-ecv/actions/workflows/artifacts-exemple.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/artifacts-exemple.yml)
[![Generate Image](https://github.com/Wysath/devops-ecv/actions/workflows/generate-image.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/generate-image.yml)
[![Comment on Commit](https://github.com/Wysath/devops-ecv/actions/workflows/comment-on-commit.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/comment-on-commit.yml)
[![Discord Notification](https://github.com/Wysath/devops-ecv/actions/workflows/discord-notification.yml/badge.svg)](https://github.com/Wysath/devops-ecv/actions/workflows/discord-notification.yml)

Dépôt d’exercices DevOps (ECV) sur **GitHub Actions**.

## Où regarder pour corriger
1. Onglet **Actions** du dépôt : historique des runs, statut, temps d’exécution.
2. Certains workflows sont lançables manuellement : **Actions → (workflow) → Run workflow**.

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
