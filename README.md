# Outage-State-Predictor
DSC80 Project for UCSD

By Albert Henderson

# Introduction

For this project, I will be analyzing a data set containing major power outages in the United State from January 2000 to July 2016. This dataset was obtained through Purdue University`s Laboratory for Advancing Sustainable Critical Infrastructure, at https://engineering.purdue.edu/LASCI/research-data/outages.

This dataset contains various information about each power outage such as the State, climate, region, and postal code of the outage. As well as the number of people affected, the population of where it happened, and the cause of the major outage.

The purpose behind this project is that I want to answer the question, what regions in the U.S are most impacted by power outages. This question is meaningful to me as it can give insight into what parts of the country should be given resources in order to improve their electrical infrastrucutre.

This dataset has 1537 rows and 57 columns, however I will only be using these columns for this project

Colons can be used to align columns.

| Column        | Description   |
| ------------- |:-------------:|
| Year     | Year of the outage
| Month      | Month of the outage     |
| U.S._STATE | State the outage occured in      |
| Postal Code | The States Postal Code |
| OUTAGE.START.TIME | Time the outage started |
| OUTAGE.START.DATE | The date the outage started |
| OUTAGE.DURATION | How long the outage lasted for (in minutes)|
| CLIMATE.REGION | The Region in the U.S the outage occured |
| OUTAGE.RESTORATION.DATE | Date the outage was resolved |
| OUTAGE.RESTORATION.TIME | Time the outage was resolved |
| CAUSE.CATEGORY | What caused the outage |
| TOTAL.PRICE | The states average price for electricity in cents/kilowatts-hour |
| TOTAL.SALES | The states electricity sales for that year in Megawatts/hour |
| TOTAL.CUSTOMERS | Total number of customers affected |
| POPULATION | Population of the affected state |
| CUSTOMERS.AFFECTED | Number of customers affected by the outage |
| PCT.LAND | Percentage of the state that`s land |

# Data Cleaning and Analysis

## Data Cleaning

1. First, I dropped all columns I found to have a large number of missing values and then removed columns I found to be irrelevant to my proposed questions and only kept the columns I listed above. Those being, YEAR, MONTH, U.S._STATE, CLIMATE.REGION, OUTAGE.START.DATE, OUTAGE.START.TIME, OUTAGE.RESTORATION.DATE, OUTAGE.RESTORATION.TIME, CAUSE.CATEGORY, OUTAGE.DURATION, CUSTOMERS.AFFECTED, TOTAL.PRICE, TOTAL.SALES, TOTAL.CUSTOMERS.

2. I then removed the first two rows of the dataset as they were unneccesary descriptions followed by then converting the `Variables` row into the official columns for my dataframe

3. Lastly I replaced all 0`s in the `OUTAGE.DURATION` columns with np.nan as a way to exclude the missing values from being included in my Visualizations and future calculations.

Here are the first few rows of the cleaned dataframe

|   YEAR |   MONTH |    POPULATION | CLIMATE.CATEGORY   | CLIMATE.REGION     |   CUSTOMERS.AFFECTED | TOTAL.SALES   |
|-------:|--------:|--------------:|:-------------------|:-------------------|---------------------:|:--------------|
|    nan |     nan | nan           | nan                | nan                |                  nan | Megawatt-hour |
|   2011 |       7 |   5.34812e+06 | normal             | East North Central |                70000 | 6562520       |
|   2014 |       5 |   5.45712e+06 | normal             | East North Central |                  nan | 5284231       |
|   2010 |      10 |   5.3109e+06  | cold               | East North Central |                70000 | 5222116       |
|   2012 |       6 |   5.38044e+06 | normal             | East North Central |                68200 | 5787064       |

# Data analysis

## Univariate Analysis

I first performed an univariate Analysis to explore the yearly trend of the number of outages occuring and what region has the most outages in total

This first graph depicts the positive then negative trend in the number of power outages happening each year from 2000-2016

<iframe
  src="assets/year_trend.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This graph shows the total number of power outages in the U.S seperated by `CLIMATE REGION`

<iframe
  src="assets/region_trend.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Bivariate Analysis

Following my univariate analysis, I also performed bivariate analysis in an attempt to find any relationships between variables that may be present in the data. 

I started this analysis by taking a look at the `TOTAL.SALES` and `MONTH` variables expecting to spike in the `TOTAL.SALES` values during the summer months as this is during summer break where people have much more free time to be using electricity for activities such as playing video games or just watching television. My expectations were correct with a spike in `TOTAL.SALSE` being present between the months July through September which is when school resumes.

<iframe
  src="assets/month.vs.sales.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I then did an analysis on the relationship between the `OUTAGE.DURATION` and `U.S._STATE` variables. I initially thought that states like California and New York would be the leading outliers due to their large populations. However after plotting the box plot it was shown that states, Michigan, Arizona, and Wisconsin were among the states containing some of the largest outliers. This told me that `OUTAGE.DURATION` won`t be the as strong of a predictor as I thought.

