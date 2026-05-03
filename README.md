# Credit Card Fraud Detection
An end-to-end data analytics capstone project analyzing 339,607 credit card transactions across the western United States to identify patterns, build a rule-based risk scoring model, and visualize insights.
## Table of Contents
 1. [Project Overview](#project-overview)
 2. [Datasettion Description](Dataset Description)
 3. Methodology & Workflow
 4. Key Findings
 5. Fraud Risk Scoring Model
 6. Model Performance
 7. Visualizations & Dashboard
 8. Project Structure
 9. How to Use
 10. Limitations
 11. Author & Contact
## Project Overview
Credit card fraud poses a significant financial risk and erodes customer trust. This project explores transaction data to identify risk factors, test key hypotheses, and build a scoring model that flags fraudulent transactions with a high recall rate.
## Dataset Description
 * **Source**: Adapted from Kaggle and DataCamp.
 * **Volume**: 339,607 transactions.
 * **Target Variable**: is_fraud (1 = Fraud, 0 = Legitimate).
 * **Overall Fraud Rate**: 0.52% (highly imbalanced dataset).
 * **Key Columns**:
   * amt: Transaction amount in USD.
   * Is_Night: Categorical (Day / Night).
   * category: Transaction category (e.g., shopping_net, misc_net).
   * Cutomer_age: Derived customer age from date of birth.
   * Dist_km: Distance between customer and merchant.
## Methodology & Workflow
The analysis was performed across three distinct phases:
 1. **Phase 1: Exploratory Data Analysis (EDA)**
   * Cleaned the dataset and handled missing values.
   * Derived features: Cutomer_age, transaction_hour, and Is_Night.
   * Evaluated descriptive statistics (Mean, Median, and Outliers).
 2. **Phase 2: Statistical Hypothesis Testing**
   * Tested differences in age, transaction amount, and time of day to ensure patterns were not random using the Analysis ToolPak.
 3. **Phase 3: Modeling & Evaluation**
   * Developed a rule-based fraud scoring model.
   * Created a Confusion Matrix to evaluate classification performance.
## Key Findings
 1. **High-Value Transactions Drive Fraud**: Transactions > \$500 show a fraud rate of **20.70%** (compared to the baseline of 0.52%).
 2. **Online Categories are High Risk**: The categories shopping_net and misc_net exhibit the highest rates of fraud (up to 1.44%).
 3. **Late-Night Spikes**: Fraud peaks between 10 PM and 11 PM with a fraud rate exceeding **2.6%**.
 4. **Geographic Variation**: Alaska shows the highest state-level fraud rate at 1.69%.
 5. **Distance Anomalies**: Fraudulent transactions show a significantly higher average distance between customer location and merchant.
## Fraud Risk Scoring Model
A rule-based scoring mechanism was built in Excel to score each transaction based on risk characteristics:
```excel
=IF([@amt]>500,3,0) + IF([@Amt_outliers]="Outlier",2,0) + IF([@Is_Night]="Night",2,0) + IF(OR([@category]="shopping_net",[@category]="misc_net"),2,0) + IF([@Dist_km]>100,3,0) + IF(OR([@Cutomer_age]<25,[@Cutomer_age]>65),1,0)

```
The prediction rule flags transactions reaching a threshold score of 4 or greater:
```excel
=IF([@fraud_score]>=4, 1, 0)

```
## Model Performance
 * **Accuracy**: 66.65%
 * **Precision**: 2.80%
 * **Recall (Sensitivity)**: 77.50%
 * **F1-Score**: 5.46%
> **Interpretation**: The model identifies the vast majority of all actual fraud events (Recall of 77.5%), fulfilling the objective to catch suspicious events, though it generates a high proportion of false alarms (Precision of 2.8%).
> 
## Visualizations & Dashboard
The Power BI dashboard provides an interactive summary of our findings across four distinct pages:
### Page 1: Executive Overview

*Highlights high-level KPIs including the total fraud amount, aggregate transaction numbers, and overall recall.*
### Page 2: Transaction & Risk Category Analysis

*Explores the performance of specific product and internet-based categories.*
### Page 3: Geographic & Spatial Analysis

*Tracks anomalies and distances across cities and states like Alaska.*
### Page 4: Time-Based & Demographic Trends

*Visualizes hourly and demographic risk factors.*
## Project Structure
```text
├── data/
│   └── transaction_sample.csv       <- First 1,000 rows of the dataset
├── reports/
│   └── Fraud_Analysis_Report.pdf    <- Full methodology report and findings
├── dashboard/
│   ├── Fraud_Dashboard.pbix         <- Power BI Dashboard file
│   └── dashboard_exports.pdf        <- Exported views of all 4 pages
├── assets/
│   ├── executive_overview.png       <- Dashboard screenshot
│   ├── category_insights.png        <- Dashboard screenshot
│   ├── geospatial_map.png           <- Dashboard screenshot
│   └── temporal_trends.png          <- Dashboard screenshot
└── README.md

```
## How to Use
 1. **Clone the repository**:
   ```bash
   git clone https://github.com/SediqNuhu/credit-card-fraud-detection.git
   
   ```
 2. **View the Power BI dashboard**:
   * Open the .pbix file using Microsoft Power BI Desktop.
 3. **Analyze the Data**:
   * Open transaction_sample.csv in your spreadsheet editor (Excel) to review the fraud scoring columns.
## Limitations
 * **Imbalanced Dataset**: With a low prevalence of actual fraud (0.52%), the model exhibits low precision.
 * **Rule-Based Model**: The threshold logic is static and cannot automatically capture complex, nonlinear behaviors.
 * **Geographical Approximations**: Distance values use latitude/longitude centroids rather than precise multi-modal travel routes.
## Author & Contact
**Nuhu Abubakar Sediq** * **Role**: Data Management Executive & Data Analyst
 * **LinkedIn**: Nuhu Abubakar Sediq
 * **GitHub**: Abubakar Nuhu
