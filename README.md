# ⚡ Smart Home: Software for regulating and saving domestic electricity use

[![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Algorithm](https://img.shields.io/badge/Algorithm-Peak_Shaving-orange?style=for-the-badge)](https://en.wikipedia.org/wiki/Demand_response)
[![Status](https://img.shields.io/badge/Status-Simulation_Complete-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)](LICENSE)

<div align="center">
  <h3 align="center">Peak Shaving & Tariff-Aware Load Scheduling Engine</h3>

  <p align="center">
    A Python-based simulation aimed at optimizing residential energy loads, minimizing grid stress, and reducing household costs via Time-of-Use (ToU) arbitrage.

  </p>
</div>

---

## 📖 Executive Summary 

With the increasing instability in global energy grids, **Demand Side Management (DSM)** has become a critical area of research. **Py-SHEMS** is a computational framework designed to simulate a smart home environment and optimize its energy consumption profile.

The primary objectives of this project include:
* **Categorization:** Classifying household appliances based on their energy usage and priority levels.
* **Load Shifting:** Moving high-consumption loads from peak hours to off-peak hours without disturbing user comfort.
* **Cost Analysis:** Comparing energy costs between standard usage and the optimized algorithm using a three-tiered tariff structure.
* **Grid Stability:** Reducing the maximum load on the grid by enforcing a power threshold (7500W).

## ⚙️ Algorithm Architecture 

The core engine operates on a constraint-satisfaction logic. It classifies appliances into three distinct priority levels to ensure user comfort while optimizing grid usage.

### 1. Load Prioritization Logic
The appliances are categorized as follows:

* **Priority 1 (High/Critical):** Devices requiring continuous operation (e.g., Refrigerator, Modem).
* **Priority 2 (Medium):** Devices with moderate flexibility (e.g., Oven, Coffee Machine).
* **Priority 3 (Low):** Devices with minimal urgency (e.g., Game Console, Computer).

### 2. The Optimization Loop
The algorithm iterates through 24-hour cycles with the following logic:
1.  **Monitor:** Calculate total instantaneous power ($P_{total}$).
2.  **Compare:** Check if $P_{total} > P_{threshold}$ (7500W).
3.  **Identify:** Find active appliances in **Priority 3** (Low Priority).
4.  **Action:** Shift Priority 3 loads to the nearest "Off-Peak" or "Standard" tariff slot.
5.  **Recalculate:** Update the load profile and cost matrix.

```python
# Pseudocode of the Optimization Logic
THRESHOLD = 7500 # Watts

def optimize_load(hour, current_load):
    if current_load > THRESHOLD:
        excess_load = current_load - THRESHOLD
        # Attempt to shift Priority 3 devices first
        shifted_load = shift_devices(priority=3, amount=excess_load)
        
        if shifted_load < excess_load:
             # If P3 is not enough, touch P2
             shift_devices(priority=2, amount=(excess_load - shifted_load))
             
    return rebalanced_schedule
```

## 📊 Financial & Technical Analysis (Analiz ve Sonuçlar)
The simulation was tested against a standard 3-Tier Tariff (Day, Peak, Night) scenario. The results demonstrate that load shifting significantly reduces costs without changing the total energy consumed.

### Key Performance Indicators (KPIs)
* **Total Energy Consumption:** Remains constant at 94.00 kWh for both scenarios (Efficiency).
* **Daily Cost Savings:** Reduced from 334.46 TL to 312.99 TL (-6.4%).
* **Daily Financial Gain:** A saving of 21.47 TL per day is achieved.
* **Annual Savings Projection:** Approximately 7,836.55 TL per year.
* **Peak Load Management:** Successfully kept the load under the 7500W threshold during peak hours.

## 🛠️ Tech Stack
The project leverages the following technologies and libraries:

* **Core Language:** Python 3.10
* **Data Analysis:** Pandas, NumPy
* **Visualization:** Matplotlib, Seaborn
* **Environment:** Visual Studio Code

## 🔮 Future Improvements (Gelecek Planları)
To evolve this simulation into a deployment-ready product:

- [ ] **Renewable Integration:** Incorporate Solar (PV) production data to prioritize usage when solar generation is high.
- [ ] **Machine Learning:** Implement LSTM networks to predict household usage patterns (Forecasting).
- [ ] **Real-Time I/O:** Adapt the Python script to run on a Raspberry Pi, reading real sensor data via MQTT.
