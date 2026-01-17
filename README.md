# 🌾 Wheat Yield Prediction from Satellite Imagery

Predictive modeling of wheat crop yields using satellite-derived vegetation indices and harvester telemetry data. Built as part of my bachelor's thesis research.

## Overview

This project combines **[Sentinel-2](https://en.wikipedia.org/wiki/Sentinel-2) satellite imagery** with **ground-truth harvester data** to predict wheat yield at high spatial resolution. The pipeline processes raw geospatial data, computes vegetation indices, and evaluates multiple regression approaches.

## Key Features

- **Vegetation Index Computation** — [EVI](https://en.wikipedia.org/wiki/Enhanced_vegetation_index) and [NDVI](https://en.wikipedia.org/wiki/Normalized_difference_vegetation_index) derived from Sentinel-2 bands (B02, B04, B08)
- **Multi-variable Modeling** — Yield prediction using moisture, elevation, swath width, and distance features
- **Model Comparison** — Linear regression vs. bagged regression trees with cross-validation
- **Geospatial Processing** — QGIS-based interpolation, alignment, and clipping pipeline

## Project Structure

```
├── data/                  # Processed datasets at different quantile thresholds
├── models/
│   ├── lm/                # Linear regression (single & multiple)
│   └── rt/                # Regression trees (rpart & bagged)
├── preprocessing/         # Raw data → GeoTIFF → CSV pipeline
└── presentation/          # Visualization scripts
```

## Tech Stack

| Category | Tools |
|----------|-------|
| Language | R |
| Geospatial | `raster`, `sf`, `qgisprocess` |
| Modeling | `caret`, `rpart`, `ipred` |
| Data Wrangling | `tidyverse`, `rsample` |

## Methodology

1. **Data Acquisition** — Harvester telemetry (yield, moisture, elevation) + Sentinel-2 imagery
2. **Preprocessing** — Quantile-based filtering (2.5%, 5%, 7.5%, 10% outlier removal)
3. **Feature Engineering** — Compute EVI/NDVI, align rasters to 10m resolution
4. **Model Training** — 70/30 train-test split with 10-fold CV for tree models
5. **Evaluation** — R², MSE, RSE metrics across all dataset variants

## Data

Eight dataset variants combining:
- **Prefix**: `p_` (partial) / `f_` (full mask)
- **Quantile**: 2.5 / 5 / 7.5 / 10 (outlier threshold %)

Each record contains: `x`, `y`, `YIELD`, `MOIST`, `ELEV`, `DIST`, `SWAT`, `EVI`, `NDVI`
