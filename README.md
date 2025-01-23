# AnalysisWork.R

## Overview

`AnalysisWork.R` is an R script designed to analyze an insurance dataset. It performs exploratory data analysis (EDA), data visualization, and statistical modeling to gain insights into the dataset. The script includes various operations such as data summarization, visualization, and predictive modeling using linear regression.

## Features

- **Data Loading and Inspection:**

  - Reads the dataset from a CSV file.
  - Displays the first few rows and column names.
  - Checks for missing values and data types.

- **Descriptive Statistics:**

  - Calculates mean, median, and standard deviation for key numeric columns.
  - Counts unique values in categorical columns.

- **Data Visualization:**

  - Histograms for age and BMI distribution.
  - Scatter plots to visualize relationships (e.g., BMI vs. Charges).
  - Box plots to compare distributions based on categories (e.g., charges by smoker status and region).
  - Heatmaps for correlation matrix visualization.
  - Violin plots for charge distributions across different regions.

- **Data Transformation:**

  - Converts categorical variables using one-hot encoding.
  - Normalizes numerical columns to a 0-1 scale.

- **Statistical Analysis & Machine Learning:**

  - Linear regression to predict insurance charges based on age, BMI, children, and smoker status.
  - Root Mean Squared Error (RMSE) calculation for model evaluation.
  - Confidence intervals for average charges by region.
  - T-test to analyze significant differences in charges between smokers and non-smokers.
  - Feature importance analysis using decision trees.

## Requirements

To run this script, ensure that the following R packages are installed:

- `ggplot2`
- `dplyr`
- `data.table`
- `corrplot`
- `rpart`

You can install them using:

```r
install.packages(c("ggplot2", "dplyr", "data.table", "corrplot", "rpart"))
```

## Usage

1. Update the CSV file path in the script:
   ```r
   df <- read.csv("C:/Users/USER/Downloads/insurance.csv")
   ```
2. Run the script in an R environment (e.g., RStudio).
3. The script will print statistical summaries and generate various plots for analysis.

## Output

- Summary statistics printed in the console.
- Various plots for data visualization.
- Regression model output and predictions.


![Image2](https://github.com/user-attachments/assets/d723760f-cdec-4ac1-b73d-ea256883b53d)
![Image1](https://github.com/user-attachments/assets/977b0bf7-7522-476f-ad07-2eb36d9b8a08)
![Image10](https://github.com/user-attachments/assets/2b3e8d2c-7f3c-4903-a3b9-74cbd41c1c7b)
![Image9](https://github.com/user-attachments/assets/def14292-8d95-4e26-84f3-14fac4849379)
![Image8](https://github.com/user-attachments/assets/dd2435e8-f272-4614-96ed-66e018d92497)
![Image7](https://github.com/user-attachments/assets/ee5b3c8a-8699-46e6-a8ee-1576634d5477)
![Image6](https://github.com/user-attachments/assets/20ff96d9-8734-42f2-a453-e696c0d67bdf)
![Image5](https://github.com/user-attachments/assets/dfc7105f-ca1c-4dce-8f2f-b4762f466463)
![Image4](https://github.com/user-attachments/assets/96d12eb7-4757-4854-83bc-c735feb6a7ce)
![Image3](https://github.com/user-attachments/assets/669f8a55-c218-4988-87e9-5a7d304ac1e3)
