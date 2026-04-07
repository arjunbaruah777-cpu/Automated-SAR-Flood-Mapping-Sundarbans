# Automated SAR Flood Delineation: Cyclone Remal Impact on the Sundarbans

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Google Earth Engine](https://img.shields.io/badge/Google_Earth_Engine-API-green?style=flat&logo=google)
![QGIS](https://img.shields.io/badge/QGIS-3.x-lightgrey?style=flat&logo=qgis)

## 📌 Project Overview
When Cyclone Remal struck the Sundarbans Mangrove Delta in May 2024, optical satellites were completely blinded by severe cloud cover. To rapidly and accurately quantify the true extent of the storm surge, I developed an automated cloud-computing pipeline utilizing Synthetic Aperture Radar (SAR) data.

This project demonstrates an end-to-end spatial data science workflow: connecting a local Python environment to Google Earth Engine's supercomputers, processing gigabytes of raw satellite data, executing mathematical change detection, and delivering a professional cartographic product.

### 🚨 Key Result
**Total Inundated Area Identified:** 1,563 Square Kilometers.

---

## ⚙️ Technical Architecture & Methodology

![Pipeline Infographic](AUTOMATED%20SAR%20FLOOD%20QUANTIFICATION.png)

The pipeline is structured into four distinct phases:

### Phase 1: Environment & Cloud Authentication
* Configured an isolated Conda environment (`flood_project`) to manage dependencies.
* Utilized the `ee` API to establish a secure, authenticated connection between the local Jupyter Notebook and Google Earth Engine servers.

### Phase 2: SAR Data Retrieval & Delineation
* **Data Source:** Queried the ESA Sentinel-1 database for VV+VH polarization, IW mode.
* **Temporal Filtering:** Retrieved 37 total images spanning a Baseline (April/May) and Peak Cyclone (May/June) timeline. Applied a temporal `median()` reducer to eliminate speckle noise and stabilize the radar signature.
* **Change Detection:** Applied a `-18 dB` backscatter threshold to mathematically isolate smooth surfaces (water). Subtracted the baseline water extent from the peak cyclone extent to isolate the newly inundated pixels.

### Phase 3: Quantification & Big Data Export
* **Cloud Computation:** Executed `reduceRegion()` algorithms directly on Google's servers to count millions of 10m flood pixels within the 10,000 sq km bounding box, deriving the exact 1,563 sq km metric.
* **Asset Delivery:** Triggered a background batch export to compile the binary output into a high-resolution, georeferenced GeoTIFF (`Export.image.toDrive()`).

### Phase 4: Cartographic Design (QGIS)
* Transferred the processed GeoTIFF from the cloud to desktop GIS.
* Applied custom categorical symbology (making non-flood data 100% transparent and flood data vibrant red).
* Integrated the authoritative UN World Database on Protected Areas (WDPA) boundaries for India and Bangladesh.
* Designed a professional print layout including scale, north arrow, and metadata.

---

## 🗺️ Final Deliverable

![Final Flood Map](SUNDARBAN%20REMAL%202024.jpeg)

## 💻 How to Reproduce This Workflow
1. Clone this repository.
2. Ensure you have Miniconda/Anaconda installed.
3. Install the required libraries: `conda install -c conda-forge earthengine-api geemap jupyterlab`
4. Open the Jupyter Notebooks in order and run the cells. You will be prompted to authenticate with your Google account on the first run.

---
*Developed by Arjun Baruah | Spatial Data Science & GIS Automation*
