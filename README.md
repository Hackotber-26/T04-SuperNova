# T04-SuperNova | BurnWatch
### Integrated Satellite-Based Burn Scar Detection and Spatial Analysis System

## 1. Project Overview

**BurnWatch** is an automated, toolbox-free spatial analytics engine designed to detect, cluster, and prioritize crop residue burning and wildfire burn scars.

By processing satellite-derived Differenced Normalized Burn Ratio (dNBR) matrices and cross-referencing them with NASA's Fire Information for Resource Management System (FIRMS) VIIRS active fire data, the system identifies potential burn events that conventional real-time thermal monitoring may overlook.

The project aims to bridge critical gaps in satellite-based fire monitoring by identifying small-scale burns, extinguished fires, and post-burn scars through structural changes in satellite imagery.

## 2. Problem Statement

Agricultural residue burning (stubble burning) is a major contributor to seasonal air pollution, environmental degradation, and respiratory health concerns in regions such as Punjab, India, particularly in districts like Sangrur.

Traditional satellite monitoring relies heavily on thermal anomaly detection systems such as NASA FIRMS. However, these systems may fail to capture:

- **Small-scale burns:** Agricultural fires that fall below the spatial resolution limits of satellite thermal sensors.
- **Extinguished fires:** Post-burn fields where active flames have disappeared before the satellite's observation window.
- **Cloud-obscured fires:** Active fire events hidden by cloud cover, where subsequent surface reflectance analysis may reveal detectable burn scars.

BurnWatch addresses these limitations by combining structural burn scar analysis with active fire data to provide a more comprehensive monitoring and prioritization framework.

## 3. Objectives

### 3.1 Automated Burn Scar Extraction
Identify and isolate valid structural burn patches using an optimized, single-pass connected-component pixel clustering algorithm without depending on commercial MATLAB toolboxes.

### 3.2 Cross-Satellite Verification
Cross-reference Sentinel-2-derived dNBR burn scars against NASA FIRMS VIIRS active fire hotspots using a strict 500-metre spatial verification buffer.

### 3.3 Strategic Prioritization
Aggregate unverified (unmatched) burn scars into a 5-kilometre grid-mesh matrix to dynamically rank regions requiring immediate field investigation, enforcement, or intervention.

## 4. Technologies Used

| Category | Technologies |
|---|---|
| Programming Language | MATLAB |
| Core Processing | Native MATLAB matrix operations and custom algorithms |
| Satellite Imagery | Sentinel-2 Level-2A Multispectral Reflectance |
| Fire Detection Data | NASA FIRMS VIIRS Active Fire Data |
| Data Format | CSV, MAT |
| Web GIS Integration | JavaScript, Leaflet.js |

## 5. Project Structure

```text
T04-SuperNova/
│
├── README.md
│
├── burnwatch_pipeline.m
│   └── Master toolbox-free analytics engine
│
└── results/
    ├── burnwatch_map_data.csv
    │   └── Georeferenced burn scar metrics for Leaflet integration
    │
    ├── ranked_villages.csv
    │   └── 5 km regional prioritization ranking matrix
    │
    └── burnwatch_results.mat
        └── Internal MATLAB binary workspace backup
```

## 6. Implementation

The BurnWatch processing framework operates across three primary execution tiers.

### 6.1 Burn Scar Detection Matrix

- Models a high-resolution spatial grid mapped to a georeferenced bounding box.
- Implements a single-pass neighborhood clustering algorithm to dynamically evaluate pixel coordinates.
- Converts detected burn patches into measurable surface areas in hectares.
- Filters out localized clearings below a 1-hectare operational footprint threshold (25 pixels).

### 6.2 NASA FIRMS Spatial Cross-Referencing

- Implements a Euclidean distance-based spatial evaluation scheme.
- Compares detected burn scar coordinates against NASA FIRMS active fire locations.
- Uses a 500-metre spatial buffer for verification.
- Classifies detected scars into two categories:
  - `matched` – Burn scars with corresponding thermal fire detections.
  - `unmatched` – Burn scars without corresponding FIRMS thermal detections, highlighting potential events missed by active fire monitoring.

### 6.3 Data Export and Web GIS Integration

- Generates lightweight CSV datasets for downstream visualization.
- Exports georeferenced burn scar metrics for integration with web-based GIS platforms.
- Aggregates unmatched burn scars into a 5-kilometre regional grid.
- Produces ranked regional datasets to support spatial prioritization and field investigation.

## 7. Results and Key Outcomes

### 7.1 Spatial Detection Granularity
Successfully processes spatial data at a pixel resolution granularity of approximately 0.04 hectares per pixel.

### 7.2 Blindside Detection
Identifies unmatched burn scar boundaries that are not represented in the corresponding FIRMS active fire dataset, highlighting potential gaps in conventional thermal monitoring.

### 7.3 Priority Dispatch Grids
Generates ranked high-priority zones (Grid Cells G1–G4) based on the aggregated volume of unmonitored burning, supporting more efficient allocation of field investigation resources.

### 7.4 Automated Data Generation
Generates structured output datasets for further analysis and web-based visualization:

- `burnwatch_map_data.csv`
- `ranked_villages.csv`
- `burnwatch_results.mat`

<img width="1334" height="633" alt="image" src="https://github.com/user-attachments/assets/90ead2aa-20d2-43a3-a696-cc426bbc1725" />


## 8. Future Scope

- **Open-Source Algorithm Development:** Transition the core clustering algorithm into Python using NumPy/SciPy or native C++ execution kernels for scalable, cloud-native processing.
- **SAR-Based Detection:** Incorporate temporal Synthetic Aperture Radar (SAR) profiles to identify ground surface changes under persistent cloud cover.
- **Automated Monitoring:** Integrate webhooks and automated data pipelines to deliver grid-prioritization updates to regional air quality management authorities.
- **Advanced Web GIS Integration:** Develop interactive geospatial dashboards using Leaflet.js for real-time visualization of burn scar locations, verification status, and priority regions.

## 9. Team

**Team Name:** T04-SuperNova

**Project:** BurnWatch – Integrated Satellite-Based Burn Scar Detection and Spatial Analysis System

---

*Developed as part of the T04-SuperNova project initiative.*
