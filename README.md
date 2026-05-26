# China Building Function Atlas — Interactive Map

An interactive web visualization of the nationwide, building-resolved functional atlas for China developed
in *Building-scale functional mixing reveals a decarbonization window in cities* (Li, Zhang, Huang et al.).
Each of ~200 million buildings carries a two-tier functional label, and this page lets you explore the
atlas from country scale down to individual building footprints — and now also inspect a manual validation
of the model against 1,981 human-checked samples.

**Live demo:** https://zhzhyd.github.io/china-mixed-use-building-map/

---

## What you see

The page is split into two mutually exclusive panes, switched with the **Part A / Part B** toggle below
the section heading.

### Part A — Building function atlas

- **BFMI grid** (z 6.5–11) — building functional mixing index, already normalised to `[0, 1]`. Coloured
  with a viridis ramp at 0.0 / 0.14 / 0.43 / 0.72 / 1.0; the 0.14 and 0.72 stops mark the synergy window
  identified in the paper.
- **Individual buildings** (z 12–14, z 13 is the deepest real tile; z 13–14 is overzoomed). Coloured by:
  - **BF1 — contextual label**: the dominant land-use setting of the surrounding district
    (Residential, Commercial, Industrial, Public open space, Education, Transport, Administrative, Medical).
  - **BF2 — intrinsic label**: the building's own dominant function.
  - The render-mode selector flips between **BF1 alone** and the **joint 29-class BF1×BF2 combination**
    (Supplementary Table S1).
- Building vectors and outlines can be toggled on/off; the same toggles control the BFMI grid.
- **Locator overview** of China showing the current viewport — click it to pan the main map there.

### Part B — Manual accuracy validation

- **Validation map** of 1,981 manually-checked building samples (BF1ᵥ / BF2ᵥ).
  - Points are coloured by the human label; the **render-mode selector synchronises both points and
    provinces** between 8-class (BF1) and 29-class (BF1×BF2) views.
  - Province polygons are tinted by the per-province Overall Accuracy on a 0.65 / 0.78 / 0.92 ramp.
  - Click a point to see the four labels (BF1, BF2, BF1ᵥ, BF2ᵥ); click a province for OA, Cohen's
    Kappa, macro Precision/Recall/F1 and sample count.
- **Headline cards** above the map: Contextual OA (BF1) 87.99%, Joint OA (BF1×BF2) 83.34%, sample count.
- **Evaluation analytics** below the map — second mutex toggle between BF1 (8-class) and BF1×BF2
  (29-class). Each pane shows:
  1. Per-class accuracy bar chart (Precision / Recall / F1-score / Kappa, default all on).
  2. Confusion matrix as a row-normalised heatmap (counts on hover).
  3. Province-level accuracy bar chart with the same metric set plus Overall Accuracy.

### Basemaps

- **Esri Dark** (default) and **Google Satellite**, switchable via the toggle in the top-right of each
  map.

---

## Data

All vector tiles are hosted on the project's own server at
`https://www.nolimitopia.com/cbmf_pmtiles/`:

| File | Zoom | Purpose |
|---|---|---|
| `china_bfmi_grid_z6_z11.pmtiles` | 6–11 | BFMI grid (Part A coarse view) |
| `china_buildings_z11_z13.pmtiles` | 11–13 | Individual buildings (Part A close-up) |
| `validation_points_z3_z13_nodrop.pmtiles` | 3–13 | Manually-checked validation points (Part B) |
| `china_provinces_validation_z3_z13.pmtiles` | 3–13 | Province polygons with baked-in 8-class and 29-class metrics |

## Tech

- Single static page — no build system, no bundler.
- [MapLibre GL JS](https://maplibre.org/) 3.6 for rendering.
- [PMTiles](https://github.com/protomaps/PMTiles) 3.0 for serverless vector tiles via HTTP range requests.
- All charts are plain hand-rolled SVG with a small `renderBarChart` helper (`fitWidth` mode + a
  `ResizeObserver` per chart for responsive widths).
- Mobile breakpoints at 768 px and 480 px shrink panels, stack the metric cards, and let dense charts
  scroll horizontally where the categories cannot legibly fit.

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
