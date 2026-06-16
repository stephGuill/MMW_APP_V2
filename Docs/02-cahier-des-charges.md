<!-- EXPLICATION FICHIER: docs/02-cahier-des-charges.md - Document de reference pour le projet. -->
# Cahier des charges (MVP)

## Objectifs

- Proposer un jeu type Mahjong revisite avec tuiles quiz dev.
- Permettre le jeu connecte (classement) et hors connexion (mode invite).
- Assurer conformite RGPD et pages d'information legales.

## Fonctionnalites

- Partie Mahjong simplifiee par paires.
- Tuiles quiz: bonne reponse => joker double paire.
- Systeme de niveaux et score.
- Authentification: inscription, connexion, token JWT.
- Podium global et profil utilisateur.
- FAQ et RGPD.

## Exigences techniques

- Frontend: React + Tailwind + React Router.
- Backend: Express, architecture MVC, JWT, CRUD questions.
- Base de donnees: PostgreSQL.
- Securite: bcrypt, helmet, rate-limit, validation minimale.
- Deploiement: Docker, Render ou AlwaysData.

## Criteres d'acceptation

- Application utilisable sur mobile, tablette, desktop.
- API securisee et fonctionnelle.
- CRUD question operationnel (admin requis).
- Score local fonctionnel sans connexion.
