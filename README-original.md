# Land-Use Datasets

This folder contains two land-use datasets prepared as CSVs, plus supporting GIS files and reproducible processing scripts. They come from different sources and measure different things, so choosing between them requires reading the source documentation and deciding which measurement fits the question.

## Contents

```text
outputs/ers_major_land_uses/    USDA ERS Major Land Uses acreage outputs
outputs/csv/                    HISDAC-US state-year CSV outputs
outputs/gis/                    HISDAC-US GIS outputs
outputs/bundles/                Zip file for sharing
outputs/DATA_DICTIONARY.md      Column definitions
outputs/metadata/manifest.json  HISDAC processing manifest
outputs/ers_major_land_uses/manifest.json  ERS MLU processing manifest
scripts/                        Reproducible processing scripts
data/raw_mlu/                   Downloaded USDA ERS source files
data/raw/                       Downloaded HISDAC and Census source files
data/extracted/                 Extracted HISDAC rasters
```

## Dataset 1: USDA ERS Major Land Uses

The USDA Economic Research Service Major Land Uses data product provides state-level acreage estimates for broad land-use categories. The prepared files here focus on the 48 contiguous states.

Prepared outputs:

```text
outputs/ers_major_land_uses/ers_mlu_2012_48_states_wide.csv
outputs/ers_major_land_uses/ers_mlu_2012_48_state_totals_by_category.csv
outputs/ers_major_land_uses/ers_mlu_state_year_48_states_wide.csv
outputs/ers_major_land_uses/manifest.json
```

Columns include:

- `acres_*`: acreage estimates by land-use category.
- `blocks_250k_*`: acreage divided by 250,000.
- `share_of_total_land_*`: category share of state total land.

The all-years MLU file covers ERS inventory years from 1945 through 2017. The 2012 files are included because Bloomberg’s “Here’s How America Uses Its Land” article described using USDA ERS MLU 2012 acreage estimates.

Source files:

```text
data/raw_mlu/major_land_uses_all_data_1945_2017.csv
data/raw_mlu/EIB-178.zip
```

Source links:

- USDA ERS Major Land Uses: <https://www.ers.usda.gov/data-products/major-land-uses/>
- USDA ERS Major Uses of Land in the United States, 2012: <https://www.ers.usda.gov/publications/pub-details?pubid=84879>

Rebuild:

```bash
.venv/bin/python scripts/build_ers_major_land_uses.py
```

## Dataset 2: HISDAC-US Land Use

HISDAC-US Version II provides gridded historical land-use rasters derived from property/building records. The prepared files aggregate those rasters to states.

Prepared CSV outputs:

```text
outputs/csv/hisdac_state_landuse_all_years.csv
outputs/csv/hisdac_state_landuse_2020.csv
outputs/csv/hisdac_majority_state_year.csv
outputs/csv/hisdac_counts_state_year.csv
```

Prepared GIS outputs:

```text
outputs/gis/conus_states_2020_500k.geojson
outputs/gis/hisdac_state_landuse_2020.geojson
outputs/gis/hisdac_state_landuse_all_years.gpkg
```

The HISDAC outputs include two source representations:

- **Majority class**: each 250m grid cell stores the most frequent land-use class in that cell.
- **Class counts**: each 250m grid cell stores property-record counts by land-use class.

HISDAC years run from 1940 through 2020 in five-year steps.

Source files:

```text
data/raw/Majority.tar
data/raw/Count.tar
data/raw/state_boundaries_2020_500k.zip
```

Source links:

- HISDAC-US Dataverse: <https://dataverse.harvard.edu/dataverse/hisdacus>
- Historical Land Use for the U.S. 1940-2020: Major Class Version II: <https://doi.org/10.7910/DVN/CHLNQG>
- Historical Land Use for the U.S. 1940-2020: Class Counts Version II: <https://doi.org/10.7910/DVN/PRJBUF>
- Related paper: <https://doi.org/10.1038/s41597-024-03081-x>
- Census 2020 cartographic state boundaries: <https://www2.census.gov/geo/tiger/GENZ2020/shp/cb_2020_us_state_500k.zip>

Rebuild:

```bash
.venv/bin/python scripts/aggregate_hisdac_state_landuse.py
```

## Bundle

```text
outputs/bundles/land_use_datasets.zip
```

`land_use_datasets.zip` contains the neutral documentation, prepared outputs, source files, and processing scripts. It does not include `README-instructor.md`.

## Data Dictionary

See [outputs/DATA_DICTIONARY.md](outputs/DATA_DICTIONARY.md) for column definitions.
