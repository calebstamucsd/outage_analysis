# Introduction

The dataset we'll be using for this project contains information on various power outages throughout the United States. Through examining this dataset, we hope to answer the question, "What factors cause more or less customers to be affected by power outages?" By identifying what factors cause power outages to have the most far-reaching effects, we hope to gain new insights as to how to prevent these outages in the future.
In order to perform a holistic analysis, we ought to examine as many potentially relevant columns as possible. In particular, we will be considering the following columns - ['YEAR', 'MONTH', 'U.S._STATE', 'ANOMALY.LEVEL', 'CLIMATE.CATEGORY', 'OUTAGE.START.DATE', 'OUTAGE.START.TIME', 'OUTAGE.RESTORATION.DATE', 'OUTAGE.RESTORATION.TIME', 'CAUSE.CATEGORY', 'CAUSE.CATEGORY.DETAIL', 'HURRICANE.NAMES', 'OUTAGE.DURATION', 'CUSTOMERS.AFFECTED', 'TOTAL.PRICE', 'TOTAL.SALES']. Descriptions of these columns, as well as those included in the original dataset but ommitted from this analysis, can be found [here](https://www.sciencedirect.com/science/article/pii/S2352340918307182>)

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

1. First, I read in the .xlsx file using pd.read_excel(), and filtered to the appropriate columns 
2. Next, I checked each column for missing values. To do so, I counted how many null values already existed in each column, and took a glance at the unique values in each column to see if any missing values were stored under other names. I did not find this to be the case
3. Next, I combined columns that kept the date and time of an outage's start and resolution into single columns of type pd.TimeStamp
4. Finally, I casted columns of unecessary datatypes into more specific types

### Univariate Analysis
<iframe src="assets/bar_chart.html" width=800 height=600 frameBorder=0></iframe>
### Bivariate Analysis
<iframe src="assets/scatter.html" width=800 height=600 frameBorder=0></iframe>
### Interesting Aggregates
## Assessment of Missingness
### NMAR Analysis
### Missingness Dependency
## Hypothesis Testing

<iframe src="assets/OUTAGE.DURATION_missingness.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/TOTAL.PRICE_missingness.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/TOTAL.SALES_missingness.html" width=800 height=600 frameBorder=0></iframe>