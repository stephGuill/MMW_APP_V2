<!-- EXPLICATION FICHIER: README.md - Document de reference pour le projet. -->
# Mahjong Master Web

Application full-stack basee sur ton brief: Mahjong revisite avec quiz developpeur web, mode invite hors connexion, compte utilisateur, podium, RGPD, API securisee JWT, architecture MVC, CRUD, React + Express + Tailwind + Docker.

## Stack

- Frontend: React, Vite, Tailwind CSS, React Router
- Backend: Node.js, Express, MySQL/MariaDB, JWT, bcrypt, helmet, rate-limit
- Infra: Docker Compose

## Fonctionnalites livrees

- Jeu Mahjong revisite (matching de paires)
- Tuiles quiz (?) qui donnent un joker double paire
- Progression par niveaux
- Score local hors connexion
- Inscription / connexion JWT
- Confirmation d'inscription par email avant activation du compte
- Profil utilisateur
- Classement (podium)
- FAQ et page RGPD
- Backend MVC + CRUD questions (admin)

## Arborescence

- frontend/
- backend/
- docs/
- docker-compose.yml

## Lancer en local sans Docker

### 1) Backend

- Copier backend/.env.example en backend/.env
- Installer dependances: npm install
- Demarrer API: npm run dev
- Initialiser les donnees de base: executer backend/sql/schema.sql puis backend/sql/seed.sql

#### Configuration email reelle (Gmail ou Brevo)

- Ouvrir backend/.env
- Pour Gmail SMTP:
- SMTP_HOST=smtp.gmail.com
- SMTP_PORT=587
- SMTP_SECURE=false
- SMTP_USER=ton_adresse_gmail
- SMTP_PASS=mot_de_passe_application_google (16 caracteres)
- MAIL_FROM=ton_adresse_gmail
- Pour Brevo SMTP:
- SMTP_HOST=smtp-relay.brevo.com
- SMTP_PORT=587
- SMTP_SECURE=false
- SMTP_USER=ton_login_brevo
- SMTP_PASS=ta_cle_smtp_brevo
- MAIL_FROM=no-reply@ton-domaine
- Pour forcer l'envoi reel (pas fallback local): INVITE_DEV_FALLBACK=false
- Redemarrer l'API apres toute modification du fichier .env

### 2) Frontend

- Copier frontend/.env.example en frontend/.env
- Installer dependances: npm install
- Demarrer web: npm run dev

## Lancer avec Docker

- docker compose up --build
- Frontend: <http://localhost:5173>
- API: <http://localhost:4000/api/health>

## Seed admin

- Email: <admin@mahjong-master-web.local>
- Mot de passe: Admin123!
- Fichier seed: backend/sql/seed.sql

## Endpoints API principaux

- POST /api/auth/register
- POST /api/auth/login
- GET|POST /api/auth/verify-email
- GET /api/auth/me
- GET /api/questions
- POST /api/questions (admin)
- PUT /api/questions/:id (admin)
- DELETE /api/questions/:id (admin)
- POST /api/games (auth)
- GET /api/leaderboard

## Base de donnees

- Script schema: backend/sql/schema.sql
- Compatible MySQL/MariaDB (phpMyAdmin, AlwaysData, hebergements mutualises)
- Tables principales: users, roles, user_roles, games, user_progress, reward_catalog, user_reward_balances, user_reward_events, email_verification_tokens, questions

## Livrables de conception

Voir dossier docs/:

- etude de marche, SWOT, benchmark
- cahier des charges
- sitemap, structure, diagramme d'utilisation
- charte graphique + logo
- wireframe, maquette, prototype
- MCD, MLD, MPD, DDL, architecture base de donnees

## Notes de production

- Remplacer JWT_SECRET
- Configurer CORS_ORIGIN
- Ajouter validation avancee (zod/joi)
- Ajouter tests API et E2E

## Deploiement Gratuit Propre (Sans Interstitiel)

### Option recommandee: Backend Render + Frontend Netlify

1. Backend sur Render (free)

- Creer un nouveau service web depuis ce repo.
- Render detecte `render.yaml` automatiquement.
- Configurer les variables sensibles suivantes:
- `DATABASE_URL`
- `JWT_SECRET`
- `CORS_ORIGIN` = URL Netlify (ex: `https://mahjong-master-web.netlify.app`)
- `APP_URL` = URL Netlify
- `SMTP_HOST`, `SMTP_PORT`, `SMTP_SECURE`, `SMTP_USER`, `SMTP_PASS`, `MAIL_FROM`
- URL backend finale attendue: `https://mahjong-master-api.onrender.com`

1. Base de donnees

- Creer une base PostgreSQL gratuite (Render Postgres, AlwaysData ou autre).
- Executer `backend/sql/schema.sql`, puis `backend/sql/seed.sql`.

1. Frontend sur Netlify (free)

- Importer le repo sur Netlify.
- Root directory: `frontend`.
- Build command: `npm run build`.
- Publish directory: `dist`.
- Variable d'environnement a definir: `VITE_API_URL=https://mahjong-master-api.onrender.com/api`.

1. Verification

- Health API: `https://mahjong-master-api.onrender.com/api/health`.
- Front: `https://mahjong-master-web.netlify.app`.
- Tester une invitation depuis le profil puis le lien `/invite?token=...`.

### Indexation Google (important)

- Le front inclut deja `robots.txt` et `sitemap.xml`
- Ajouter le site dans Google Search Console
- Soumettre `https://mahjong-master-web.netlify.app/sitemap.xml`
- L'indexation peut prendre plusieurs jours (ce n'est jamais instantane)
# MMW_APP_V2
