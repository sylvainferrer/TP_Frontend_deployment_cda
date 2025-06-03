# 🎧 Frontend Node.js pour le Gestionnaire de Podcasts

Ce projet est une interface web développée en **Node.js + Express + EJS** qui consomme une API PHP et affiche les podcasts dans un tableau interactif avec lecteur audio intégré.

---

## 🧱 Prérequis

- [Node.js](https://nodejs.org/) (v14 ou supérieur recommandé)
- [npm](https://www.npmjs.com/) (installé avec Node.js)
- Le backend PHP (API) doit être en fonctionnement sur

---

## 🚀 Installation

1. **Cloner ce dépôt**

```bash
git clone <url-du-repo>
cd node-frontend
```

2. **Installer les dépendances**

```bash
npm install
```

3. **Modifier le fichier .env avec l'url vers votre API backend**
```
API_URL=http://mon_nom_de_domaine/api/podcast.php
```

4. **Lancer le serveur**

```bash
node app.js
```

## Conseil pour le déploiement

S'assurer que votre serveur web dispose de NodeJS