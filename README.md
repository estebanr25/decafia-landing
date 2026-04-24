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
| ONNX inference | [onnxruntime-web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) (CDN) |
| Model weights | [HuggingFace — estebanr25/decafia](https://huggingface.co/estebanr25/decafia) |
| Fonts | Google Fonts — Playfair Display + Inter |
| Hosting | Netlify |

No build step. No framework. No npm. Open `index.html` in any browser.

## Model setup

The live demo section runs YOLOv8m ONNX inference entirely in the browser via
[onnxruntime-web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html).
The model file (`decafia_best.onnx`, ~25 MB) is **not committed to this repository**.

### Option A — HuggingFace CDN (default, no file needed)

`index.html` fetches the model directly from HuggingFace at runtime:

```
https://huggingface.co/estebanr25/decafia/resolve/main/decafia_best.onnx
```

This is the default `MODEL_URL` constant in the demo IIFE. No additional setup
is required; the model is downloaded on first use and is not cached between page
loads.

### Option B — self-hosted (faster first load, requires manual step)

If you prefer to serve the model from the same origin:

1. Download `decafia_best.onnx` from the HuggingFace repository:
   <https://huggingface.co/estebanr25/decafia>

2. Place the file at:
   ```
   assets/model/decafia_best.onnx
   ```
   (`assets/model/` is already in `.gitignore` — the binary will not be committed.)

3. In `index.html`, change the `MODEL_URL` constant in the demo IIFE to the local path:
   ```js
   var MODEL_URL = 'assets/model/decafia_best.onnx';
   ```

> **Netlify note:** The free tier's 100 MB deploy limit makes committing the model
> impractical. For production self-hosting, use
> [Netlify Large Media](https://docs.netlify.com/git/large-media/overview/) (Git LFS)
> or any external CDN, and update `MODEL_URL` accordingly.

### Required HTTP headers (WASM threads)

`onnxruntime-web` uses `SharedArrayBuffer` to enable multi-threaded WASM, which
requires the page to be served with these headers:

```
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
```

Both `netlify.toml` and `_headers` in this repo configure these for Netlify.
For local development with `python -m http.server` or `npx serve`, the headers
are absent and ORT automatically falls back to **single-threaded WASM** — inference
still works but runs ~2–4× slower.

> **COEP and cross-origin resources:** when `COEP: require-corp` is active,
> every cross-origin resource loaded by the page (CDN scripts, the HuggingFace
> model fetch) must respond with `Cross-Origin-Resource-Policy: cross-origin`.
> Both jsDelivr (ORT scripts) and the HuggingFace CDN serve this header, so the
> default configuration works out of the box.

## Local development

```bash
git clone https://github.com/estebanr25/decafia-landing.git
cd decafia-landing
```

Open directly in browser:

```bash
start index.html      # Windows
open index.html       # macOS
xdg-open index.html   # Linux
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
