# ReCell – Dynamic Pricing for Used Devices – A Predictive Modeling Approach

This repository contains the analysis and model development for the ReCell project, which focuses on developing a dynamic pricing strategy for used and refurbished devices. The goal is to predict the resale value of used phones and tablets using a linear regression model and to uncover the key factors that drive pricing in the secondary market.

## Table of Contents

- [Overview](#overview)
- [Data Description](#data-description)
- [Project Structure](#project-structure)
- [Environment & Installation](#environment--installation)
- [Analysis and Modeling](#analysis-and-modeling)
  - [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
  - [Data Preprocessing & Feature Engineering](#data-preprocessing--feature-engineering)
  - [Model Building and Evaluation](#model-building-and-evaluation)
- [Key Findings & Recommendations](#key-findings--recommendations)
- [Usage](#usage)
- [License](#license)

## Overview

The used device market has seen tremendous growth over the past decade, with forecasts predicting it to reach approximately €52.7 billion by 2023. ReCell aims to tap into this market by developing a predictive model that can dynamically price used devices based on their specifications, age, and market trends. This project uses a dataset of used devices (stored in `used_device_data (1).csv`) collected in 2021, along with detailed attributes including brand, operating system, hardware specifications, and pricing information.

## Data Description

The dataset (`used_device_data (1).csv`) includes 15 key columns such as:

- **brand_name**: Manufacturer of the device.
- **os**: Operating system (e.g., Android, iOS).
- **screen_size**: Screen size in centimeters.
- **4g/5g**: Connectivity capabilities.
- **main_camera_mp / selfie_camera_mp**: Camera resolutions in megapixels.
- **int_memory**: Internal memory (ROM) in GB.
- **ram**: RAM in GB.
- **battery**: Battery capacity in mAh.
- **weight**: Device weight in grams.
- **release_year**: Year of release.
- **days_used**: Number of days the device has been used.
- **normalized_new_price**: Normalized price of a new device (in euros).
- **normalized_used_price**: Normalized resale price (in euros).

## Project Structure

```
ReCell-Dynamic-Pricing/
├── data/
│   └── used_device_data (1).csv         # Dataset for analysis
├── notebooks/
│   └── ReCell_Project_Notebook.ipynb      # Jupyter notebook containing full analysis
├── ReCell Project Code.pdf                # Detailed code walkthrough and analysis
├── ReCell Project PowerPoint Presentation.pdf   # Presentation with key findings and recommendations
├── README.md                              # This file
└── requirements.txt                       # List of required libraries and versions
```

## Environment & Installation

To replicate the analysis, you will need Python 3.x and the following libraries:

- numpy
- pandas
- matplotlib
- seaborn
- scikit-learn
- statsmodels
- scipy

Install the required packages using:

```bash
pip install -r requirements.txt
```

The `requirements.txt` file includes the following (versions used in the project):

```text
scikit-learn==<version>
seaborn==<version>
matplotlib==<version>
numpy==<version>
pandas==<version>
statsmodels==<version>
scipy==<version>
```

## Analysis and Modeling

### Exploratory Data Analysis (EDA)

The EDA process involved:
- **Univariate Analysis**: Visualizing distributions of prices, screen size, camera specifications, memory, and other key features.
- **Bivariate Analysis**: Investigating relationships such as the correlation between the new and used prices, the impact of hardware specs (RAM, camera, battery) on resale value, and differences across brands and connectivity (4G vs. 5G).
- **Market Insights**: Observing that used devices are generally priced 20–25% lower than their new counterparts, with factors like camera quality, RAM, and device weight playing significant roles.

### Data Preprocessing & Feature Engineering

Key steps in data preprocessing included:
- **Missing Value Imputation**: Hierarchical imputation was performed using medians, grouped by release year and brand, followed by final imputation using the overall median.
- **Feature Engineering**: A new feature, `years_since_release`, was derived from the release year (using 2021 as the baseline) to capture device age and depreciation.
- **Encoding**: Categorical features (brand, OS, 4G, and 5G) were converted into dummy variables for regression analysis.

### Model Building and Evaluation

A linear regression (OLS) model was developed with the following highlights:
- **Dependent Variable**: `normalized_used_price`
- **Key Predictors**: `normalized_new_price`, camera specifications (`main_camera_mp` and `selfie_camera_mp`), `ram`, `weight`, and `years_since_release`.
- **Model Performance**: 
  - R-squared on training data: ~0.85 
  - Test data R-squared: ~0.83 
  - RMSE: ~0.23 
  - MAPE: ~4.3%
- **Assumptions Check**: 
  - Multicollinearity was addressed by dropping variables with high VIF scores.
  - Residual analysis indicated acceptable linearity, normality, and homoscedasticity.

## Key Findings & Recommendations

- **Influential Features**: The resale price is heavily influenced by the new price, camera quality, RAM, and weight. Devices with higher “years_since_release” tend to have lower resale values.
- **Connectivity Impact**: 4G capability has a positive effect on resale value, while 5G is currently associated with lower prices (likely due to lower market penetration).
- **Brand Effect**: Brands such as Nokia, Xiaomi, and Asus positively influence used device pricing.
- **Business Strategy**: 
  - Optimize pricing for devices with superior camera features and higher RAM.
  - Focus on sourcing and promoting 4G-capable devices.
  - Monitor 5G trends for future pricing strategy adjustments.
  - Account for depreciation using the device’s age to adjust pricing dynamically.

## Usage

1. **Data Preparation**: Place the `used_device_data (1).csv` file in the `data/` folder.
2. **Run the Notebook**: Open the Jupyter notebook in the `notebooks/` directory to view the full analysis and model building steps.
3. **Review Documentation**: For a detailed understanding of the code and results, refer to the accompanying PDF documents:
   - [ReCell Project Code.pdf](./ReCell%20Project%20Code.pdf)
   - [ReCell Project PowerPoint Presentation.pdf](./ReCell%20Project%20PowerPoint%20Presentation.pdf)

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---
