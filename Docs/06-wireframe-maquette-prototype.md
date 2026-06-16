<!-- EXPLICATION FICHIER: docs/06-wireframe-maquette-prototype.md - Document de reference pour le projet. -->
# Wireframe, maquette, prototype

## Wireframe ecran jeu (mobile first)

```mermaid
flowchart TB
  H[Header score niveau joker]
  G[Grille de tuiles]
  A[Actions: aide quiz pause]
  H --> G --> A
```

## Maquette fonctionnelle

- Header sticky avec score, niveau, bouton joker.
- Grille responsive 4 colonnes mobile, 5 tablette, 6 desktop.
- Carte quiz en bas de grille quand tuile ? activee.
- Navigation top vers podium, profil, legal.

## Prototype de parcours

```mermaid
flowchart TD
  S[Start] --> N1[Niveau 1]
  N1 --> Q[Tuile quiz]
  Q -->|Bonne reponse| J[Joker +]
  Q -->|Mauvaise reponse| P[Penalite score]
  J --> W[Fin niveau]
  P --> W
  W --> N2[Niveau suivant]
```
