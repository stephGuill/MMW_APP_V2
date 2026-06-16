<!-- EXPLICATION FICHIER: docs/03-sitemap-et-structure.md - Document de reference pour le projet. -->
# Sitemap et structure du site

## Sitemap

- /
- /play
- /leaderboard
- /auth
- /profile
- /faq
- /legal

## Diagramme de navigation

```mermaid
flowchart TD
  A[Accueil] --> B[Jouer]
  A --> C[Podium]
  A --> D[Connexion Inscription]
  A --> E[FAQ]
  A --> F[RGPD]
  D --> G[Profil]
  B --> C
```

## Structure technique

- frontend/
  - src/pages
  - src/components
  - src/services
  - src/data
- backend/
  - src/controllers
  - src/models
  - src/routes
  - src/middleware
  - sql/
