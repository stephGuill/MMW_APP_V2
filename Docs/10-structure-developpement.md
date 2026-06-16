<!-- EXPLICATION FICHIER: docs/10-structure-developpement.md - Document de reference pour le projet. -->
# 14 - Structure De Developpement

## Objectif

Ce document fixe une structure de dev claire pour maintenir et faire evoluer Mahjong Master Web sans regressions.

## Arborescence Recommandee

```text
MMW_APP_V2/
  backend/
    src/
      config/         # Connexions et configuration technique
      controllers/    # Logique HTTP (validation simple + orchestration)
      middleware/     # Auth, roles, protections transverses
      models/         # Acces SQL, transactions et mapping DB
      routes/         # Mapping URL -> controller
      services/       # Services externes (mail, etc.)
    sql/
      schema.sql      # Structure complete de la base
      seed.sql        # Donnees initiales
  frontend/
    src/
      components/     # UI reutilisable + logique de jeu
      pages/          # Ecrans routes
      data/           # Donnees statiques (tuning, layouts, quiz)
      services/       # Client API
    public/           # robots.txt, sitemap.xml, assets statiques
  docs/               # Documentation fonctionnelle et technique
```

## Regles De Separation Des Responsabilites

- `routes`: aucune logique metier, uniquement declaration des endpoints.
- `controllers`: validation d'entree, gestion des statuts HTTP, appel des modeles/services.
- `models`: logique SQL uniquement, requetes parametrees et transactions explicites.
- `services`: communication externe (SMTP, APIs), sans dependre d'Express.
- `frontend/pages`: orchestration ecran + composition.
- `frontend/components`: comportement UI isole, testable.

## Workflow Dev Local

### 1. Prerequis

- Node.js 20+
- PostgreSQL
- npm

### 2. Setup backend

```bash
cd backend
cp .env.example .env
npm install
```

Initialiser la base:

```sql
-- executer dans cet ordre
backend/sql/schema.sql
backend/sql/seed.sql
```

Lancer l'API:

```bash
npm run dev
```

### 3. Setup frontend

```bash
cd frontend
cp .env.example .env
npm install
npm run dev
```

## Convention De Branches

- `main`: production stable
- `develop`: integration continue
- `feature/<nom-court>`: nouvelle fonctionnalite
- `fix/<nom-court>`: correction bug
- `docs/<nom-court>`: documentation

## Convention De Commit

Format conseille:

```text
type(scope): message
```

Exemples:

- `feat(auth): add email verification endpoint`
- `fix(game): block trapped free tiles`
- `docs(dev): add development structure guide`

## Checklist Pull Request

- Build frontend OK (`frontend: npm run build`)
- Backend charge sans erreur d'import
- Endpoints modifies testes (auth, game, invites)
- Schema SQL coherent avec les modeles
- Variables `.env.example` mises a jour
- Docs mises a jour si comportement change

## Variables D'environnement Critiques

### Backend

- `DATABASE_URL`
- `JWT_SECRET`
- `CORS_ORIGIN`
- `APP_URL`
- `SMTP_HOST`
- `SMTP_PORT`
- `SMTP_SECURE`
- `SMTP_USER`
- `SMTP_PASS`
- `MAIL_FROM`
- `EMAIL_VERIFY_EXPIRES_IN`
- `INVITE_EXPIRES_IN`
- `INVITE_PER_HOUR`

### Frontend

- `VITE_API_URL`

## Definition Of Done

Une tache est terminee si:

1. Le code compile sans erreur.
2. Le comportement est valide fonctionnellement.
3. La securite n'est pas degradee (JWT, CORS, SQL parametre, emails verifies).
4. La documentation impactee est a jour.
5. Le parcours utilisateur principal reste operationnel:
   - inscription
   - verification email
   - connexion
   - jeu + score
   - invitation ami
