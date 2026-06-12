# Programmeren & OOP — Docusaurus

Cursussite voor het graduaat Programmeren aan AP Hogeschool.

## Vereisten

- Node.js >= 20
- npm >= 9

## Lokaal starten

```bash
npm install
npm start
```

De site opent op http://localhost:3000.

## Bouwen

```bash
npm run build
npm run serve
```

## Structuur

```
docs/                cursusinhoud (168 markdown bestanden)
static/img/          afbeeldingen
sidebars.js          navigatiestructuur
docusaurus.config.js siteconfiguratie
```

## Deploy

Elke push naar `main` deployt automatisch via GitHub Actions naar GitHub Pages.
