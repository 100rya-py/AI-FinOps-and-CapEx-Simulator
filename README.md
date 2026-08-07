# AI FinOps & Cloud CapEx Simulator

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Shiny](https://img.shields.io/badge/PyShiny-App-brightgreen)](https://shiny.posit.co/py/)
[![Monte Carlo](https://img.shields.io/badge/Simulation-Monte%20Carlo-orange)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A stochastic risk assessment and CapEx optimization engine for AI Cloud workloads, modeling on-demand versus spot pricing dynamics.

**[🌐 Live Web App](https://shaurya-portfolio.shinyapps.io/ai-finops-simulator/)** | **[Insert Alternative Web App Link Here]**

---

### 📸 Dashboard Preview

*(Replace the placeholder image below with a screenshot of your deployed Shiny web application)*

![Web App Preview]([Insert_Link_To_Web_App_Photo_Here])

---

## 📌 Project Overview

This simulator provides a rigorous quantitative framework for assessing AI infrastructure costs. By merging deterministic unit economics with stochastic risk modeling, the application allows technical leaders to forecast Total Addressable Market (TAM) revenue, evaluate CapEx thresholds, and measure the ROI of FinOps optimization agents. 

The core mathematical engine models the volatility of cloud compute pricing (specifically GPUs like NVIDIA H100 and A100) across major providers, transitioning smoothly between real-time API integrations and statistical fallbacks.

## 🛠️ Key Architectural Features

*   **Real-Time Cloud Pricing ETL Pipeline:** Actively fetches live spot and on-demand GPU rates across providers (AWS, DeepInfra) to maintain accurate market benchmarks.
*   **Statistical Fallback Engine:** In the event of API rate limits or failure, the pipeline seamlessly shifts to a Gaussian (Normal) distribution model to simulate stochastic market volatility and spot discounts mathematically.
*   **Vectorized Monte Carlo Simulations:** Executes 10,000 iterations of market share and pricing variance using NumPy. Extracts the 10th (Worst Case), 50th (Expected), and 90th (Best Case) percentiles for Net Profit and ROI without freezing the client UI.
*   **Deterministic Business Modeling:** Calculates baseline Unit Economics, Total Costs (Fixed + Variable), Projected Revenue, and Gross/Net Savings.
*   **Interactive PyShiny Interface:** A fully reactive frontend built with Shiny for Python and Plotly, delivering high-fidelity waterfall charts and risk distribution visualizations.

## 📊 Data Sources & Integration

*(Add specific details about your underlying market data, APIs, or assumptions here)*

*   **Primary Data Source:** `[Insert Data Source / API Documentation Here]`
*   **Internal Configuration:** Spot rate baselines and on-demand rates are tracked via `src/cloud_pricing.yaml`.
*   **Automated Updates:** The daily ETL script (`update_pricing_pipeline`) dynamically adjusts unit prices and variable costs.

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
├── .github/                   
├── src/                       
│   ├── business_logic.py      
│   ├── cloud_pricing.yaml      
│   ├── scraper.py              
│   └── simulation_engine.py    
├── .env                        
├── .gitignore                  
├── app.py                     
└── requirements.txt            
