# Groundwater Recharge Zone Mapping — Kathmandu Valley

## Overview

This project aims to identify and map potential groundwater recharge zones within the Kathmandu Valley using a machine learning approach. By analyzing various geospatial and environmental factors such as elevation, geology, land use, rainfall, slope, and soil composition, the project develops a classification model to categorize areas into different groundwater recharge suitability classes (e.g., Unsuitable, Poor, Moderate, Good, Excellent).

The final output includes interactive and static maps visualizing these suitability zones, along with a predictive model that can be used for future assessments.

## Project Structure

The notebook is organized into the following sections:

*   **SECTION 1: Install & Import Libraries**: Setup and necessary package imports.
*   **SECTION 2: Load Dataset**: Loading the raw groundwater data.
*   **SECTION 3: Data Cleaning**: Handling missing values and data preprocessing.
*   **SECTION 4: Feature Engineering**: Creating and transforming features for model input.
*   **SECTION 5: Recharge Suitability Score & Target Classes**: Defining the target variable based on a domain-inspired scoring system.
*   **SECTION 6: Feature & Target Selection**: Selecting relevant features and the target for modeling.
*   **SECTION 7: Train / Test Split**: Dividing data for model training and evaluation.
*   **SECTION 8: Model Definitions**: Defining machine learning models (Random Forest, Decision Tree, K-Nearest Neighbors).
*   **SECTION 9: Train, Evaluate, and Compare Models**: Training models and assessing their performance.
*   **SECTION 10: Model Comparison Table**: Presenting model performance metrics in a tabular format.
*   **SECTION 11: Model Comparison Chart**: Visualizing model performance.
*   **SECTION 12: Select Best Model**: Identifying the top-performing model.
*   **SECTION 13: Confusion Matrix (Best Model)**: Visualizing the performance of the best model.
*   **SECTION 14: Feature Importance (Tree-Based Models)**: Analyzing the contribution of each feature to the model's predictions.
*   **SECTION 15: Generate Full-Dataset Predictions**: Applying the best model to the entire dataset.
*   **SECTION 16: Extract Coordinates from .geo Column**: Processing geographical data for mapping.
*   **SECTION 17: Static Scatter Map**: Generating a static visualization of recharge zones.
*   **SECTION 18: Interactive Folium Map**: Creating an interactive map for exploring recharge zones.
*   **SECTION 19: Save Outputs**: Exporting results, figures, and maps.
*   **SECTION 20: Cross-Validation for Model Robustness**: Assessing the model's generalization ability.

## Data

The primary dataset used is `kathmandu_raw_groundwater_data.csv`, which contains various environmental and geographical parameters for locations within the Kathmandu Valley.

**Columns include:**
*   `system:index`: Unique identifier (removed during cleaning).
*   `elevation`: Altitude above sea level.
*   `geology`: Geological classification of the area.
*   `landuse`: Land use type (e.g., urban, agricultural, forest).
*   `rainfall`: Average rainfall.
*   `slope`: Terrain slope.
*   `soil_clay`: Percentage of clay in the soil.
*   `.geo`: GeoJSON string containing geographical coordinates.

## Methodology

1.  **Data Preprocessing**: Raw data is loaded, `system:index` is dropped, and any rows with missing values are removed.
2.  **Feature Engineering**: Several features (`slope_norm`, `soil_conductivity`, `rainfall_norm`, `geology_norm`, `landuse_norm`) are engineered and normalized. `slope` and `soil_clay` are inverted to align with recharge suitability (flatter terrain and lower clay content indicate better infiltration).
3.  **Recharge Suitability Scoring**: A composite `recharge_score` is calculated using domain-inspired weights for the engineered features. This score quantifies the potential for groundwater recharge.
4.  **Target Class Generation**: The `recharge_score` is then binned into 5 balanced classes (Unsuitable, Poor, Moderate, Good, Excellent) using quantile-based categorization.
5.  **Model Training**: Random Forest, Decision Tree, and K-Nearest Neighbors classifiers are trained on the processed data.
6.  **Model Evaluation**: Models are evaluated based on Accuracy, Weighted F1-score, Macro F1-score, Classification Reports, and Confusion Matrices.
7.  **Best Model Selection**: The model with the highest performance is selected for further analysis.
8.  **Feature Importance**: For tree-based models, feature importance is analyzed to understand key contributing factors.
9.  **Predictions and Mapping**: The best model is used to predict recharge suitability for the entire dataset. Geographical coordinates are extracted to visualize these predictions on static scatter maps and interactive Folium maps.
10. **Cross-Validation**: Stratified K-Fold cross-validation is performed to ensure the model's robustness and generalization capabilities.

## Results

The analysis identifies **Random Forest Classifier** as the best-performing model for predicting groundwater recharge suitability, achieving an accuracy of approximately **[Insert Best Model Accuracy]**.

Key findings and visualizations include:

*   **Class Distribution**: A bar chart showing the distribution of the 5 recharge suitability classes.
*   **Model Comparison**: A bar chart comparing the accuracy and F1-scores of all trained models.
*   **Confusion Matrix**: A detailed breakdown of the best model's classification performance.
*   **Feature Importance**: A chart indicating the most influential factors for groundwater recharge (e.g., slope, land use, elevation).
*   **Recharge Maps**: Static and interactive maps illustrating the predicted groundwater recharge zones across the Kathmandu Valley.

## How to Reproduce

1.  **Clone the Repository**: 
    ```bash
    git clone [Your GitHub Repository URL]
    cd [Your Repository Name]
    ```
2.  **Open in Google Colab**: Upload the `[Your_Notebook_Name].ipynb` file to Google Colab.
3.  **Ensure Data is Present**: Make sure the `kathmandu_raw_groundwater_data.csv` is in the `/content/` directory within Colab (it should be if you followed the previous instructions for GitHub upload and downloaded it).
4.  **Run All Cells**: Execute all cells in the notebook sequentially.

## Outputs

The following files are generated and saved during the notebook execution:

*   `/content/cleaned_groundwater_data.csv`: The cleaned dataset.
*   `/content/groundwater_recharge_predictions.csv`: The dataset with predicted recharge classes and geographical coordinates.
*   `/content/groundwater_recharge_map.html`: An interactive Folium map of recharge zones.
*   `/content/figures/class_distribution.png`: Bar chart of recharge class distribution.
*   `/content/figures/model_comparison.png`: Bar chart comparing model performance.
*   `/content/figures/confusion_matrix.png`: Confusion matrix for the best model.
*   `/content/figures/feature_importance.png`: Feature importance chart for tree-based models.
*   `/content/figures/recharge_map.png`: Static scatter map of recharge zones.
