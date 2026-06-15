# TrueScale — Online Ruler

A browser-based, calibrated on-screen ruler that measures real physical objects in **centimetres and inches**. Fully client-side, no backend, works offline.

Calibrate once with any credit/ID card (ISO/IEC 7810 ID-1, 85.60 mm) and the on-screen scale maps to true physical units. Drag the two caliper jaws to measure.

## Features
- Reference-card calibration (long or short edge) + direct PPI entry, persisted in `localStorage`
- Physically-accurate SVG ruler in cm (1/5/10 mm) and inches (1/16″ hierarchy)
- Two draggable caliper markers with live readout; full keyboard + screen-reader support
- Installable PWA — works fully offline after first load
- Zero dependencies, no build step

## Run locally
```bash
node serve.js   # http://localhost:8080  (dev only — needed for the service worker)
```
Or just open `index.html` directly (offline/PWA features need the served origin).

## Deploy
Static site — host the folder on any static host. See [DEPLOY.md](DEPLOY.md) for the domain + AdSense find-and-replace steps.

Built from the TrueScale v1.0 technical specification.
