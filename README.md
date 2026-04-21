# DECAFIA Landing — Coffee Leaf Disease Detection

> Research project landing page for **DECAFIA**, a YOLOv8-based coffee leaf disease detection system developed at Universidad Industrial de Santander (UIS), Colombia.

**🌱 Live site:** https://decaf-ia.netlify.app
**📄 Research paper:** submitted to *Sensors* (MDPI) — link to be added upon publication
**🔬 Main research repo:** [estebanr25/decafia](https://github.com/estebanr25/decafia)
**📸 Webcam demo source:** [estebanr25/decafia-webcam](https://github.com/estebanr25/decafia-webcam)

[![Netlify Status](https://api.netlify.com/api/v1/badges/8f1427c5-41ed-45f1-942c-9148f4694fa3/deploy-status)](https://app.netlify.com/projects/decaf-ia/deploys)
![License](https://img.shields.io/badge/license-MIT-blue)
![HTML](https://img.shields.io/badge/built_with-vanilla_HTML%2FCSS%2FJS-orange)
![Chart.js](https://img.shields.io/badge/Chart.js-4-ff6384)
![Leaflet](https://img.shields.io/badge/Leaflet-1.9-199900)

---

## About

DECAFIA detects three coffee leaf conditions — coffee rust (*Hemileia vastatrix*), weevil defoliation (*Compsus* sp. / *Epicaerus* sp., Curculionidae), and leaf miner (*Leucoptera coffeella*) — using a YOLOv8m model trained on 2,786 field images collected at a *Coffea arabica* plantation in El Socorro, Santander, Colombia.

The model achieves **mAP50 = 92.4%** and **mAP50-95 = 76.6%** on the held-out test set, and is deployed as a WhatsApp chatbot (live in production) plus a companion Android application for offline inference.

This repository contains the **project landing page** — a bilingual (ES/EN), accessible, single-file HTML site presenting the research, methodology, results, and deployment architecture.

## Features

- **Bilingual content** — full Spanish/English toggle with localStorage persistence
- **Dark mode** — manual toggle + `prefers-color-scheme` support
- **Interactive metrics dashboard** — 5 tabs (Overall metrics / Per-class AP / Confusion matrix / PR curves / Training dynamics) powered by Chart.js
- **Live WhatsApp bot integration** — direct CTAs to the production bot
- **Leaflet map** — dataset collection site in El Socorro, Santander
- **Scientific rigor** — cited methodology, reproducible metrics, BibTeX export
- **WCAG 2.1 AA accessibility** — semantic HTML, keyboard navigation, focus rings, `prefers-reduced-motion` support
- **JSON-LD structured data** — `ScholarlyArticle` + `SoftwareApplication` schemas for SEO

## Tech stack

| Layer | Technology |
|---|---|
| Markup | Vanilla HTML5 (single file) |
| Styles | Vanilla CSS with custom properties |
| Interactivity | Vanilla JavaScript (IIFE-organized) |
| Charts | [Chart.js 4](https://www.chartjs.org/) (CDN) |
| Maps | [Leaflet 1.9](https://leafletjs.com/) (CDN) |
| Fonts | Google Fonts — Playfair Display + Inter |
| Hosting | Netlify |

No build step. No framework. No npm. Open `decafia_landing_v6.html` in any browser.

## Local development

```bash
git clone https://github.com/estebanr25/decafia-landing.git
cd decafia-landing
```

Open directly in browser:

```bash
start decafia_landing_v6.html      # Windows
open decafia_landing_v6.html       # macOS
xdg-open decafia_landing_v6.html   # Linux
```

For live-reload during development, any static server works:

```bash
npx serve .
# or:
python -m http.server 8000
```

## Deployment

The site is deployed on **Netlify** with automatic redeployment on every push to `main`.

## Research team

- **Luis Esteban Rosas Ruiz** — Author ([@estebanr25](https://github.com/estebanr25))
- **Andrey Fernando Salom Medina** — Co-author
- **Prof. Jaime Guillermo Barrero Pérez** — Director

*Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones*
*Universidad Industrial de Santander · Bucaramanga, Colombia*

## Citation

If you reference DECAFIA in academic work, please cite the paper (BibTeX block on the site). The website itself may be referenced as:

```bibtex
@misc{rosas2025decafialanding,
  author = {Rosas Ruiz, Luis Esteban},
  title  = {DECAFIA: Coffee Leaf Disease Detection --- Project Website},
  year   = {2025},
  url    = {https://decaf-ia.netlify.app}
}
```

## License

MIT License — see [LICENSE](./LICENSE).

The underlying research and trained model weights are governed separately by the main [decafia repo](https://github.com/estebanr25/decafia).
