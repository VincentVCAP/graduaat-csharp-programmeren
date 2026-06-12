# Programmeren & OOP — Docusaurus

Gegenereerd vanuit de originele GitBook op `c:\TEMP\CourseOOP`.

## Vereisten

- **Node.js >= 16.14** (jouw huidige versie is 14 — update via https://nodejs.org of via nvm)
- npm >= 8

## Starten

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
docs/                   ← alle cursusinhoud (168 markdown bestanden)
static/img/             ← alle afbeeldingen (285 bestanden)
sidebars.js             ← navigatiestructuur
docusaurus.config.js    ← site configuratie
```

## Noten

- GitBook `{% hint %}` blokken zijn omgezet naar Docusaurus admonitions (`:::info`, `:::warning`, etc.)
- Afbeeldingspaden zijn omgezet van `../../assets/` naar `/img/`
- `README.md` bestanden zijn hernoemd naar `index.md`
- De map `DEPRECATED/` is niet meegenomen
