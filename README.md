# Lidar-and-Radar-Systems--Influence-of-fog-on-Sensors.
Comparative analysis of fog impact on Velodyne, Blickfeld LiDAR, and RADAR sensors. Evaluating performance degradation of LiDAR and RADAR point clouds under foggy conditions.


[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Data-Pandas%20%7C%20NumPy-orange.svg)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Task-Sensor%20Evaluation-green.svg)]()

This repository provides an empirical study on how dense fog degrades point cloud quality, return intensity, and spatial range across different automotive perception sensors[cite: 1, 3]. By comparing clear-weather recordings against artificial fog scenarios, this work quantifies signal attenuation, range loss, and phantom noise across two LiDAR systems and one millimeter-wave RADAR platform[cite: 1, 3].

---

##  Project Overview

- **Core Objective**: Analyze point cloud distance distributions and return intensities in clear (`c_building_pedestrian_clear_anon`) versus foggy (`c_building_pedestrian_fog_anon`) environments[cite: 1, 2].
- **Distance Metric**: Root Mean Square (RMS) distance calculation derived from $3\text{D}$ spatial coordinates $(x, y, z) \in \mathbb{R}^3$[cite: 2]:
  $$\text{RMS Distance} = \sqrt{x^2 + y^2 + z^2}$$
- **Key Finding**: LiDAR systems suffer severe point loss and range degradation beyond $10\text{ m}$ RMS distance in fog, whereas RADAR performance remains virtually unaffected up to $15\text{ m}$ RMS distance[cite: 3].

---

##  Sensors Under Evaluation

| Sensor Name | Type | Key Wavelength / Tech | Primary Impact in Fog |
| :--- | :--- | :--- | :--- |
| **Velodyne Puck** | Spin LiDAR | Laser Point Cloud | Massive reduction in overall point returns beyond $10\text{ m}$ RMS[cite: 1, 3]. |
| **BlickfeldCube 1** | MEMS LiDAR | Solid-State Laser | Intensity drop and creation of dense near-field noise ($0$--$10\text{ m}$)[cite: 1]. |
| **MMWAVCAS-RF-EVM** | MMW RADAR | Millimeter-Wave RF | Highly resilient; minor degradation observed only past $15\text{ m}$ RMS[cite: 1]. |

---

##  Methodology & Data Pipeline
1. **Data Ingestion**: Process point cloud data from clear and foggy recording sessions (`c_building_pedestrian_clear_anon` and `c_building_pedestrian_fog_anon`)[cite: 2].
2. **Preprocessing**: Parse spatial coordinates, drop unused metadata attributes, and merge sensor frames[cite: 2].
3. **Metric Calculation**: Execute `calculate_rms()` to compute $3\text{D}$ Euclidean distance metrics per return[cite: 2].
4. **Statistical Comparison**: Construct frequency histograms across RMS distance bins to visualize attenuation and scattering effects[cite: 2].

---

##  Experimental Results

### 1. Velodyne Puck LiDAR
* **Clear Condition**: Demonstrates consistent point return density across mid-to-long ranges[cite: 3].
* **Fog Condition**: Suffers severe laser scattering and signal attenuation[cite: 3]. Point returns beyond an RMS distance of $10\text{ m}$ drop drastically, restricting precision and active operational range[cite: 3].

### 2. BlickfeldCube 1 LiDAR
* **Clear Condition**: Yields balanced point frequency around the $10\text{ m}$ RMS distance bin (~$2 \times 10^6$ returns).
* **Fog Condition**: Exhibits significant backscatter noise. Near-field point return counts (~$10\text{ m}$ RMS) surge to ~$3.5 \times 10^6$ due to reflections from suspended fog particles, accompanied by a noticeable intensity drop in the $10$--$25\text{ m}$ range.

### 3. MMWAVCAS-RF-EVM RADAR
* **Clear Condition**: Displays uniform target tracking distributions across ranges.
* **Fog Condition**: Demonstrates high operational stability. Point frequency remains stable up to $15\text{ m}$ RMS distance, proving millimeter-wave RF signals easily penetrate atmospheric fog particles compared to optical laser pulses.

---

##  Visual Histogram Comparisons

Place your exported plots inside an `assets/` directory to display them in the README:

| Sensor | Clear Weather Histogram | Foggy Weather Histogram |
| :--- | :---: | :---: |
| **Velodyne Puck** | `assets/histogram_velodyne_clear.jpg` | `assets/histogram_velodyne_fog.jpg` |
| **BlickfeldCube 1** | `assets/histogram_blickfeld_clear.jpg` | `assets/histogram_blickfeld_fog.jpg` |
| **MMWAVCAS-RF-EVM** | `assets/histogram_radar_clear.jpg` | `assets/histogram_radar_fog.jpg` |

---

##  Summary & Sensor Fusion Insights

* **Optical Vulnerability**: Both mechanical and solid-state LiDAR sensors experience range loss and backscattering noise when encountering airborne fog droplets[cite: 3].
* **RF Reliability**: Millimeter-wave RADAR remains the most reliable sensor modality for target detection under adverse atmospheric visibility.
* **Sensor Fusion Recommendation**: Multi-sensor autonomous perception pipelines must dynamically increase RADAR confidence weighting under foggy conditions to compensate for LiDAR degradation.

---

##  Getting Started

### Installation
```bash
pip install numpy pandas matplotlib

Authors: Abdul Rahman Mohammed (Matriculation No.: 29641746), Dhruv Sunilkumar Joshi (Matriculation No.: 12141621)  Advisor: Prof. Dr. Stefan Elser  Institution: RW Hochschule Ravensburg-Weingarten University of Applied Sciences  Program: Master of Science - Mechatronics  Date: December 8, 2023 