<iframe
  src="assets/states.vs.duration.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Aggregate analysis

For my aggregate analysis, I performed it by grouping the data on the `U.S._STATE` and `CAUSE.CATEGORY` columns in order to get a visualization of the number of outages that occur in each states broken down by what types of outages occured in each state.

|   YEAR |   MONTH |   POSTAL.CODE |   CLIMATE.REGION |   CLIMATE.CATEGORY |   OUTAGE.START.DATE |   OUTAGE.START.TIME |   OUTAGE.RESTORATION.DATE |   OUTAGE.RESTORATION.TIME |   OUTAGE.DURATION |   TOTAL.PRICE |   TOTAL.SALES |   TOTAL.CUSTOMERS |   POPULATION |   CUSTOMERS.AFFECTED |   PCT_LAND |
|-------:|--------:|--------------:|-----------------:|-------------------:|--------------------:|--------------------:|--------------------------:|--------------------------:|------------------:|--------------:|--------------:|------------------:|-------------:|---------------------:|-----------:|
|      1 |       1 |             1 |                1 |                  1 |                   1 |                   1 |                         1 |                         1 |                 1 |             1 |             1 |                 1 |            1 |                    0 |          1 |
|      5 |       4 |             5 |                5 |                  4 |                   4 |                   4 |                         4 |                         4 |                 4 |             4 |             4 |                 5 |            5 |                    5 |          5 |
|      1 |       0 |             1 |                0 |                  0 |                   0 |                   0 |                         0 |                         0 |                 0 |             0 |             0 |                 1 |            1 |                    1 |          1 |
|      4 |       4 |             4 |                4 |                  4 |                   4 |                   4 |                         4 |                         4 |                 4 |             4 |             4 |                 4 |            4 |                    3 |          4 |
|     18 |      18 |            18 |               18 |                 18 |                  18 |                  18 |                        15 |                        15 |                15 |            18 |            18 |                18 |           18 |                    2 |         18 |

<iframe
  src="assets/state_outages.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I also created a pivot table grouping the `POSTAL.CODE` and `OUTAGE.DURATION` columns in order to see the average outage duration by state. The first fews rows of that table are shown below

| POSTAL.CODE   |   OUTAGE.DURATION |
|:--------------|------------------:|
| AL            |          1152.8   |
| AR            |          1514.36  |
| AZ            |          4552.92  |
| CA            |          1674.8   |
| CO            |           901.071 |

# Assessment of Missingness

## NMAR Analysis

Of all the columns in the dataset, CUSTOMERS.AFFECTED has a marginally higher number of missing values compared to any other column in the dataset. Due to the datasets method of collecting the data from various companies, I believe this high number of missing values in this column is caused by some companies not providing the number of customers affected by their outages for whatever reason they saw fit.

This belief also causes me to think that the CUSTOMER.AFFECTED column is NMAR. I would check if this column is MAR by collecting the companies name for each of the outages and testing if missingness in the column is dependent on the company by performing a permutation test.

## Missingness Dependency

I will be testing missingness dependency on the `OUTAGE.DURATION` column as this is the column with the second most missing values in my cleaned dataset. I will test this against the `POSTCAL.CODE` and `CLIMATE.CATEGORY` columns

I start with the `POSTAL.CODE` column

**Null Hypothesis**: The distribution of the `POSTAL.CODE` column is the same when `OUTAGE.DURATION` is missing vs when it`s no missing

**Alternate Hypothesis**: The distribution of the `POSTAL.CODE` column is different when `OUTAGE.DURATION` is missing vs when it`s no missing

My observed test statistic was 0.39 and after performing a TVD permutation test I obtained a p-value of 0.0. These values are telling me that I can reject my null hypothesis as well as tell me that the distribution of the `POSTAL.CODE` column is significantly impacted by the missingness of values in `OUTAGE.DURATION`

<iframe
  src="assets/postal_test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I next test the `CLIMATE.CATEGORY` column

**Null Hypothesis**: The distribution of the `CLIMATE.CATEGORY` column is the same when `OUTAGE.DURATION` is missing vs when it`s no missing

**Alternate Hypothesis**: The distribution of the `CLIMATE.CATEGORY` column is different when `OUTAGE.DURATION` is missing vs when it`s no missing

The observed test statistic was 0.0941 with my p-value being 0.072 after performing another TVD permutation test. With a p-value of 0.072 I can accept my null hypothesis and state that there is not significant evidence that the `OUTAGE.DURATION` column`s missingness isn`t dependent `CLIMATE.CATEGORY`

<iframe
  src="assets/climate_test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Hypothesis Testing

