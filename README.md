## Planning Interactif (Mobile Web App)

Cette webapp affiche un planning hebdomadaire interactif (lundi à dimanche) permettant de sélectionner un créneau pour chaque jour :
- 🌅 Matin
- 🌇 Soir
- 🌙 Nuit
- 💤 Off

Un seul choix par jour est possible. Le planning est mis à jour automatiquement et peut être partagé via un fichier JSON.

### 🎯 Fonctionnalités principales
- Choix par jour avec un visuel épuré et mobile-first
- Deux trames prédéfinies : A (`S O O S S O O`) et B (`O S S O O S S`)
- Sauvegarde locale automatique (via `localStorage`)
- Sauvegarde distante via GitHub Actions (voir ci-dessous)
- Accès protégé par un code à 4 chiffres (persisté dans le navigateur)

---

### 🚀 Déploiement GitHub Pages
Ce dépôt peut être déployé directement via GitHub Pages (branche `main`, dossier racine).

### 🛠 Sauvegarde JSON via GitHub Actions
Chaque commit mettant à jour le fichier `planning.json` est automatiquement pris en charge par un workflow GitHub Action.

#### `.github/workflows/save-json.yml`
```yaml
name: Save planning JSON

on:
  push:
    paths:
      - 'planning.json'

jobs:
  commit-json:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Commit updated JSON
        run: |
          git config --global user.name "GitHub Action"
          git config --global user.email "action@github.com"
          git add planning.json
          git commit -m "📝 Mise à jour automatique du planning" || echo "Aucun changement"
          git push
```

---

### 📁 planning.json
Ce fichier sera utilisé comme point de référence partagé pour l’état du planning (lecture/écriture côté front via fetch).

---

### 🧪 À faire (si besoin)
- Synchronisation régulière avec GitHub (pull en lecture ?)
- Interface multi-utilisateurs
- Historique ou édition collaborative
