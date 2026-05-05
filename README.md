# Small multiple exploration of how America's Land Changed

An interactive small multiples visualization – with customization panel – exploring how land use shifted across all 48 contiguous US states over 72 years. Built as a class exercise using USDA Economic Research Service Major Land Uses data.

The visualization tool allows you to track four major land-use categories — cropland, forest, grassland, and urban — plus parks & wildlife and defense land, as shares of each state's total land area from 1945 to 2017. The top 8 panels feature states with the most dramatic changes (sorted by your chosen metric), with short editorial annotations explaining what happened. The remaining 40 states appear in a compact grid below for comparison.

## Features

- **Multiple chart types**: Stacked area, line, stream, stacked bar, % change, sparkline for time-series views. Non-time-series views include the treemap and waffle chart options which show land-use composition for a single year
- **Sort by different stories**: Urban growth, forest decline, cropland decline, grassland decline, parks growth, defense land changes, or alphabetical — each with its own headline and annotations
- **"Other" breakdown**: Parks & Wildlife and Defense & Industrial shown as separate bands; additional sub-categories (transport, farmsteads, miscellaneous) available via checkboxes
- **Desaturation slider**: Grey out non-featured categories to make the sorted metric pop
- **Color schemes**: 11 presets including NYT, Bloomberg, FT, and Economist styles, plus individual color pickers
- **Year range zoom**: Slider to focus on any time window
- **Curve options**: Smooth, linear, step, basis, or cardinal interpolation
- **State mini-maps**: Tiny US outline with red dot showing each state's location
- **Export**: Download as SVG (text-editable), PNG, or JPG; export/import settings as JSON

## Data source

USDA Economic Research Service, Major Land Uses series (1945–2017). 48 contiguous states, 16 time points at roughly 5-year intervals. The CSV lives at `outputs/ers_major_land_uses/ers_mlu_state_year_48_states_wide.csv`.

See `outputs/DATA_DICTIONARY.md` for column definitions. See `README-original.md` and `README-instructor.md` for the full dataset documentation.

## Built with

- D3.js v7
- html2canvas (for PNG/JPG export)