I want to test if the northestern region of the United States, on average, has power outages that last longer than power outages in the southern region of the United States. I will be testing this using the `CLIMATE.REGION` and `OUTAGE.DURATION` columns

**Groups**: Northeast and South region

**Null**: On average, the northwest region has the same duration of power outages as the south region

**Alt**: On average, the northwest region has longer power outage durations than the south region

**Test statistic** = difference in means

**Significance Level** = 0.05

I chose to do a permutation test for this hypothesis because I have two distinct groups that I want to see how similar their distributions are. I performed 1000 permutation test simulations and plotted the distribution of the difference in the simulation means. I chose to use a difference in means test statistic because im comparing the average values of the duration of outages in both regions. I chose this statistic as opposed to using absolute difference in means because I'm testing if the northeastern region has longer outages than the southern region meaning I want to see negative and positive values for my test statistic to signify which region is larger per test.

After completing the permutation test I calculated a p-value of 0.154 which is larger than my propsed significance level of 0.05 meaning I can rejecy my null hypothesis. So in conclusion, there is not significane evidence to conclude that the northeastern region of the United States, on average, experiences similar durations of power outages compared the southern region. I think a reason for this is because of the northern regrion's overall larger population and urban enviornment causing more demand for electricity than the southern region which is more rural.

The plot below shows the results of my testing

<iframe
  src="assets/empirical.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Framing a Prediction Problem

My model will try to predict the region a power outage occured. This will be a classification model because we are only focusing on the location the power outage occured in.

The metric I am using the evaluate my model is the accuracy, because all that matters in the classification model is how accurate it's predictions are about the location of the outage.

At the time of prediction, we would know the  climate category, population, total price, total sales, and outage duration. These features will allow us to predict what the cause of a major power outage is.

# Baseline Model

My model is a RandomForest which I will be using for classification with the features climate category, population, total price, total sales, and outage duration to predict where a major power outage occured. These features will allow comapanies to better understand, given these features where an outage is likely to occur to better prepare for it.

These features will be; `CLIMATE.CATEGORY` (nominal), `POPULATION` (quantitative), `TOTAL.PRICE` (quanititative), `TOTAL.SALES` (quantitative), and OUTAGE.DURATION (quantitative). My reasoning behind choosing these features is that `CLIMATE.CATEGORY` helps in narrowing down where in the U.S the outage can be, `POPULATION` helps narrow down regions due to some having a higher population than others, `TOTAL.PRICE` because some areas are more expensive than others, `TOTAL.SALES` same reasoning as `TOTAL.PRICE` and `CLIMATE.CATEGORY` since all regions of the U.S have varying climates compared to one another.

The only encoding I performed was onehot encoding on the `CLIMATE.CATEGORY`.

The baseline models performance was poor with having an accuracy of only %46.

# Final Model

My final model uses the same features as my baseline model however I engineered two new features from my orignally selected. I'm still using a RandomForest Classifier.

I binarized the `TOTAL.PRICE` feature in order to categorizes locations as high or low priced inorder to add further classification to each observation. I also applied a standard scaler to `TOTAL.SALES` and `OUTAGE.DURATION` in order to have a normal distribution on these features and better identify outliers. Finally, I kept my original onehot encoding of the `CLIMATE.CATEGORY` column.

I then used GridSearchCV (crossvalidation) to find the most optimal hyperparameters for my RandomForest. My hyperperameters were:

criterion: ‘entropy’
max_depth: None
min_samples_split: 2

After engineering new features and using the hyperperameters given from grid search cross validation my final model was able to acheive an accuracy of %89.


# Fairness Analysis

In order to test the models fairness I decided to see if my model can accurately and equally predict the climate region for both small and large populations.

My reasoning behind choosing these groups was because climate regions all have varying populations within themselves so I want to test if my model can accurately predict the climate region no matter the population size so companies can get accurate insights for any region.

My evaluation metric will still be accuracy for my groups, large vs small population. I only care about accuracy in this case since this is a classification model and it being wrong isn't as impactful as it being right. Also the groups are fairly balanced. I will use permutation tests to calculate the accuracy for larger and smaller populations and then compare there difference to the observed difference.

Null Hypothesis: The model is fair. Its accuracy for larger and smaller populations are roughly the same, and any differences are due to random chance.

Alternative Hypothesis: The model is not fair and its accuracy for larger populations is significantly different from the accuracy for smaller populations.

I calculated the mean population size and used this as my cutoff for large or small populations. I then performed a permutation test. My significance level will be 0.05, and my p_value was 0.0. Because this is below my significance level, I can reject the null hypothesis meaning my model'saccuracy is significantly different for larger populations compared to smaller populations.

The figure below shows the distribution of the statistic.

<iframe
  src="assets/fairness.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
