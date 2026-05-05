# Instructor Notes

This note is for deciding how to use the two datasets in class and how to frame the measurement choices.

## First Principle

The two datasets are not competing versions of the same measurement. They are designed for different questions.

**USDA ERS Major Land Uses (MLU)** is an acreage accounting dataset. It is organized around broad, reconciled categories intended to account for the land base.

**HISDAC-US** is a historical gridded property-record land-use dataset. It is organized around observed built/property records and land-use themes within a 250m grid.

## When To Use MLU

Use MLU when the question is about broad land allocation:

- How much land is cropland, pasture/range, forest, urban, special use, or miscellaneous?
- What share of a state’s land base falls into major land-use categories?
- How would we reproduce or critique a Bloomberg-style “How America Uses Its Land” graphic?
- How many 250,000-acre blocks would represent each category?

MLU is the appropriate base for the Bloomberg article because the article’s methodology says it used USDA ERS MLU acreage estimates, displayed per 250,000 acres.

What MLU gives:

- State acreage by category.
- Broad categories that reconcile overlapping sources.
- Long-run state estimates from 1945 to 2017.
- A coherent denominator: land acreage.

What MLU does not give:

- Exact within-state locations for each category.
- Pixel-level land cover.
- A modern 2020+ update for all categories in the prepared all-data CSV.
- The Bloomberg article’s additional custom subcategories without further sourcing.

Important caveat: the prepared MLU CSV uses the current ERS all-data file, which was revised after Bloomberg’s 2018 article. It is the correct source family, but some historical values may not exactly match Bloomberg’s original extraction.

## When To Use HISDAC

Use HISDAC when the question is about historical property-record land-use patterns:

- How did observed residential/commercial/industrial/etc. property records change from 1940 to 2020?
- Where do majority-class and count-based interpretations disagree?
- How does a spatial footprint measure differ from a record-intensity measure?
- How does coverage change over time?
- How do property-record-derived land-use patterns differ from broad acreage accounting?

What HISDAC gives:

- 250m gridded historical land-use rasters.
- Five-year steps from 1940 to 2020.
- Majority land-use class by cell.
- Property-record counts by class.
- State aggregation, plus GIS outputs for mapping.

What HISDAC does not give:

- A complete accounting of every acre of land.
- USDA categories like forest-use land, grassland pasture/range, rural highways, parks, defense land, wetlands/desert, or miscellaneous land.
- Exact acreage by property use from the count rasters.
- Parcel-level area.
- A direct reproduction of Bloomberg’s land-use graphic.

## Majority Versus Counts In HISDAC

HISDAC majority:

- A 250m cell gets one class: the most frequent class in that cell.
- Area-like fields are cell-footprint area: `cell_count * 0.0625 km2`.
- Good for visualizing dominant spatial footprint.
- Can hide mixed-use or high-intensity minority classes.

HISDAC counts:

- Rasters store property-record counts by class.
- Good for intensity/composition questions.
- Count totals are not area.
- Occupied-cell area can be computed, but classes can overlap spatially.

Important distinction:

- `majority_area_km2_commercial` means area of cells where commercial is dominant.
- `occupied_area_km2_commercial` means area of cells with at least one commercial record.
- `record_count_commercial` means number of commercial property records.

None of those is exact commercial land acreage.

## Boundary Notes

For HISDAC, the aggregation uses constant 2020 Census state boundaries for all years. This is a harmonization choice. It is reasonable for a state-level CONUS classroom exercise, but it is not historical boundary reconstruction.

Included in HISDAC aggregation:

- 48 conterminous states plus District of Columbia.

Excluded from HISDAC aggregation:

- Alaska, Hawaii, Puerto Rico, Virgin Islands, Guam, Northern Mariana Islands, American Samoa.

The MLU 48-state Bloomberg-base outputs exclude Alaska, Hawaii, and DC.

## Bloomberg-Specific Notes

The Bloomberg article combines several steps:

1. Start with USDA ERS MLU acreage estimates by state.
2. Convert acreage to visible units, with each square representing 250,000 acres.
3. Use NLCD and other sources to locate categories approximately within states.
4. Add additional custom subdivisions from other sources, such as livestock groups, parks, airports, golf, large landowners, and Weyerhaeuser.

The prepared MLU files cover step 1 and the 250,000-acre unit calculation for step 2. They do not reproduce the full Bloomberg placement or all custom subcategories.

## Suggested Student Questions

For MLU:

- Which broad category occupies the largest share of the contiguous U.S.?
- How do state-level shares differ from national shares?
- What changes if students visualize acres versus percentages?
- How does a 250,000-acre unit affect the visual hierarchy?
- How much of the Bloomberg graphic is data accounting, and how much is editorial placement?

For HISDAC:

- Which states have high observed HISDAC coverage by 2020?
- Where do majority and count dominant classes differ?
- What does “residential-owned dominates by record count” mean compared with “residential-owned dominates by cell area”?
- Which states show increasing commercial or industrial record shares over time?
- What gets lost when a cell has only one majority class?

Cross-dataset:

- Why can two land-use datasets both be valid and still answer different questions?
- What is the denominator in each dataset?
- Are categories mutually exclusive?
- Is the unit acreage, grid cells, occupied grid cells, or property records?
- Does the dataset locate land use spatially, summarize it statistically, or both?

## Common Pitfalls

- Treating HISDAC record counts as acreage.
- Treating HISDAC majority-cell footprint as exact land-use acreage.
- Assuming MLU has precise within-state spatial placement.
- Summing HISDAC occupied-cell areas across classes as if they are mutually exclusive.
- Ignoring `No classified land-use record` in HISDAC early years.
- Comparing year-to-year wiggles in MLU without checking methodology notes.
- Assuming Bloomberg’s custom labels are all directly present in MLU.

## Teaching Framing

A useful way to put it:

> MLU is for “How is the land base allocated?” HISDAC is for “What property-record land-use patterns are observed on a historical grid?”

Neither dataset is generally better. Each becomes good or bad depending on the claim a student wants to make.

