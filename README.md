# Credit Card Fraud Detection
An end-to-end data analytics capstone project analyzing 339,607 credit card transactions across the western United States to identify patterns, build a rule-based risk scoring model, and visualize insights.
![#Cedit-card-fraud-detecttion](https://github.com/absediqni/credit-card-fraud-detection/blob/main/assets/dimage.gif)

## Table of Contents
 1. [Project Overview](#Project-Overview)
 2. [Dataset Description](#Dataset-Description)
 3. [Methodology & Workflow](#Methodology-&-Workflow)
 4. [Key Findings](#Key-Findings)
 5. [Fraud Risk Scoring Model](#Fraud-Risk-Scoring-Model)
 6. [Model Performance](#Model-performance)
 7. [Visualizations & Dashboard](#Visualizations-&-Dashboard)
 8. [Project Structure](#Project-Structure)
 9. [How to Use](#How-to-use)
 10. [Tools used](#Tools-used)
 11. [Limitations](#Limitations)
 12. [Author & Contact](#Author-&-Contact)
## Project Overview
Credit card fraud poses a significant financial risk and erodes customer trust. This project explores transaction data to identify risk factors, test key hypotheses, and build a scoring model that flags fraudulent transactions with a high recall rate.
## Dataset Description
 * **Source**: Adapted from [Kaggle](https://www.kaggle.com/datasets/kartik2112/fraud-detection) and [DataCamp](https://www.datacamp.com/datalab/w/a0f4d3c5-f954-493b-bb2d-5093769ed232/edit).
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
   * Tested differences in age, transaction amount, and time of day to ensure patterns were not random using functions and forulas.
 3. **Phase 3: Modeling & Evaluation**
   * Developed a rule-based fraud scoring model.
   * Created a Confusion Matrix to evaluate classification performance.
## Key Findings
 1. **High-Value Transactions Drive Fraud**: Transactions > \$500 show a fraud rate of **20.70%** (compared to the baseline of 0.52%).
 2. **Online Categories are High Risk**: The categories shopping_net and misc_net exhibit the highest rates of fraud (up to 1.44%).
 3. **Late-Night Spikes**: Fraud peaks between 10 PM and 11 PM with a fraud rate exceeding **2.6%**.
 4. **Geographic Variation**: Alaska shows the highest state-level fraud rate at **1.69%**.
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
 * **Accuracy**: 82.74%
 * **Precision**: 2.32%
 * **Recall (Sensitivity)**: 77.50%
 * **F1-Score**: 4.50%
> **Interpretation**: The model identifies the vast majority of all actual fraud events (Recall of 77.5%), fulfilling the objective to catch suspicious events, though it generates a high proportion of false alarms (Precision of 2.32%).
> 
## Visualizations & Dashboard
The Power BI dashboard provides an interactive summary of our findings across four distinct pages:
### Page 1: Executive Overview
![#overview](https://github.com/absediqni/credit-card-fraud-detection/blob/main/assets/overview.png)
*Highlights high-level KPIs including the total fraud amount, aggregate transaction numbers, and overall recall.*
### Page 2: Transaction Deep-Dive
![deep_dive](https://github.com/absediqni/credit-card-fraud-detection/blob/main/assets/deep_dive.png)
*Explores the performance of specific product and internet-based categories.*
### Page 3: Customer Risk Profile
![risk_profile](https://github.com/absediqni/credit-card-fraud-detection/blob/main/assets/risk_profile.png)
*Tracks anomalies and distances across cities and states like Alaska.*
### Page 4: Model Performance
![model_performance](https://github.com/absediqni/credit-card-fraud-detection/blob/main/assets/model_performance.png)
*Visualizes hourly and demographic risk factors.*
* [View Live Interactive Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMjFjNzU2YTktZjI2NC00MzQ4LThlYmItMDc3OWRkMzFkMGNkIiwidCI6ImI5ZDkyNjZmLWU2ZmEtNGU5Ni05YTE2LWE4MjQ0OTY3YTMzZSJ9)
## Project Structure
```text
├── data/
│   └── Credit_card_sample_dataset.csv <- First 1,000 rows of the dataset)
├── reports/
│   └── Project_Report.pdf    <- Full methodology report and findings
├── dashboard/
│   └── dashboard_exports.pdf        <- Exported views of all 4 pages
├── assets/
│   ├── executive_overview.png       <- Dashboard screenshot
│   ├── Deep_dive.png        <- Dashboard screenshot
│   ├──  risk_profile.png           <- Dashboard screenshot
│   └── model_performance.png          <- Dashboard screenshot
└── README.md

```
## How to Use
### Power BI Dashboard (.pbix)
* **Software** Microsoft Power BI Desktop (Free).
* **Interaction:**
  * Open the file in the ![Power BI file/Dashboard folder](https://drive.google.com/file/d/1cGym5XEFuuvcb3JayOaiG7SxnLHw02ma/view?usp=drive_link) to explore the 4-page report.
  * Use the *Bookmark Buttons* (Default, Fraud-Only, High-Risk) to toggle pre-set analytical views.
  * Interact with *Slicers* and *Tooltips* to filter data by date, category, or geography.
  * Use the *navigation* buttons to move across pages
### Excel Scoring Logic (.csv)
* **Software** Microsoft Excel.
* **Interaction:**
  * Open the dataset in the /data folder to view transaction-level details.
  * Review the Scoring Columns at the far right to see the Excel formulas calculating fraud risk.
  * Test the logic by modifying transaction amounts to see the Fraud Score update in real-time.

## Tools used 
  **Excel | Power BI | GitHub**
  * **Microsoft Excel** was used for data cleaning and modeling. This included handling missing values, removing duplicates, transforming raw data into structured formats, and building logical data models for analysis.
  * **Power BI** was used for data visualization and reporting. Interactive dashboards were created to present key insights, trends, and performance metrics, enabling clear and data-driven decision-making.
  * **GitHub** — Used to host the data analysis project, manage version control, track code changes, and maintain collaboration workflows.

## Limitations
 * **Imbalanced Dataset**: With a low prevalence of actual fraud (0.52%), the model exhibits low precision.
 * **Rule-Based Model**: The threshold logic is static and cannot automatically capture complex, nonlinear behaviors.
 * **Geographical Approximations**: Distance values use latitude/longitude centroids rather than precise multi-modal travel routes.
   
## Author & Contact
**Nuhu Abubakar Sediq** 
 * **Role**: Data Management Executive & Data Analyst
 * **LinkedIn**: [Nuhu Abubakar](https://www.linkedin.com/in/absediqni/)
 * **Contact**: [Send me a mail](mailto:absediqni@gmail.com)
