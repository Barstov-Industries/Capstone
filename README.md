# Retail Inventory Optimization for H&M Online Warehouse

## Project Overview

This project optimizes inventory for H&M’s online warehouse by forecasting product demand. The goal is to ensure optimal stock levels, focusing on commonly sold items and avoiding both overstock and stockouts. The project uses an ensemble modeling approach for accurate demand prediction and includes an inventory rebalancing feature.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Objective](#objective)
3. [Data](#data)
4. [Methodology](#methodology)
5. [Modeling](#modeling)
6. [Requirements](#requirements)
7. [Results](#results)
8. [Next Steps](#next-steps)
9. [Contributors](#contributors)

## Objective

The project’s primary objectives are to:
- **Predict weekly demand** for products based on type, color, price, and seasonality.
- **Optimize inventory levels** to meet demand while avoiding overstock and stockouts.
- **Rebalance inventory** based on seasonal demand patterns to prevent stockouts of high-demand items.

## Data

- **Source**: H&M transaction data from September 2018 to March 2020.
- **Content**: The dataset contains transaction data, and features were engineered to predict demand and support inventory optimization.
- **Processed Data**: Data was cleaned, deduplicated, and organized into weekly periods, with features engineered for better forecasting.

## Methodology

1. **Data Preprocessing**: 
   - Filtered data up to March 2020 and sorted by product and week.
   - Identified peak seasons using quantile-based thresholds for each product type and color.
   
2. **Feature Engineering**:
   - **Lag Features**: Added lag features to capture recent sales trends.
   - **Seasonality**: Created month and peak season indicators (`is_peak_season`).
   - **Price Scaling**: Adjusted the price to match demand predictions.

3. **Modeling**:
   
**Ensemble Model**:  
- Combined predictions from three base models:  
  - **Random Forest Regressor**  
  - **Linear Regression**  
  - **MLP Regressor**  

**Meta-model**:  
- A **Random Forest Regressor** was employed as the meta-model.  
- This approach combined the base model predictions to improve overall forecasting accuracy.
  
5. **Inventory Rebalancing**:
   - A dynamic rebalancing flag was created based on predicted low demand, which helps adjust stock levels for low-performing items.
   
## Modeling

- **Feature Columns**: The following features were used in the model:
  ```python
  feature_columns = ['product_type_no', 'colour_group_code', 'average_price',
                     'lag_units_sold_1week', 'lag_units_sold_2weeks', 'month', 'is_peak_season']
  ```

- **Ensemble Model**: Combined **Random Forest**, **Linear Regression**, and **MLP Regressor** for robust weekly demand forecasting, with Random Forest as the meta-model.
- **Train, Validation, and Test Splits**:
  - Training: 2019 data.
  - Validation: January 2020 data.
  - Testing: February 2020 data.

- **Rebalancing**: A dynamic low-demand threshold was set based on seasonality and past sales to flag products that require rebalancing.

## Requirements

- **Python 3.7+**
- **Libraries**: Install dependencies using the `requirements.txt` file:

    ```bash
    pip install -r requirements.txt
    ```

## Results

- **Model Performance**:
  - **Extended Validation MAE**: 9.36
  - **Extended Validation RMSE**: 26.61
  - **Test MAE**: 23.65
  - **Test RMSE**: 75.53

- **Predicted Inventory Needs (Test Period)**: 
  - The model predicted the required inventory levels across various product types and colors for the test period.
  - Example:
    ```plaintext
    product_type_no | colour_group_code | predicted_inventory_needs
    -1               | 6                 | 291
    -1               | 7                 | 173
    515              | 12                | 2
    ```

- **Potential Rebalance Needs**:
  - Items flagged for rebalancing based on predicted low demand during non-peak seasons.
  - Example:
    ```plaintext
    product_type_no | colour_group_code | predicted_inventory_needs | rebalance_units
    -1               | 42                | 1                          | 1
    57               | 4                 | 4                          | 4
    ```

- **Total Predicted Inventory Needs**: 881,262 units for the test period.
- **Total Rebalance Needs**: 25,806 units requiring adjustments.

## Next Steps

- **Improve Model Accuracy**: Explore incorporating additional features like promotional data or competitor stock levels.
- **Deploy Model**: Implement the model for real-time inventory forecasting and dynamic updates.
- **Refine Rebalancing Logic**: Enhance the rebalance flag system with more precise seasonal adjustments.

## Contributors
- [Ivan Chertov](ivanchertov86@gmail.com)
- <a href="https://www.linkedin.com/in/ivan-chertov/">
  <img src="https://upload.wikimedia.org/wikipedia/commons/c/ca/LinkedIn_logo_initials.png" alt="LinkedIn" width="20" height="20"/>
</a>
- [Emma Le Bars](lebars.emma@gmail.com)
- <a href="https://www.linkedin.com/in/emma-le-bars/">
  <img src="https://upload.wikimedia.org/wikipedia/commons/c/ca/LinkedIn_logo_initials.png" alt="LinkedIn" width="20" height="20"/>
</a>
