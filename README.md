# 🛰️ ISS Tracker & Sky Visualizer

![Language](https://img.shields.io/badge/language-Python-blue.svg)
![Library](https://img.shields.io/badge/library-Skyfield-orange.svg)
![Status](https://img.shields.io/badge/status-Active-green.svg)

A real-time orbital tracking engine that calculates the position of the International Space Station (ISS) relative to a specific observer on Earth. This project uses Two-Line Element (TLE) sets to predict "human-visible" flyovers and generates professional astronomical sky charts for observation.

## 🔭 Project Overview

This tool answers three critical questions:
1.  **Where is the ISS right now?** (Real-time Geocentric & Topocentric tracking).
2.  **When can I see it?** (Predicting passes where the station is illuminated while the observer is in darkness).
3.  **Where do I look?** (Generating a Polar Radar Plot to guide the observer).

## 📊 Features

* **Live Telemetry:** Fetches fresh TLE data from CelesTrak to ensure sub-kilometer accuracy.
* **Visibility Logic:** Filters out daytime passes and deep-shadow passes to find only true visual opportunities.
* **Sky Chart Generation:** Creates a "Radar Plot" (Azimuth/Elevation) visualizing the arc of the station across the sky.
* **30-Day Scanner:** Scans up to a month in advance to find rare high-latitude viewing windows.

## 🧠 The Science

This project relies on **Vector Astrometry** provided by the Skyfield library.

### 1. Coordinate Systems
To track a satellite, we must convert between multiple reference frames:
* **TEME (True Equator Mean Equinox):** The inertial frame used by the raw TLE data.
* **ITRF (International Terrestrial Reference Frame):** The Earth-fixed frame (rotating with the planet) used to determine Latitude/Longitude.
* **Topocentric (Alt/Az):** The observer's local frame. We calculate the vector difference ($\vec{r}_{sat} - \vec{r}_{observer}$) to determine where to point a telescope.

### 2. The Visibility Problem
A satellite is only visible to the naked eye if a specific geometric "triangle" occurs:
1.  **Elevation > 0°:** The satellite is above the observer's horizon.
2.  **Solar Elevation < -6°:** The observer is in Civil Twilight or darkness (Sun is down).
3.  **Satellite Illumination:** The satellite is at a high enough altitude to remain in direct sunlight (not in Earth's shadow).

This project solves this geometry for every second of the orbit to filter false positives.

## 🛠 Installation

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/yourusername/iss-tracker.git](https://github.com/yourusername/iss-tracker.git)
    cd iss-tracker
    ```

2.  **Install Dependencies**
    We use `Skyfield` for the physics engine and `Matplotlib` for visualization.
    ```bash
    pip install skyfield matplotlib numpy
    ```

## 💻 Usage

The core logic is contained in the Jupyter Notebook `Satellite_Tracker.ipynb`.

1.  **Open the Notebook:**
    ```bash
    jupyter notebook Satellite_Tracker.ipynb
    ```
2.  **Set Your Location:**
    Update the coordinates in **Cell 1** to your specific city:
    ```python
    # Example: Banchory, Scotland
    lat_degrees = 57.0519
    lon_degrees = -2.4839
    ```
3.  **Run All Cells:**
    * **Cell 2** gives you the live dashboard.
    * **Cell 3** scans the next 30 days for passes.
    * **Cell 4** generates the Sky Chart for the next pass.

## 📷 Visualization Preview

**The Sky Chart (Radar Plot)**
The notebook generates a polar plot representing the dome of the sky.
* **Center:** Zenith (90° - Straight up).
* **Edge:** Horizon (0°).
* **Cyan Line:** The path of the satellite.

## 🤝 Contributing
Contributions are welcome! Future roadmap items include:
* [ ] Adding Starlink Train visualization.
* [ ] Automating email alerts for high-quality passes (>60° elevation).
* [ ] 3D Globe visualization using `Cartopy`.

## 📜 License
Distributed under the MIT License.