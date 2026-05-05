# Data Dictionary

## ERS Major Land Uses Files

Prepared USDA ERS Major Land Uses files:

```text
outputs/ers_major_land_uses/ers_mlu_2012_48_states_wide.csv
outputs/ers_major_land_uses/ers_mlu_2012_48_state_totals_by_category.csv
outputs/ers_major_land_uses/ers_mlu_state_year_48_states_wide.csv
```

MLU columns:

| Column pattern | Meaning |
| --- | --- |
| `year` | ERS MLU inventory year. |
| `state_abbr` | Postal abbreviation. |
| `state_name` | State name. |
| `acres_<category>` | ERS acreage estimate for the state/category. |
| `blocks_250k_<category>` | `acres_<category> / 250000`. |
| `share_of_total_land_<category>` | Category acreage divided by state total land acreage. |

The `ers_mlu_2012_48_state_totals_by_category.csv` file has one row per ERS land-use category for the contiguous 48-state total.

MLU category slugs:

| Slug | ERS category |
| --- | --- |
| `total_land` | Total land |
| `total_cropland` | Total cropland |
| `cropland_used_for_crops` | Cropland used for crops |
| `cropland_used_for_pasture` | Cropland used for pasture |
| `cropland_idled` | Cropland idled |
| `grassland_pasture_range` | Grassland pasture and range |
| `forest_use_land` | Forest-use land (all) |
| `grazed_forest_use_land` | Grazed forest-use land |
| `ungrazed_forest_use_land` | Ungrazed forest-use land |
| `special_uses_land` | All special uses of land |
| `rural_transportation` | Land in rural transportation facilities |
| `rural_parks_wildlife` | Land in rural parks and wildlife areas |
| `defense_industrial` | Land in defense and industrial areas |
| `farmsteads_roads_misc_farmland` | Farmsteads, roads, and miscellaneous farmland |
| `urban_areas` | Land in urban areas |
| `miscellaneous_other_land` | Miscellaneous other land |

The ERS MLU files in this folder exclude Alaska, Hawaii, and DC.

## HISDAC Files

The primary CSVs are wide files with one row per state-year:

```text
outputs/csv/hisdac_state_landuse_all_years.csv
outputs/csv/hisdac_state_landuse_2020.csv
```

Method-specific wide files:

```text
outputs/csv/hisdac_majority_state_year.csv
outputs/csv/hisdac_counts_state_year.csv
```

## Identifiers

| Column | Meaning |
| --- | --- |
| `year` | HISDAC raster label year: 1940, 1945, ..., 2020. |
| `cumulative_through_year` | For count columns, the approximate final year included in that cumulative layer. Example: `1940` means cumulative through `1944`. |
| `state_fips` | Two-character state FIPS code. Use this for joins. |
| `state_abbr` | Postal abbreviation. |
| `state_name` | State or District of Columbia name. |
| `state_land_area_km2` | Census `ALAND` converted to square kilometers. |
| `rasterized_state_area_km2` | Area implied by rasterizing the 2020 state polygon to the HISDAC 250m grid. |

## Majority Columns

Majority columns describe the categorical majority-class raster.

| Column pattern | Meaning |
| --- | --- |
| `observed_majority_cell_count` | Nonzero majority cells in that state-year. |
| `observed_majority_area_km2` | `observed_majority_cell_count * 0.0625`. |
| `observed_majority_share_state_area` | Observed nonzero majority area divided by rasterized state area. |
| `majority_dominant_code` | Class code with the largest majority-cell area. |
| `majority_dominant_label` | Human-readable label for the dominant majority class. |
| `majority_dominant_slug` | Machine-friendly label for the dominant majority class. |
| `majority_dominant_cell_count` | Cell count for the dominant majority class. |
| `majority_dominant_area_km2` | Area of cells where the dominant class wins. |
| `majority_dominant_share_observed` | Dominant class share among nonzero majority cells. |
| `majority_dominant_share_state_area` | Dominant class share of rasterized state area. |
| `majority_cells_<class>` | Number of cells whose majority class is `<class>`. |
| `majority_area_km2_<class>` | Area of cells whose majority class is `<class>`. |
| `majority_share_observed_<class>` | Share among nonzero majority cells. |
| `majority_share_state_area_<class>` | Share of rasterized state area. |

Majority includes `no_classified_land_use_record` columns. These are coverage/no-record cells, not a land-use class.

## Count Columns

Count columns describe class-specific cumulative property-record rasters.

| Column pattern | Meaning |
| --- | --- |
| `total_property_record_count` | Sum of all class-count records in the state-year. |
| `counts_dominant_code` | Class code with the largest property-record count. |
| `counts_dominant_label` | Human-readable label for the dominant count class. |
| `counts_dominant_slug` | Machine-friendly label for the dominant count class. |
| `counts_dominant_record_count` | Record count for the dominant count class. |
| `counts_dominant_record_share` | Dominant class share of all property records in that state-year. |
| `counts_dominant_occupied_cell_count` | Number of cells with at least one record for the dominant count class. |
| `counts_dominant_occupied_area_km2` | Occupied-cell footprint for the dominant count class. |
| `record_count_<class>` | Property-record count for `<class>`. |
| `record_share_<class>` | Class share of all property records in that state-year. |
| `occupied_cells_<class>` | Number of cells with at least one record for `<class>`. |
| `occupied_area_km2_<class>` | `occupied_cells_<class> * 0.0625`. |
| `records_per_occupied_cell_<class>` | Average records per occupied cell for `<class>`. |

Count values are cumulative. Do not read `record_count_commercial` in 1980 as “new commercial records in 1980.”

## Class Slugs

| Theme | Code | Slug | Label |
| ---: | --- | --- | --- |
| 0 | `0` | `no_classified_land_use_record` | No classified land-use record |
| 1 | `A` | `agriculture` | Agriculture |
| 2 | `C` | `commercial` | Commercial |
| 3 | `I` | `industrial` | Industrial |
| 4 | `RC` | `recreational` | Recreational |
| 5 | `RI` | `residential_income` | Residential-Income |
| 6 | `RO` | `residential_owned` | Residential-Owned |
| 7 | `GV` | `governmental` | Governmental |
| 8 | `VL` | `vacant_land` | VacantLand |

## GIS Files

```text
outputs/gis/conus_states_2020_500k.geojson
outputs/gis/hisdac_state_landuse_2020.geojson
outputs/gis/hisdac_state_landuse_all_years.gpkg
```

The 2020 GeoJSON contains the same columns as `hisdac_state_landuse_2020.csv` plus geometry. The all-years GeoPackage repeats state geometry once per state-year and includes `year_date` for QGIS temporal mapping.
