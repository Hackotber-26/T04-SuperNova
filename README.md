T04-SuperNova - BurnWatch Integrated Analysis
Project Overview
BurnWatch is an automated, toolbox-free spatial analytics engine designed to detect, cluster, and prioritize crop residue burning and wildfire burn scars. By processing satellite-derived Differenced Normalized Burn Ratio (dNBR) matrices and cross-referencing them against NASA's Fire Information for Resource Management System (FIRMS) VIIRS active fire data, the system fills critical gaps where real-time thermal sensors miss small or rapidly moving burn events.
Problem Statement
Agricultural residue burning (stubble burning) is a massive driver of seasonal air pollution, environmental degradation, and respiratory crises in regions like Punjab, India (e.g., the Sangrur district). Traditional satellite monitoring relies heavily on thermal anomaly detection (like NASA FIRMS), which often fails to capture:
Small-scale burns falling below coarse sensor resolution limits.
Post-burn fields where active fires have already extinguished by the time a satellite passes over.
Cloud-obscured active fires that leave clear structural scars detectable later via surface reflectance indexes.
Objectives
Automated Burn Scar Extraction: Isolate valid structural burn patches using an optimized custom single-pass connected-component pixel cluster tracking algorithm without relying on commercial MATLAB toolboxes.
Cross-Satellite Verification: Cross-reference Sentinel-2 derived dNBR scars against NASA FIRMS VIIRS hotspots using a strict 500-meter spatio-temporal buffer.
Actionable Strategic Prioritization: Aggregate unverified (unmatched) burn scars into a 5-kilometre grid-mesh matrix to dynamically rank regions requiring immediate field enforcement or corporate intervention.
Technologies Used
Language & Core Logic: MATLAB (Native Core, Engineering Matrix Pipeline)
Data Integrations: Sentinel-2 Level-2A Multispectral Reflectance, NASA FIRMS VIIRS Active Fire Data (`.csv`)
Downstream Web Interfacing: JavaScript (Leaflet.js Data Consumption Layer)
Project Structure
```text
├── burnwatch_pipeline.m    # Master toolbox-free analytics engine and simulation model
└── results/                # Automated output directory
    ├── burnwatch_map_data.csv # Georeferenced burn scar metrics for Leaflet map integration
    ├── ranked_villages.csv    # 5km regional prioritization ranking matrix
    └── burnwatch_results.mat  # Internal MATLAB binary workspace backup
```
Implementation
The processing framework runs across three distinct core execution tiers:
The Burn-Scar Detection Matrix: Models a high-resolution grid mapped to a georeferenced bounding box. A single-pass neighborhood clustering algorithm evaluates pixel coordinates dynamically, converting raw imagery into continuous surface hectares. It filters out small localized clearings below a 1-hectare operational footprint threshold (25 pixels).
NASA FIRMS Spatial Cross-Referencing: Implements a fast Euclidean distance matrix evaluation scheme. It loops through active coordinates to label scars as `matched` (verified by thermal sensors) or `unmatched` (hidden burn scars exposed exclusively by structural index tracking).
Data Export Engine: Generates lightweight data sheets directly compatible with web GIS layers, automatically converting geo-coordinates to target region boundaries.
Results
Precision Validation: Successfully resolves individual smallholdings down to a 0.04-hectare pixel resolution granularity.
Blindside Detection: Isolates critical `unmatched` burn boundaries missed during diurnal orbit cycles.
Priority Dispatch Grids: Ranks high-priority zones (Grid Cells G1–G4) by total volume of unmonitored burning, optimizing field allocation paths.
Team
T04-SuperNova
Future Scope
Transition the core clustering algorithm into open-source Python (`NumPy`/`SciPy`) or native C++ execution kernels for cloud-native APIs.
Incorporate temporal synthetic aperture radar (SAR) profiles to detect ground changes under absolute thick cloud configurations.
Hook up automated webhooks directly feeding grid prioritization updates to regional air quality management teams.
