# Cleaning the shorebird survey data 


## The data set

ARCTIC SHOREBIRD DEMOGRAPHICS NETWORK [https://doi.org/10.18739/A2222R68W](https://doi.org/10.18739/A2222R68W)

Data set hosted by the [NSF Arctic Data Center](https://arcticdata.io) data repository 

Field data on shorebird ecology and environmental conditions were collected from 1993-2014 at 16 field sites in Alaska, Canada, and Russia.

![Shorebird, copyright NYT](https://static01.nyt.com/images/2017/09/10/nyregion/10NATURE1/10NATURE1-superJumbo.jpg?quality=75&auto=webp)

Data were not collected every year at all sites. Studies of the population ecology of these birds included nest-monitoring to determine the timing of reproduction and reproductive success; live capture of birds to collect blood samples, feathers, and fecal samples for investigations of population structure and pathogens; banding of birds to determine annual survival rates; resighting of color-banded birds to determine space use and site fidelity; and use of light-sensitive geolocators to investigate migratory movements. 

Data on climatic conditions, prey abundance, and predators were also collected. Environmental data included weather stations that recorded daily climatic conditions, surveys of seasonal snowmelt, weekly sampling of terrestrial and aquatic invertebrates that are prey of shorebirds, live trapping of small mammals (alternate prey for shorebird predators), and daily counts of potential predators (jaegers, falcons, foxes). Detailed field methods for each year are available in the `ASDN_protocol_201X.pdf` files. All research was conducted under permits from relevant federal, state, and university authorities.

See `01_ASDN_Readme.txt` provided in the [course data repository](https://github.com/UCSB-Library-Research-Data-Services/bren-meds213-spring-2024-class-data) for full metadata information about this data set.

## DATA & FILE OVERVIEW

### File List

#### `data/processed/`
- `all_cover_fixed_OVERBYE.csv`: Cleaned dataset of snow, water, and land cover observations. Created in `eds213_data_cleaning_assign.qmd`
- `species_presence.csv`: Cleaned long-format bird species presence/absence dataset from daily counts

#### `data/raw/`
- `ASDN_Snow_survey.csv`: Raw snow/land/water cover percentages with some inconsistent values
- `ASDN_Daily_species.csv`: Wide-format species observation counts
- `01_ASDN_Readme.txt`: Metadata and documentation for ASDN source data

#### `docs/`
- `data-cleaning.html`: Rendered HTML output showing processing and code execution

#### Project root:
- `data_cleaning.qmd`: Primary script that cleaned snow and species data
- `eds213_data_cleaning_assign.qmd`: Targeted cleaning of `Water_cover`, `Land_cover`, and integrity checks
- `README.md`: This file

---

### Relationship Between Files
- `ASDN_Snow_survey.csv`: cleaned using `data_cleaning.qmd` and further validated in `eds213_data_cleaning_assign.qmd` to create `all_cover_fixed_OVERBYE.csv`
- `ASDN_Daily_species.csv`: reshaped using `pivot_longer()` to create `species_presence.csv`

---

## DATA-SPECIFIC INFORMATION  
**File:** `data/processed/all_cover_fixed_OVERBYE.csv`

### Number of Variables  
11

### Number of Rows  
42,830

### Variable Descriptions

| Variable       | Description                                                   | Unit/Format     |
|----------------|---------------------------------------------------------------|-----------------|
| `Site`         | 4-letter ASDN field site code                                 | e.g., `eaba`, `klgo` |
| `Year`         | Year of observation                                           | YYYY            |
| `Date`         | Date of survey                                                | Date (YYYY-MM-DD) |
| `Plot`         | Plot ID within site                                           | String          |
| `Location`     | Sub-location within the plot                                  | String          |
| `Snow_cover`   | % area covered by snow/slush                                  | Numeric (0–100) |
| `Water_cover`  | % area covered by standing water                              | Numeric (0–100) |
| `Land_cover`   | % area with exposed land                                      | Numeric (0–100) |
| `Total_cover`  | Sum of the three cover types                                  | Should equal 100 |
| `Observer`     | Observer initials or first name in multi-observer fields      | Cleaned String  |
| `Notes`        | Field notes                                                   | Text            |

---

### Missing Data Codes

| Code        | Meaning                                |
|-------------|----------------------------------------|
| `NA`        | Missing/invalid value                  |
| `.`         | Re-coded to NA                         |
| `-`         | Re-coded to NA                         |
| `n/a`       | Re-coded to NA                         |
| `unk`       | Re-coded to NA                         |
| `<1`        | Interpreted as trace, re-coded to `0`  |

---

### Cleaning Logic

- Columns ending in `_cover` were checked for non-numeric values and re-coded where needed
- `<1` was interpreted as presence and changed to `0`
- Values >100% or <0% were set to `NA`
- Final `Total_cover` was computed and rows where the sum ≠ 100 were dropped
- `Observer` names were simplified to keep only the first listed observer when multiple were listed

---

## SHARING / ACCESS INFORMATION

### 1. Licenses/restrictions placed on the data  
The data used in this project is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](http://creativecommons.org/licenses/by/4.0/). This license allows for redistribution and adaptation with appropriate credit.

---

### 2. Links to publications that cite or use the data  
All 16 known citations of the dataset can be viewed on the [host site](https://arcticdata.io/catalog/view/doi%3A10.18739%2FA2222R68W).  
Example publications include:

- https://onlinelibrary.wiley.com/doi/10.1111/gcb.17356  
- https://link.springer.com/article/10.1007/s10646-023-02708-w  
- https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0270957  

---

### 3. Links to other publicly accessible locations of the data

- Arctic Data Center DOI: [https://doi.org/10.18739/A2222R68W](https://doi.org/10.18739/A2222R68W)  
- DataONE catalog mirror: [https://search.dataone.org/view/doi:10.18739%2FA2222R68W](https://search.dataone.org/view/doi:10.18739%2FA2222R68W)

---

### 4. Links/relationships to ancillary data sets  
This dataset is part of the Arctic Shorebird Demographics Network (ASDN) and is related to several supporting data files:

- `site.csv`: Full names and metadata for ASDN site codes  
- `personnel.csv`: Observer information including affiliations and years of participation  
- `Study_Plot.kmz`: Google Earth-compatible plot shapefiles  
- `ASDN_Snow_survey.csv`: Original raw dataset used to derive the cleaned version

---

### 5. Was data derived from another source?

Yes. This processed dataset (`all_cover_fixed_OVERBYE.csv`) was derived from:

- **Original source**: Arctic Shorebird Demographics Network.  
  "ASDN_Snow_survey.csv" (1993–2014).  
  NSF Arctic Data Center.  
  [https://arcticdata.io](https://arcticdata.io)

---

### 6. Recommended citation for the project

> Lanctot, R.B., Brown, S.C., & Sandercock, B.K. (2017).  
> *Arctic Shorebird Demographics Network*.  
> NSF Arctic Data Center.  
> [https://arcticdata.io/catalog/view/doi:10.18739/A2222R68W](https://arcticdata.io/catalog/view/doi:10.18739/A2222R68W)
