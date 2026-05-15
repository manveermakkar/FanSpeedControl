# 🌡️ Air Conditioner / Fan Speed Control Based on Temperature and Humidity

A smart climate control system that uses **fuzzy logic** to automatically adjust fan or AC speed based on real-time temperature and humidity inputs. This was developed as a group project using real weather data from Agra, India.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Methodology](#methodology)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Future Scope](#future-scope)
- [References](#references)

---

## Overview

Traditional air conditioning and fan systems rely on fixed thermostats or manual settings that fail to adapt dynamically to changing environmental conditions — and often ignore humidity entirely, which significantly affects human comfort.

This project addresses that gap by implementing a **fuzzy logic-based control system** that:

- Takes **temperature** and **humidity** as real-time inputs
- Outputs an appropriate **fan/AC speed** level
- Makes decisions that mimic human reasoning (e.g., "slightly warm + very humid → high fan speed")

The system was tested using real weekly weather data from **Agra, India** (late June / early July), a city known for its high heat and fluctuating humidity.

---

## Features

- ✅ Dual-input fuzzy logic system (temperature + humidity)
- ✅ Two implementations: basic rule-based logic and advanced sigmoidal/Gaussian fuzzy inference
- ✅ Real weather data from Agra used for testing
- ✅ Smooth, continuous fan speed output (no abrupt on/off switching)
- ✅ Visualization of temperature, humidity, and fan speed trends
- ✅ Energy-efficient control — avoids unnecessary cooling

---

## Methodology

### Real Data Used (Agra, India)

| Day | Temperature (°C) | Humidity (%) |
|-----|-----------------|--------------|
| Fri | 33 | 75 |
| Sat | 35 | 72 |
| Sun | 32 | 78 |
| Mon | 35 | 70 |
| Tue | 34 | 73 |
| Wed | 32 | 80 |
| Thu | 30 | 82 |

Data sourced from AccuWeather forecasts for Agra.

---

### Implementation 1 — Basic Rule-Based Logic

A simplified fuzzy decision system using `if-else` conditionals:

| Condition | Fan Speed |
|-----------|-----------|
| Temperature < 30°C | Low (1) |
| Temperature 30–34°C AND Humidity < 60% | Medium (2) |
| Temperature 30–34°C AND Humidity ≥ 60% | High (3) |
| Temperature > 34°C | High (3) |

**Limitation:** Does not capture partial truth or overlapping linguistic categories.

---

### Implementation 2 — Sigmoidal & Gaussian Fuzzy Inference (Upgraded)

Uses the `scikit-fuzzy` library with proper fuzzy membership functions:

- **Sigmoid functions** — for "low" and "high" categories (smooth 0→1 or 1→0 transitions)
- **Gaussian functions** — for "medium" categories (bell-curve shape)

**Fuzzy Variables:**

| Variable | Universe | Linguistic Sets |
|----------|----------|----------------|
| Temperature | 0–50°C | Low, Medium, High |
| Humidity | 0–100% | Low, Medium, High |
| Fan Speed | 0–100% | Slow, Medium, Fast |

**Fuzzy Rules:**

```
IF temperature is LOW   AND humidity is LOW    → fan_speed is SLOW
IF temperature is MEDIUM AND humidity is MEDIUM → fan_speed is MEDIUM
IF temperature is HIGH  OR  humidity is HIGH   → fan_speed is FAST
IF temperature is MEDIUM AND humidity is LOW   → fan_speed is MEDIUM
IF temperature is HIGH  AND humidity is LOW    → fan_speed is FAST
```

---

## Tech Stack

| Tool / Library | Purpose |
|---------------|---------|
| Python 3 | Core programming language |
| `scikit-fuzzy` | Fuzzy logic inference system |
| `numpy` | Numerical computations |
| `matplotlib` | Data visualization |
| Google Colab | Development environment |

---

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/fan-speed-fuzzy-control.git
   cd fan-speed-fuzzy-control
   ```

2. **Install dependencies**
   ```bash
   pip install numpy matplotlib scikit-fuzzy
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook fancontrol.ipynb
   ```
   Or open directly in [Google Colab](https://colab.research.google.com/).

---

## Usage

Open `fancontrol.ipynb` and run all cells. The notebook contains two implementations:

- **Cell Block 1** — Basic if-else rule-based fan speed control with a plot
- **Cell Block 2** — Advanced sigmoidal fuzzy inference system with labeled output chart

You can modify the `temps` and `humids` lists to test with your own weather data:

```python
temps  = [33, 35, 32, 35, 34, 32, 30]   # Temperature in °C
humids = [75, 72, 78, 70, 73, 80, 82]   # Humidity in %
```

---

## Results

The upgraded fuzzy logic model produces continuous, smooth fan speed values for each input set:

| Input Set | Temp (°C) | Humidity (%) | Fan Speed (%) |
|-----------|-----------|--------------|---------------|
| Set 1 | 33 | 75 | ~81.9 |
| Set 2 | 35 | 72 | ~79.2 |
| Set 3 | 32 | 78 | ~80.3 |
| Set 4 | 35 | 70 | ~77.5 |
| Set 5 | 34 | 73 | ~80.8 |
| Set 6 | 32 | 80 | ~80.2 |
| Set 7 | 30 | 82 | ~94.0 |

The sigmoidal fuzzy inference model significantly outperforms the basic rule-based approach by:
- Providing granular, percentage-based fan speed output
- Handling overlapping conditions smoothly
- Closely mirroring real-world fuzzy control systems

---

## Future Scope

- 🌐 **IoT Integration** — Remote monitoring and control via mobile apps or web dashboards
- 📡 **Multi-Sensor Networks** — Zone-based temperature/humidity detection across a room or building
- 🤖 **Machine Learning** — Predictive fan control by learning usage patterns over time
- ⚡ **Power Optimization** — Motion-sensor-triggered energy saving; smart grid scheduling
- 🎙️ **Voice Assistant Support** — Alexa/Google Assistant compatibility
- 🌬️ **Air Quality Monitoring** — CO₂ and particulate sensors for comprehensive indoor environment control
- 🏢 **Large-Scale Deployment** — Scalable to commercial HVAC systems in offices, schools, and hospitals

---

## References

1. A. Ali, Y. You, and Z. Zhao, *"Fuzzy Logic Controller of Temperature and Humidity Inside an Agricultural Greenhouse,"* ResearchGate, 2016. [Link](https://www.researchgate.net/publication/303563634)

2. G. H. Merabet, M. Essaaidi, and D. Benhaddou, *"Effectiveness of the Fuzzy Logic Control to Manage the Microclimate Inside a Smart Insulated Greenhouse,"* Journal of Smart Cities, vol. 7, no. 3, 2023. [Link](https://www.mdpi.com/2624-6511/7/3/55)

3. A. Jaiswal and S. Verma, *"IoT-Based Hydroponic Temperature and Humidity Control System Using Fuzzy Logic,"* IJSRED, vol. 2, no. 2, pp. 160–165, 2019. [Link](https://www.researchgate.net/publication/332098358)

---

## 📄 License

This project was developed as an academic group project. Feel free to use or build upon it for educational purposes.
