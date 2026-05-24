# China Building Function Atlas — Interactive Map

An interactive web visualization of the nationwide, building-resolved functional atlas for China developed
in *Building-scale functional mixing reveals a decarbonization window in cities* (Li, Zhang, Huang et al.).
Each of ~200 million buildings carries a two-tier functional label, and this page lets you explore the
atlas from country scale down to individual building footprints.

**Live demo:** https://zhzhyd.github.io/china-mixed-use-building-map/

---

## What you see

- **BF1 — contextual label**: the dominant land-use setting of the surrounding district
  (Residential, Commercial, Industrial, Public open space, Education, Transport, Administrative, Medical).
- **BF2 — intrinsic label**: the building's own dominant function.
- **Two render modes:** color by BF1 alone, or by the **joint 29-class BF1–BF2 combination** that drives
  the analysis in the paper (Supplementary Table S1).
- **Two zoom regimes:**
  - z 6.5–11 — aggregated 2 km grid
  - z 12–14 — individual building footprints (z 13 is the deepest real tile; z 13–14 is overzoomed)
- **Locator overview** showing the current viewport on a fixed China-wide map; click anywhere on it to
  pan the main map there at the current zoom.
- **Two basemaps** — Esri World Dark Gray Canvas (default) and Google high-resolution satellite imagery,
  switchable via the toggle in the top-right of the map.
- Building vectors and outlines can be toggled on/off independently.

## Tech

- Single static page — no build system, no bundler.
- [MapLibre GL JS](https://maplibre.org/) 3.6 for rendering.
- [PMTiles](https://github.com/protomaps/PMTiles) 3.0 for serverless vector tiles via HTTP range requests.
- Vector data hosted as PMTiles archives:
  - `china_agg_grid_z0_z11_nodrop.pmtiles` — aggregated grid (z 0–11)
  - `china_buildings_z11_z13.pmtiles` — individual buildings (z 11–13)

## Running locally

Open `index.html` directly in a browser, or serve the folder over HTTP:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

PMTiles range requests work over the page's HTTPS origin; opening via `file://` also works because the
data is fetched over HTTPS, not from disk.

## Deployment

The page is deployed via **GitHub Pages** from the `main` branch root. Any push to `main` triggers a
fresh deploy.

## Citation

If you use this visualization or the underlying atlas, please cite the manuscript:

> Li, J., Zhang, Z., Huang, X., Pan, X., Ma, S., Xiong, X., & Zhang, L. *Building-scale functional
> mixing reveals a decarbonization window in cities.*

## Attribution

- Esri World Dark Gray Canvas © Esri
- Satellite imagery © Google
- PMTiles tooling © Protomaps contributors
