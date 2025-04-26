# Wikipedia Page Views Forecasting for Ad Optimization

![Time Series Forecasting](https://img.shields.io/badge/Time%20Series-Forecasting-blue)
![SARIMA/SARIMAX](https://img.shields.io/badge/SARIMA-SARIMAX-green)
![Prophet](https://img.shields.io/badge/Facebook-Prophet-purple)
![Python](https://img.shields.io/badge/Python-3.8%2B-yellow)

## 📊 Project Overview
This repository contains a comprehensive time series analysis and forecasting project for Ad Ease, a digital advertising company that helps businesses maximize clicks at minimum cost. The goal is to forecast Wikipedia page views across multiple language markets to optimize ad placement timing and bidding strategies.

## 🏢 Business Context
Ad Ease is developing an end-to-end digital advertising solution powered by three AI modules: Design, Dispense, and Decipher. This project contributes to the Decipher component by analyzing historical Wikipedia page views and forecasting future traffic patterns to:

- Optimize ad placement timing across different language markets
- Predict high-traffic periods for campaign planning
- Provide data-driven insights for bid optimization
- Maximize ROI for clients in diverse regional markets

## 📂 Dataset Description
The analysis uses two primary datasets:

1. **`train_1.csv`**: 
   - 145,063 Wikipedia pages × 550 days (July 2015-December 2016)
   - Page name format: `SPECIFIC_NAME_LANGUAGE.wikipedia.org_ACCESS_TYPE_ACCESS_ORIGIN`
   - Daily page view counts across different languages, access types, and access origins

2. **`Exog_Campaign_eng.csv`**:
   - Binary indicator (0/1) of campaign days for English pages
   - Used as exogenous variables for enhanced forecasting

## 🔍 Technical Approach

### Data Preprocessing
- Extraction of language, access type, and access origin information
- Handling of missing values (7.75% of data)
- Aggregation of data by language
- Time series transformation for modeling

### Stationarity Analysis
- Augmented Dickey-Fuller tests
- First and seasonal differencing 
- Time series decomposition (trend, seasonality, residual)

### Modeling Progression
1. **ARIMA**: Base models with first differencing
2. **SARIMA**: Added weekly (7-day) seasonality components
3. **SARIMAX**: Incorporated exogenous campaign variables
4. **Prophet**: Alternative forecasting approach with seasonality and regressors

### Model Optimization
- ACF and PACF analysis for parameter selection
- Grid search for optimal parameters
- Cross-validation for performance evaluation
- Multi-language forecasting pipeline

## 🔑 Key Findings

### Language-Specific Performance
| Language | MAPE (%) | Model Type | Predictability |
|----------|----------|------------|----------------|
| English (en) | 4.73% | SARIMAX | Excellent |
| Japanese (ja) | 11.65% | SARIMA | Moderate |
| German (de) | 13.94% | SARIMA | Moderate |
| Russian (ru) | 17.91% | SARIMA | Fair |
| Spanish (es) | 87.64% | SARIMA | Poor |

### Critical Insights
- Weekly seasonality is consistent across all languages
- Campaign data significantly improves forecast accuracy (3-4% MAPE improvement)
- Optimal model structure: SARIMA((0,1,0),(0,1,1,7))
- English pages receive 5-6x more traffic than other languages
- December holiday periods show unique patterns requiring special handling

## 🚀 Installation and Usage

### Prerequisites
- Python 3.8+
- Libraries: pandas, numpy, matplotlib, statsmodels, scikit-learn, prophet

### Setup
```bash
# Clone the repository
git clone https://github.com/yourusername/wikipedia-views-forecasting.git
cd wikipedia-views-forecasting

# Install required packages
pip install -r requirements.txt

# Run the analysis
jupyter notebook Wikipedia_Views_Forecasting.ipynb
```

## 📁 File Structure
```
wikipedia-views-forecasting/
├── data/
│   ├── train_1.csv                    # Main Wikipedia page views dataset
│   └── Exog_Campaign_eng.csv          # Campaign data for English pages
├── notebooks/
│   ├── 01_Data_Exploration.ipynb      # Initial data analysis and preprocessing
│   ├── 02_Stationarity_Analysis.ipynb # Stationarity tests and transformations
│   ├── 03_ARIMA_SARIMA_Modeling.ipynb # Time series model development
│   ├── 04_Prophet_Modeling.ipynb      # Facebook Prophet implementation
│   └── 05_Cross_Language_Analysis.ipynb # Multi-language pipeline and results
├── src/
│   ├── data_processing.py             # Data cleaning and transformation functions
│   ├── stationarity.py                # Stationarity test functions
│   ├── modeling.py                    # ARIMA/SARIMA/SARIMAX model functions
│   └── forecasting_pipeline.py        # End-to-end forecasting pipeline
├── results/
│   ├── figures/                       # Generated visualizations
│   └── model_performance.csv          # Performance metrics by language
├── requirements.txt                   # Required packages
└── README.md                          # Project documentation
```

## 📊 Results Summary
The analysis demonstrated that Wikipedia page views can be accurately forecasted, with varying degrees of success across languages:

1. **English pages**: Excellent forecasting accuracy (4.73% MAPE) using SARIMAX with campaign data
2. **Non-English pages**: Moderate to fair accuracy (11.65% - 17.91% MAPE) using SARIMA
3. **Spanish anomaly**: Requires further investigation (87.64% MAPE)

Business recommendations include:
- Implementing a tiered ad optimization strategy based on language forecast confidence
- Collecting language-specific campaign data to enhance non-English forecasts
- Developing specialized models for holiday periods and special events
- Creating automated retraining pipelines for continuous model improvement

## 🔮 Future Work
- Incorporate additional exogenous variables for non-English markets
- Develop category-specific models (news, entertainment, etc.)
- Implement anomaly detection for unusual traffic patterns
- Create ensemble models combining multiple forecasting approaches
- Develop real-time forecasting system for adaptive bidding

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgements
- Data provided by Ad Ease
- Analysis developed as part of the Wikipedia Traffic Forecasting business case study

---
*Note: This is a demonstration project and actual implementation would require integration with Ad Ease's systems and potentially more recent data.*