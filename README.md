# Introduction
This work is a subset of [hlrcm](https://github.com/LLeiSong/hrlcm.git) project. It seeks to analyze the spatial pattern of agricultural land use change (cropland)in Tanzania over a 6-year (2017-2022) period, using advanced machine learning to map annual cropland cover in high resolution (~5 m) PlanetScope imagery combined with Sentinel-1 radar imagery over the entire country. This study will identify the areas and determine the rate of expansion in cropland during the analyzed time period while identifying temporal patterns in cultivation that indicate variations in cropping/fallow cycles. Ultimately, it will provide further insights into the nature and extent of agricultural transformation, which can help raise awareness of food security and biodiversity and enable better spatial planning and agricultural policies.

# Repository structure
* __data__: the directory to save the datasets, such as boundary geojson, image catalog, etc.
* __docs__: the directory to save the documents, notebooks, etc.
* __scripts__: the directory to save the independent scripts.

# Project details
## Time series
2017 - 2022 (Using 11/01 - 10/31 as the agriculture year)

## Dataset
PlanetScope NICFI basemaps (2017 - 2022), which will be queried from Planet website.
Harmonic regression coefficients of Sentinel-1 time series, which will calculated in GEE.
Other ancillary datasets, such as wetland dataset, permanent ice mask, or building dataset. We will download these datasets accordingly.
## Training labels
In general, training labels will be generated using an ensemble workflow that combines Random Forest and manual editing. The training labels (~2500) for 2018 are ready. The work plan to collect labels for other years:

* Step 1: randomly select 10% of existing tiles (~250) to revisit. Plus, select a number of new tiles (~250) in highly possible changed areas that are detected by BEFAST on Landsat NDVI.
Run the Random Forest model (maybe train a new one that is more general for these years) to predict the “gap-filled” labels for these newly selected tiles for each year.
Human editing these labels.
## Modeling
We will train a U-Net model for land cover mapping. The plan for now is that we first train a general big model, and then fine tune it each year. But this will be tested and adjusted accordingly.

## Independent validation dataset
Pixel-based validation dataset needs to be collected in order to make a validation report for the dataset. Geo-wiki, or other platforms or even just in QGIS will be used to collect validation dataset. Two persons separately collect, compare, and merge the labels. The method will follow the workflow of other global datasets, such as Copernicus Global Land Operations and the following WorldCover.
This part would be important to provide a dataset for others to use.

## Analysis
The analysis of the validated maps produced will be done by adopting the approach of Bilintoh et al. (2022), using the “Intensity Analysis” method. It will analyze the temporal difference of the agricultural land cover maps for the six-year period. The framework of intensity analysis revolved around three levels of intensities: interval, categorical, and transitional, which show different levels in detail. The categorical level intensity measures the sizes and intensities of each category’s (expansion or rotation) dormant or active, during a given time interval. The transitional level intensity will show which category’s transitions are intensively avoided or targeted during the studied period.

## Expected Outcomes
Upon completion, this research is expected to produce insights into the spatial analysis of agricultural land use patterns (expansion and rotation) in Tanzania during the considered time periods through the agricultural land use maps (digital records of agricultural fields) produced. We will also understand the rate of agricultural land use change in Tanzania and its impact on food security.
