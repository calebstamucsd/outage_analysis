# Outage Analysis

## Introduction

The dataset we'll be using for this project contains information on various power outages throughout the United States. Through examining this dataset, we hope to answer the question, "What factors cause more or less customers to be affected by power outages?" By identifying what factors cause power outages to have the most far-reaching effects, we hope to gain new insights as to how to prevent these outages in the future.

In order to perform a holistic analysis, we ought to examine as many potentially relevant columns as possible. In particular, we will be considering the following columns - ['YEAR', 'MONTH', 'U.S._STATE', 'ANOMALY.LEVEL', 'CLIMATE.CATEGORY', 'OUTAGE.START.DATE', 'OUTAGE.START.TIME', 'OUTAGE.RESTORATION.DATE', 'OUTAGE.RESTORATION.TIME', 'CAUSE.CATEGORY', 'CAUSE.CATEGORY.DETAIL', 'HURRICANE.NAMES', 'OUTAGE.DURATION', 'CUSTOMERS.AFFECTED', 'TOTAL.PRICE', 'TOTAL.SALES']. 

Descriptions of these columns, as well as those included in the original dataset but ommitted from this analysis, can be found [here](https://www.sciencedirect.com/science/article/pii/S2352340918307182>)

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning
|    |   YEAR |   MONTH | U.S._STATE   |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   CUSTOMERS.AFFECTED |   TOTAL.PRICE |   TOTAL.SALES | OUTAGE.START        | OUTAGE.RESTORATION   |
|---:|-------:|--------:|:-------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|---------------------:|--------------:|--------------:|:--------------------|:---------------------|
|  0 |   2011 |       7 | Minnesota    |            -0.3 | normal             | severe weather     | nan                     |               nan |              3060 |                70000 |          9.28 |       6562520 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|  1 |   2014 |       5 | Minnesota    |            -0.1 | normal             | intentional attack | vandalism               |               nan |                 1 |                  nan |          9.28 |       5284231 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|  2 |   2010 |      10 | Minnesota    |            -1.5 | cold               | severe weather     | heavy wind              |               nan |              3000 |                70000 |          8.15 |       5222116 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|  3 |   2012 |       6 | Minnesota    |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |              2550 |                68200 |          9.19 |       5787064 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|  4 |   2015 |       7 | Minnesota    |             1.2 | warm               | severe weather     | nan                     |               nan |              1740 |               250000 |         10.43 |       5970339 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |

1. First, I read in the .xlsx file using pd.read_excel(), and filtered to the appropriate columns 
2. Next, I checked each column for missing values. To do so, I counted how many null values already existed in each column, and took a glance at the unique values in each column to see if any missing values were stored under other names. I did not find this to be the case
3. Next, I combined columns that kept the date and time of an outage's start and resolution into single columns of type pd.TimeStamp
4. Finally, I casted columns of unecessary datatypes into more specific types

### Univariate Analysis
<iframe src="assets/bar_chart.html" width=800 height=600 frameBorder=0></iframe>
This is a bar chart of the different cause categories for all of the recorded power outages. Understanding which categories our dataset is skewed towards can contextualize further analysis.

### Bivariate Analysis
<iframe src="assets/scatter.html" width=800 height=600 frameBorder=0></iframe>
This is a scatter plot that compares the number of customers affected to the price of electricity in the region where the outage occured. We might expect that areas with more expensive electricity would have less customers affected, but the scatter plot does not demonstrate such an obvious relationship.

### Interesting Aggregates
| CLIMATE.CATEGORY   |   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public appeal |   severe weather |   system operability disruption |\n|:-------------------|--------------------:|------------------------:|---------------------:|------------:|----------------:|-----------------:|--------------------------------:|\n| cold               |             93920.3 |                0        |              76.2712 |    6615.29  |         7016.67 |           165993 |                        207286   |\n| normal             |            126292   |                0.333333 |            1521.89   |    9255.83  |         7859.6  |           195791 |                        249994   |\n| warm               |             74708.3 |                0        |            4474.02   |     758.125 |          nan    |           205123 |                         86869.8 |

This dataframe, obtained by using the pivot_table method, tells us the mean number of customers affected by each cause for a power outage in each climate classification. This helps us to identify which cause and climatess categories tend to have the most signifcant effects.

## Assessment of Missingness
### NMAR Analysis
I do not believe that any of the columns relevant to my data analysis are NMAR. Many of the columns are MD, like CAUSE.CATEGORY.DETAIL or HURRICANE.NAMES. I thought that the column OUTAGE.DURATION might have a chance of being NMAR, but nothing about the data generation process leads me to believe that the presence of missing values in this column are dependent on the values themselves.

### Missingness Dependency
Here, we find that the presence of missing values in the CUSTOMERS.AFFECTED column is a result of the OUTAGE.DURATION column.
Particularly, we have a p-value of 0.014, which would be considered significant at most commonly used significance levels.
<iframe src="assets/OUTAGE.DURATION_missingness.html" width=800 height=600 frameBorder=0></iframe>

## Hypothesis Testing
Null Hypothesis: There is no significant difference in the average amount of customers affected by power outages in California and Texas.
Alternative Hypothesis: Power outages in Texas affect more customers, on average, than power outages in Texas.
P-value: 0.544
So, we fail to reject the null hypothesis.

This is a good test to perform because it is holistic and topical. The Texas Interconnection Power Grid is maintained as a separate power grid from the rest of the nation, a decision often criticized after mass outages in Texas such as in the Winter of 2021. This permutation test answers whether the factor of Texas being on a separate power grid might result in an increase in the amount of customers affected.