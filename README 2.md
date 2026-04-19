# SkinIQ

> Dermatological intelligence for every skin tone.

**Live site:** [YOUR_USERNAME.github.io/SkinIQ](https://YOUR_USERNAME.github.io/SkinIQ)

---

## What it does

SkinIQ is a clinical-grade skincare intelligence platform built on a trained PyTorch ResNet-18 model. It combines a 25-condition dermatology database, a 64-product catalog, a 112-ingredient analyzer, a Fitzpatrick-calibrated skin analyzer, and an interactive world skin-tone map — all in a single privacy-first web app.

| Tool | What it does |
|------|-------------|
| **Conditions** | 25 conditions with Fitzpatrick I–VI presentation notes, treatment ladders, and illustrated cross-sections |
| **Products** | 64+ products across 40+ brands — full INCI transparency, SkinIQ ingredient scores, filters by skin type |
| **Ingredients** | 112-ingredient database — A–F ratings, comedogenicity 0–5, irritancy 1–5, conflict warnings, barcode scanner |
| **Skin Analyzer** | Camera or upload → Fitzpatrick ITA estimate + ResNet-18 classifier (demo mode or live Flask backend) |
| **Skin Tones** | Fitzpatrick I–VI cards + interactive SVG world map with cursor-hover tooltips |

---

## Tech stack

- **Frontend** — React 18, Vite, Tailwind CSS, lucide-react
- **Backend (optional)** — Flask, PyTorch ResNet-18
- **Fonts** — Playfair Display, Inter, JetBrains Mono
- **Hosted** — GitHub Pages (static frontend)

---

## Running locally

```bash
# Frontend
cd skiniq-frontend
npm install
npm run dev
# → http://localhost:3000 (use Google Chrome)
```

```bash
# Backend (optional — for real ML predictions)
cd skiniq-backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp /path/to/model.pth .
python app.py
# → http://127.0.0.1:5000
```

Once both are running, go to **Analyzer → Connect backend** in the app and click **Ping backend** to verify the connection.

---

## Repository structure

```
SkinIQ/
├── docs/                  ← GitHub Pages serves this folder
│   ├── index.html
│   ├── _headers           ← Netlify security headers (ignored by GitHub Pages)
│   ├── _redirects         ← Netlify SPA routing (ignored by GitHub Pages)
│   └── assets/
│       ├── index-*.js
│       └── index-*.css
├── skiniq-frontend/       ← React source (optional, for development)
│   ├── src/
│   │   ├── App.jsx        ← Full application (~7000 lines)
│   │   ├── main.jsx
│   │   └── index.css
│   ├── package.json
│   ├── vite.config.js
│   └── tailwind.config.js
├── skiniq-backend/        ← Flask inference server (optional)
│   ├── app.py
│   ├── requirements.txt
│   └── README.md
├── README.md
├── .gitignore
└── SECURITY.md
```

> **Note:** `model.pth` weights (~110MB) are excluded from the repo. See `skiniq-backend/README.md` for setup instructions.

---

## Connecting the ML backend

The frontend works fully without the backend — the Skin Analyzer falls back to demo mode (browser-based feature extraction, clearly labeled). To use real ResNet-18 predictions:

1. Start the Flask server: `python skiniq-backend/app.py`
2. In the app, go to **Analyzer → Connect backend**
3. Leave the URL as `http://127.0.0.1:5000/diagnose`
4. Click **Ping backend** → should show ✓ Reachable
5. Upload or capture a photo and analyze

---

## Browser requirements

| Feature | Chrome | Firefox | Safari |
|---------|--------|---------|--------|
| Full app | ✅ | ✅ | ✅ |
| Camera capture | ✅ | ✅ | ✅ |
| Barcode scanner | ✅ | ❌ | ❌ |

Use **Google Chrome** for the full experience including barcode scanning.

---

## Deploying updates

```bash
# Build a new dist
cd skiniq-frontend
npm run build

# Copy into docs/
rm -rf ../docs/*
cp -r dist/* ../docs/

# Push to GitHub Pages
cd ..
git add docs/
git commit -m "Deploy: describe your changes"
git push origin main
```

GitHub Pages updates within ~1 minute.

---

## Disclaimer

SkinIQ is **educational only**. It is not a medical device, is not FDA-cleared, and does not replace a board-certified dermatologist. All outputs are probabilistic suggestions.

---

## Credit

Built by **Aditya Kondur** — powered by PyTorch ResNet-18.

Data sources: [Fitzpatrick17k](https://github.com/mattgroh/fitzpatrick17k), [DDI](https://ddi-dataset.github.io/), [ISIC Archive](https://www.isic-archive.com/), [DermNet NZ](https://dermnetnz.org/), [Open Beauty Facts](https://world.openbeautyfacts.org/).
