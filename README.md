# Oil-Spill-Detection
The code aims to:

Detect oil spills based on Sentinel-1 Synthetic Aperture Radar (SAR) data.
Process each anomaly (location and timestamp) identified in an AIS dataset.
Generate a map for every anomaly where an oil spill is detected and export vector data for further analysis.
Key Components of the Code
1. Input Data
The input data (anomalies_df) contains:

Latitude (LAT) and Longitude (LON): Location of potential anomalies.
BaseDateTime: Timestamp associated with the anomaly.
2. Sentinel-1 Data Filtering
Filters SAR images from the COPERNICUS/S1_GRD collection based on:
Date: One day around the anomaly date.
Location: A dynamic 10 km buffer around the anomaly coordinates.
Polarization: VV band.
Instrument Mode: IW (Interferometric Wide Swath).
3. Oil Spill Detection Process
Despeckling: Applies a focal mean filter to reduce radar noise.
Thresholding: Detects potential oil spills by identifying pixels with radar backscatter values less than -22 dB.
Masking: Creates a binary mask for areas detected as oil spills.
4. Area Calculation
The area of the detected oil spill is calculated:

Multiplies the mask by the pixel area (in square kilometers).
Sums up the total detected area within the defined ROI (Region of Interest).
5. Conditional Map Generation
A map is generated only if the detected oil spill area is greater than zero.
The map includes layers:
Sentinel-1 image (VV band).
Despeckled image.
Oil spill detection (binary mask).
Oil spill vector overlay.
6. Export to Google Drive
Detected oil spill vectors are exported to Google Drive in Shapefile format for further analysis.

Code Flow
Loop through each row in the anomalies dataset.
For each anomaly:
Define a 10 km ROI around the anomaly location.
Fetch and process Sentinel-1 data for that ROI.
Detect oil spills based on thresholding and masking.
Calculate the area of the detected oil spill.
If an oil spill is detected:
Generate a map with relevant layers.
Export vectorized spill data to Google Drive.
Display the map dynamically for each detected spill.
Features and Advantages
Dynamic ROI: Adapts to each anomaly's location for targeted analysis.
SAR Data Usage: Exploits radar's capability to detect oil spills even in adverse weather or low-light conditions.
Efficient Processing: Avoids generating maps for anomalies without detected oil spills.
Scalable and Automatable: Can handle large datasets and process multiple anomalies programmatically.
Data Export: Facilitates further geospatial analysis by exporting results as Shapefiles.
Limitations
Threshold Sensitivity: The threshold value for detection (-22 dB) might need tuning based on environmental conditions.
SAR Image Availability: Limited to areas and dates with Sentinel-1 coverage.
Assumptions: Requires the input anomalies dataset to have accurate timestamps and locations.
This code provides a streamlined approach to anomaly-specific oil spill detection and visualization while being resource-efficient by only focusing on relevant anomalies.
