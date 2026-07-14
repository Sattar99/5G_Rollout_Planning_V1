# 5G Rollout Planning (Cork, Ireland)

A geospatial optimization system for planning 5G telecom tower placement across Cork, Ireland — built as part of an MSc thesis (DATA9003) at Munster Technological University.

The system combines population density, elevation, existing infrastructure, and land-use data to recommend tower locations that maximise coverage while minimising redundancy with existing sites.

## What it does

- Cleans and processes population density data (WorldPop 1km grid) and existing tower locations for the Cork region
- Uses **HDBSCAN** clustering to identify high-density population clusters that need coverage
- Applies a **Random Forest** model to help prioritise candidate sites based on terrain and demand features
- Evaluates candidate sites against elevation (via the `elevation`/`rasterio` pipeline) and land-use constraints (via `osmnx`/`geopandas`)
- Produces an interactive **Folium** map (`tower_placement_map.html`) visualising optimal vs. existing tower placement
- Compares a pure HDBSCAN approach against a hybrid HDBSCAN + greedy optimisation strategy (see the multiple `*_towers.csv` outputs)

## Tech stack

- **Language:** Python (Jupyter Notebooks)
- **Geospatial:** `geopandas`, `shapely`, `pyproj`, `rasterio`, `osmnx`, `fiona`, `folium`
- **Clustering / ML:** `hdbscan`, `scikit-learn` (Random Forest)
- **Optimisation:** `pulp`
- **Elevation:** `elevation`, `owslib` (WCS)

## Project structure

```
5G_Rollout_Planning_V1/
├── 5G_Tower_Placement.ipynb        # Main analysis: preprocessing, clustering, modelling
├── Cork5G_Planning_Cork.ipynb      # Cork-specific planning notebook
├── DATA9003_R00259436_Thesis.pdf   # Full thesis write-up
├── Datasets/
│   ├── Ireland_pop/                # WorldPop population density data
│   ├── Existing_Tower/             # Existing tower location data
│   └── LandUse/                    # Land-use constraint data
├── tower_placement_map.html        # Interactive Folium output map
└── *.csv                           # Candidate/optimal tower location outputs
```

## Getting started

```bash
pip install -q geopandas shapely pyproj rasterio folium hdbscan pulp osmnx fiona tqdm scikit-learn
jupyter notebook 5G_Tower_Placement.ipynb
```

> Note: some geospatial dependencies (e.g. `rasterio`, `fiona`, `osmnx`) may require system-level GDAL libraries. See each package's install docs if you hit build errors.

## Output

Open `tower_placement_map.html` in a browser for an interactive view of proposed vs. existing tower placements.

## Background

This project underpins the thesis *"5G Rollout Planning"* (DATA9003), which applies unsupervised clustering and geospatial ML to telecom infrastructure planning. Full methodology and results are documented in `DATA9003_R00259436_Thesis.pdf`.

## License

See [LICENSE](./LICENSE).
