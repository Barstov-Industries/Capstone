# Retail Inventory Optimization

## Project Overview

This project focuses on optimizing inventory for H&M’s online warehouse. The goal is to ensure that the right products are available in the right quantities at the right time, helping reduce overstock and avoid stockouts. The analysis includes customer purchasing patterns to forecast inventory needs and meet demand.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Objective](#objective)
3. [Data](#data)
4. [Methodology](#methodology)
5. [Project Structure](#project-structure)
6. [Requirements](#requirements)
7. [How to Run](#how-to-run)
8. [Results](#results)
9. [Next Steps](#next-steps)
10. [Contributors](#contributors)

## Objective

Our objective is to:
- Predict the types and volumes of items customers are likely to purchase.
- Optimize stock levels to ensure that the online warehouse has adequate supplies, avoiding overstocking and sold-out items.

## Data

- **Source**: This project uses the H&M dataset, containing transaction data from September 2018 to September 2020.
- **Content**: Transaction-level data without geographical or inventory-specific fields. Customer postal codes are assumed to imply geographic clusters.

## Methodology

1. **Data Preprocessing**: Cleaned and merged datasets with no null values or duplicates.
2. **Feature Engineering**: Extracted seasonal trends and customer buying patterns.
3. **Clustering Analysis**: Used DBSCAN and HDBSCAN to group customers into geographic clusters based on assumed proximity.
4. **Time-Series Forecasting**: Employed ARIMA for seasonality prediction and demand forecasting.
5. **Inventory Optimization**: Analyzed cluster-based buying patterns to recommend inventory levels.

## Project Structure

```
├── data                    # Raw and processed data files
├── notebooks               # Jupyter notebooks for analysis
├── scripts                 # Python scripts for data preprocessing, clustering, and forecasting
├── results                 # Output files and graphs
├── README.md               # Project overview and instructions
└── requirements.txt        # Required Python libraries
```

## Requirements

- **Python**: Ensure you have Python 3.7 or later installed.
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
   - Run the scripts in the `scripts` folder to load and preprocess the data.

3. **Run Analysis**:
   - Execute the Jupyter notebooks in the `notebooks` folder for clustering and forecasting.

4. **View Results**:
   - Check the `results` folder for visualizations and analysis output.

## Results

- **Clustering Insights**: [Summary of clusters]
- **Forecasting Accuracy**: [Key metrics on forecast performance]
- **Inventory Recommendations**: Suggested inventory levels based on demand forecasting.

## Next Steps

- Expand the analysis to include additional data sources for a more comprehensive approach.
- Test alternative clustering and forecasting methods for improved accuracy.
- Implement a real-time monitoring system for inventory adjustments.

## Contributors

- [Ivan Chertoy](your-email@example.com)
- [Emma Le Bars](collaborator-email@example.com)

