# AI FinOps & Cloud CapEx Simulator

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Shiny](https://img.shields.io/badge/PyShiny-App-brightgreen)](https://shiny.posit.co/py/)
[![Monte Carlo](https://img.shields.io/badge/Simulation-Monte%20Carlo-orange)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A stochastic risk assessment and CapEx optimization engine for AI Cloud workloads, modeling on-demand versus spot pricing dynamics.

[🌐 Live Web App](https://shaurya-portfolio.shinyapps.io/ai-finops-simulator/)

---

### 📸 Dashboard Preview

![Market Sizing](https://github.com/100rya-py/AI-FinOps-and-CapEx-Simulator/blob/main/Screenshots/Market%20Sizing.png)
![ROI Risk Simulation](https://github.com/100rya-py/AI-FinOps-and-CapEx-Simulator/blob/main/Screenshots/ROI%20Risk%20Simulation.png)

---

## 📌 Project Overview

This simulator provides a rigorous quantitative framework for assessing AI infrastructure costs. By merging deterministic unit economics with stochastic risk modeling, the application allows technical leaders to forecast Total Addressable Market (TAM) revenue, evaluate CapEx thresholds, and measure the ROI of FinOps optimization agents. 

The core mathematical engine models the volatility of cloud compute pricing (specifically GPUs like NVIDIA H100 and A100) across major providers, transitioning smoothly between real-time API integrations and statistical fallbacks.

## ⚙️ Core Features & The Complete Pipeline

**1. Live Data Ingestion & API Integration (Extract)**

*   **Real-Time Price Fetching:** Integrates with the ComputePrices API to extract live on-demand and spot GPU rates for enterprise AI workloads (NVIDIA A100, H100) across AWS and DeepInfra.
*   **Local State Cache:** Dynamically updates a `cloud_pricing.yaml` configuration file to act as a local ledger for baseline rate tracking and failover redundancy.

**2. Statistical Fallback Architecture (Transform & Clean)**

*   **Stochastic Volatility Simulation:** In the event of API rate limits, the engine mathematically simulates spot market fluctuations using a Gaussian (Normal) Distribution (Mean discount = ~70%, Standard Deviation = 5%).
*   **Seamless Failover:** Ensures zero downtime in the pipeline by automatically generating statistically valid synthetic pricing when live endpoints are unreachable.

**3. Deterministic Business Modeling (Unit Economics)**

*   **CapEx vs OpEx Metrics:** Calculates baseline Total Addressable Market (TAM), projected revenue, total operational costs, and base ROI using fixed user inputs.
*   **Net Margin Calculation:** Accurately models the gross and net savings of utilizing FinOps agent software versus traditional on-demand provisioning.

**4. Applied Mathematics: Monte Carlo Risk Engine**

Instead of static assumptions, the engine applies rigorous probability modeling:
*   **Vectorized Iterations:** Executes 10,000 parallel simulation cycles using `numpy` to model simultaneous market share and pricing variance without freezing the client UI.
*   **Percentile Extraction:** Calculates continuous probability thresholds, outputting the 10th (Worst-Case), 50th (Expected), and 90th (Best-Case) percentiles for Net Profit and ROI.

**5. Interactive Frontend Application (Serving)**

*   **Reactive PyShiny Layout:** Compiles backend math into a highly responsive, styled web interface featuring dual-tab navigation for Deterministic and Risk Simulation views.
*   **High-Fidelity Visuals:** Leverages `plotly` to render interactive Waterfall charts for unit economics and distribution Bar charts for Monte Carlo risk scenarios.

## 💻 Tech Stack

*   **Languages:** Python 3.10+, YAML
*   **Data Collection & Architecture:** `requests`, `python-dotenv`
*   **Analytics & Mathematics:** `numpy`, `pandas`
*   **Frontend & Visualization:** `shiny`, `shinywidgets`, `plotly`
*   **Infrastructure:** Local `yaml` caching, Shinyapps.io
  

## 🚀 Installation & Local Deployment

### 1. Clone the Repository
```bash
git clone https://github.com/shaurya-portfolio/Ai-FinOps-Simulator.git
cd Ai-FinOps-Simulator
```

### 2. Set Up a Virtual Environment (Recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Environment Variables
Create a `.env` file in the root directory to store your API keys for the pricing pipeline:
```env
COMPUTE_PRICES_API_KEY=your_api_key_here
```

### 5. Launch the Application
```bash
shiny run app.py --reload
```

## 🏗️ Project Structure

```text
├── .github/workflows/update_data.yaml               
├── src/                       
│   ├── business_logic.py      
│   ├── cloud_pricing.yaml      
│   ├── scraper.py              
│   └── simulation_engine.py    
├── .env                        
├── .gitignore                  
├── app.py                     
└── requirements.txt            
