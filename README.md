# Hamilton City Flood Inundation Prediction

This project uses GIS spatial analysis and Python automation to predict flood inundation areas and water depths in Hamilton City under extreme rainfall scenarios. It also identifies potential shelter locations to support emergency planning.

## 🌧️ Project Background

As extreme weather events become more frequent due to climate change, Hamilton is likely to face more serious rainfall-related flooding. This project explores the questions:

> **When extreme rainfall occurs, where will flooding happen, and where can people go?**

## 🛠️ Methodology

The workflow integrates ArcGIS Pro hydrological tools with Python scripting, and follows the steps below:

1. **Data Preparation**  
   - Hamilton City boundary, DEM (1m resampled to 10m), soil and landcover layers
   - Rainfall scenarios: 10-, 20-, and 50-year return periods (1-hour duration)

2. **Weighted Flow Simulation**  
   - Composite weight raster created from soil and landcover data using Manning’s n value references
   - Fill → Flow Direction → Weighted Flow Accumulation

3. **Water Depth Estimation**  
   - Water depth = Rainfall × Flow Accumulation  
   - Filter extreme values using the 90th percentile threshold

4. **Smoothing and Region Extraction**  
   - Focal Statistics (MEAN or MEDIAN, radius = 3 or 5)  
   - Remove areas with depth < 0.1m  
   - Use Region Group and Raster to Polygon to extract inundation regions > 1000 m²

5. **Contour and Shelter Site Identification**  
   - Generate 0.5 m interval contours  
   - Use Erase tool to find non-flooded schools/hospitals as candidate shelters

6. **Result Metrics Extracted**  
   - Total inundation area  
   - Number of flood regions  
   - Average and maximum flood depths

## 📊 Key Findings

- MEAN smoothing generates larger and deeper flood areas than MEDIAN
- A radius of 5 (vs. 3) improves spatial continuity
- Flood characteristics increase with rainfall intensity
- Under extreme rainfall, results are highly sensitive to statistical methods used

## 📂 Files Included

- `Report.pdf` – Full methodology, data sources, results, and analysis  
- `Poster.pptx` – Visual summary for presentation  
- `analysis_script.ipynb` – Jupyter Notebook automating spatial and statistical analysis

## 📉 Data Sources

| Dataset | Source |
|--------|--------|
| DEM (1m LiDAR) | [LINZ Data Service](https://data.linz.govt.nz/layer/117092-waikato-hamilton-lidar-1m-dem-2023/) |
| Rainfall | [NIWA HIRDS](https://hirds.niwa.co.nz/) |
| Boundary | [Stats NZ](https://datafinder.stats.govt.nz/layer/120963-territorial-authority-2025/) |
| Soil & Landcover | [LRIS](https://lris.scinfo.org.nz) |
| Facilities | [LINZ](https://data.linz.govt.nz/layer/105588-nz-facilities/) |

## ⚠️ Limitations

- Did not account for underground drainage infrastructure  
- No accessibility analysis included in shelter site selection  
- Weight values not tested for sensitivity

## 🔍 Future Work

- Incorporate real-time rainfall and drainage network simulation  
- Perform sensitivity analysis on weights  
- Integrate accessibility network analysis for shelter planning

---

