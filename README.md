# Retail Inventory Optimization for H&M Online Warehouse

## Project Overview

This project aims to optimize inventory for H&M's online warehouse by predicting product demand. Our goal is to ensure the warehouse maintains the appropriate stock levels, focusing on commonly sold items while avoiding overstock and stockouts. The analysis and modeling efforts are designed to refine stock management on a weekly or biweekly basis.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Objective](#objective)
3. [Data](#data)
4. [Methodology](#methodology)
5. [Modeling](#modeling)
6. [Project Structure](#project-structure)
7. [Requirements](#requirements)
8. [How to Run](#how-to-run)
9. [Results](#results)
10. [Next Steps](#next-steps)
11. [Contributors](#contributors)

## Objective

Our primary goals are to:
- **Predict weekly demand** for products based on type, color, price, and seasonality.
- **Optimize inventory levels** to meet customer demand, reducing excess stock and avoiding sold-out situations.
- Provide actionable insights on customer purchasing patterns, supporting effective inventory decisions.

## Data

- **Source**: H&M transaction data spanning from September 2018 to September 2020.
- **Content**: Transaction data without explicit inventory or geographical fields. Postal codes and purchase data are used to infer customer clusters based on buying patterns.
- **Processed Data**: The dataset was cleaned, deduplicated, and organized by weekly transactions, with key features engineered for forecasting.

## Methodology

1. **Data Preprocessing**: Cleaned the transaction data, resulting in a merged and complete dataset. Created weekly and monthly aggregates to manage data efficiently.
2. **Feature Engineering**:
   - **Time-Based Features**: Included weekly sinusoidal representations (`week_sin`, `week_cos`) and holiday indicators.
   - **Product-Level Features**: Utilized product type and color group codes.
   - **Lagged Variables**: Added `lag_units_sold` for 1-week and 2-week lag to capture recent sales trends.
3. **Clustering Analysis**:
   - **HDBSCAN**: Used for clustering customers by inferred geographical pockets, allowing for targeted stock allocation based on buying behavior.
4. **Modeling**:
   - **Ensemble Model with Random Forest**: Built to predict weekly units sold for each product-color combination, focusing on commonly sold items.
   - **Time-Series Forecasting**: Seasonal trends captured through ARIMA, supplemented by the ensemble model to adjust for seasonality.
5. **Evaluation and Testing**:
   - Created separate test and validation sets for performance assessment.
   - Implemented cross-validation and seasonal splits for model robustness.

## Modeling

- **Primary Model**: Random Forest model trained on weekly aggregated data for inventory demand forecasting. The model uses the following features:
  - `product_type_no`, `colour_group_code`, `average_price`, `lag_units_sold_1week`, `lag_units_sold_2weeks`, `week_sin`, `week_cos`, `day_of_week`, and `is_holiday`.
- **Ensemble Approach**: Combines Random Forest and ARIMA models, each focused on capturing unique patterns, allowing for a more accurate forecast by handling both trend and seasonal variations.
- **Data Splits**: For model validation, we split the data into training, test, and validation sets, with the last month’s first two weeks as the test set and the final two weeks as the validation set.

## Project Structure

```
├── data                    # Raw and processed data files
├── notebooks               # Jupyter notebooks for analysis and model training
├── scripts                 # Python scripts for data preprocessing, clustering, and modeling
├── results                 # Output files, visualizations, and model evaluations
├── README.md               # Project overview and instructions
└── requirements.txt        # Python dependencies
```

## Requirements

- **Python 3.7+**
- **Libraries**: Install the libraries from `requirements.txt` with:

    ```bash
    pip install -r requirements.txt
    ```

## How to Run

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd retail-inventory-optimization
   ```

2. **Data Preparation**:
   - Run the scripts in the `scripts` folder to load, preprocess, and organize the data into weekly aggregates.

3. **Run Analysis**:
   - Execute the Jupyter notebooks in the `notebooks` folder to explore data, perform clustering, and train the predictive model.

4. **View Results**:
   - Visualizations and model outputs are saved in the `results` folder for further analysis.

## Results

- **Clustering**: Customer clusters based on purchasing patterns are identified, offering insight into geographic buying behaviors.
- **Model Performance**: The Random Forest model performed well on weekly aggregated data, with minimal resource demands, making it feasible to use on available computing resources.
- **Inventory Recommendations**: Weekly and biweekly inventory adjustments are suggested based on demand predictions, prioritizing commonly sold items.

## Next Steps

- **Improve Model Accuracy**: Refine model with additional features (e.g., price trends, discount impact).
- **Geographic Precision**: Consider integrating postal code data to enhance clustering accuracy when available.
- **Real-Time Adjustments**: Explore real-time model updates for dynamic inventory management.

## Contributors

- [Ivan Chertov](ivanchertov86@gmail.com)
- [Emma Le Bars](lebars.emma@gmail.com)

