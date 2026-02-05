# Consumer Confidence & Well-being Data Cleaning

This description outlines the data cleaning and preparation steps in wb_cc_cleaning.ipynb, which prepares the UK well-being indicators and Consumer Confidence Index (CCI) values for exploratory analysis.
The goal of this notebook is to transform the raw monthly data into a consistent quarterly time series, enabling accurate comparison with other wellbeing datasets.

### Data Source and Objective

- Data Source: The notebook uses the Excel file "WB.xls", specifically the sheet named "Consumer_confidence_month". The WB.xls file was created from cleaning the spreadsheet obtained from the UK government online portal "ukmeasuresofnationalwellbeingfeb20251.xlsx".
- Context: Ensuring time series consistency across datasets. The goal is to harmonize the Consumer Confidence time series (originally monthly) with other well-being variables (like happiness and anxiety), which are provided on a quarterly basis.
- Conversion Methodology: The conversion from monthly to quarterly data is achieved by calculating the mean of the Consumer Confidence values over each three-month period.


### Data Processing Steps (Code Summary)

Imported necessary libraries: pandas and nunmpy

The code performs the following transformations on the original Consumer Confidence DataFrame:

1. Data Loading:
- The file "WB.xls" is read, selecting the "Consumer_confidence_month" sheet.

2. Monthly Grouping:
- A group column is created to group rows into sets of three months (df['group'] = df.index // 3).
- The mean of the Value column is calculated for each three-month group, resulting in the df_grouped DataFrame (quarterly mean).

3. Creation of Quarterly Period Column:
- An array of quarter names (['Apr to June', 'July to Sept', 'Oct to Dec', 'Jan to Mar']) is used to label the new quarters.
- The year is extracted from the first row of each group.
- The Quarter and Year columns are combined to create the final Period column (e.g., 'Apr to June 2011').

4. Final Organization:
- The final DataFrame is reorganized to include only the Period and Mean columns (the average quarterly value).

5. Export:
- The cleaned and grouped DataFrame (df_grouped) is exported to a new Excel file named "Consumer_confidence_quarter.xlsx".

The output file "Consumer_confidence_quarter.xlsx" will have the following structure (showing the first rows):

| Period | Mean |
| :--- | :--- |
| Apr to June 2011 | -25.600000 |
| July to Sept 2011 | -30.200000 |
| Oct to Dec 2011 | -32.000000 |
| Jan to Mar 2012 | -29.466667 |
| Apr to June 2012 | -30.200000 |

# Consumer Confidence and Well-being Analysis

The following description documents the final analysis of the UK's National Well-being variables in relation to Consumer Confidence across different time periods — pre-pandemic, during the pandemic, and post-pandemic.
The notebook wb_cc_analysis.ipynb performs data exploration, visualization, and interpretation to understand how economic and social conditions influence population wellbeing.

### Analysis Objective 

The main goal of this analysis is to investigate::

- Relationships between UK wellbeing indicators (Happiness, Anxiety, Life Satisfaction, Life Worthwhile).
- Differences across the following time periods (pre-pandemic, pandemic, post-pandemic).
- How the Consumer Confidence Index relates to these wellbeing measures.
- Which indicators fluctuated the most before, during, and after pandemic period.

### Input Data Sets

- Primary Data Source: The original dataset is derived from the spreadsheet "ukmeasuresofnationalwellbeingfeb20251.xlsx" (mentioned in the preceding data cleaning notebook).
- Well-being Data: Well-being data is extracted from specific sheets (those containing quarterly happiness and anxiety data).
- Consumer Confidence: The Consumer Confidence time series, which was cleaned and converted to a quarterly frequency in a previous step, is used as a key explanatory variable.

### Key Analysis Steps

1. Data Loading and Combination:

- Loading the quarterly Well-being series and the quarterly Consumer Confidence data.
- Performing a join of the time series based on the quarterly period.

2. Exploratory Data Analysis (EDA):

- Visualization of the time series over time (trends and seasonality).
- Calculation and visualization of the correlation between Consumer Confidence and the Well-being measures.

3. Statistical Modeling:

- Construction of models (e.g., Linear Regression, ARIMA, or Panel models, depending on complexity) to test the predictive power of Consumer Confidence on Well-being.
- Interpretation of model coefficients and assessment of statistical significance.

4. Conclusion:

- Summarizing the findings regarding the relationship between economic sentiment (Consumer Confidence) and subjective well-being.

### Methods & Tools Used

- Pandas for data handling and cleaning
- NumPy, math, statistics
- SciPy (linregress) for linear relationship assessment
- Matplotlib and Seaborn for visualizations
- Heatmap for correlation analysis
- Boxplots comparing wellbeing metrics across period

### Key Findings

- During the pandemic, anxiety levels increased significantly, while happiness decreased.
- In the post-pandemic period, wellbeing indicators partially recovered, but did not fully return to pre-pandemic levels.
- “Life Worthwhile” remained remarkably stable across all three periods.
- There is a noticeable connection between economic sentiment (CC) and wellbeing variables.