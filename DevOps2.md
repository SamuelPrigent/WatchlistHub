📁 Fichiers créés

1. .github/workflows/deploy.yml

Workflow GitHub Actions qui se déclenche sur chaque push vers main :

- Backend : Appelle le Deploy Hook Railway via curl
- Frontend : Info que Vercel déploie automatiquement via son intégration GitHub native
- Notification : Résumé du déploiement

2. DEVOPS.md

Guide complet étape par étape pour configurer toutes les plateformes :

🔧 Secrets à configurer

GitHub Secrets (dans Settings → Secrets and variables → Actions)

- RAILWAY_DEPLOY_HOOK : URL du webhook Railway (format :
  https://backboard.railway.app/v1/webhooks/deploy/...)

Railway Variables (dans le dashboard Railway)

MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/watchlisthub
PORT=3000
JWT_SECRET=généré_avec_crypto_64_chars
NODE_ENV=production
FRONTEND_URL=https://votre-app.vercel.app
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...
TMDB_API_KEY=...

Vercel Variables (dans Project Settings → Environment Variables)

VITE_API_URL=https://watchlisthub-backend-production.up.railway.app
VITE_TMDB_API_KEY=...

MongoDB Atlas

- Aucun secret à configurer dans GitHub
- Créer le cluster, l'utilisateur, et autoriser IP 0.0.0.0/0
- Copier l'URI pour l'utiliser dans Railway

📋 Ordre de configuration (résumé)

1. MongoDB Atlas → Créer cluster → Récupérer MONGO_URI
2. Railway → Créer service → Configurer variables → Créer Deploy Hook → Récupérer URL backend
3. Vercel → Créer projet → Configurer frontend/ comme root → Configurer variables → Récupérer URL
   frontend
4. Railway → Retour pour mettre à jour FRONTEND_URL avec l'URL Vercel
5. GitHub → Ajouter secret RAILWAY_DEPLOY_HOOK

🚀 Workflow de déploiement

git add .
git commit -m "feat: deploy to production"
git push origin main

→ GitHub Actions se déclenche
→ Railway redéploie le backend (2-3 min)
→ Vercel redéploie le frontend (1-2 min)
→ Application en ligne ! 🎉

Le fichier DEVOPS.md contient TOUS les détails avec des captures d'écran textuelles pour chaque étape.
Tu peux le suivre étape par étape sans rien oublier !
