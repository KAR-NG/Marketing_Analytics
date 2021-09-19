Marketing Analytics
================
Kar Ng
2021

-   [1 SUMMARY](#1-summary)
-   [2 R PACKAGES](#2-r-packages)
-   [3 INTRODUCTION](#3-introduction)
-   [4 DATA PREPARATION](#4-data-preparation)
    -   [4.1 Data import](#41-data-import)
    -   [4.2 Data description](#42-data-description)
    -   [4.3 Data exploration](#43-data-exploration)
-   [5 DATA CLEANING AND
    MANIPULATION](#5-data-cleaning-and-manipulation)
    -   [5.1 Data type conversion](#51-data-type-conversion)
    -   [5.2 Examing tricky missing
        value](#52-examing-tricky-missing-value)
    -   [5.3 Fill up the blank salary
        cells](#53-fill-up-the-blank-salary-cells)
    -   [5.4 Create Age Column](#54-create-age-column)
    -   [5.5 Data processing summary](#55-data-processing-summary)
-   [6 EXPLORATORY DATA ANALYSIS
    (EDA)](#6-exploratory-data-analysis-eda)
    -   [6.1 What does the average customer look like for this
        company?](#61-what-does-the-average-customer-look-like-for-this-company)
        -   [6.1.1 Age](#611-age)
        -   [6.1.2 Country](#612-country)
        -   [6.1.3 Education](#613-education)
        -   [6.1.4 Marital Status](#614-marital-status)
        -   [6.1.5 Customer’s Family size](#615-customers-family-size)
        -   [6.1.6 Income](#616-income)
    -   [6.2 Which products are performing the
        best?](#62-which-products-are-performing-the-best)
    -   [6.3 Which marketing campaign is most
        successful?](#63-which-marketing-campaign-is-most-successful)
    -   [6.4 Which channels are
        underperforming?](#64-which-channels-are-underperforming)
-   [7 STATISTICAL ANALYSIS](#7-statistical-analysis)
    -   [7.1 Testing for
        multicollinearity](#71-testing-for-multicollinearity)
        -   [7.1.1 Correlation assessment](#711-correlation-assessment)
        -   [7.1.2 Variance Inflation factor (VIF)
            assessment](#712-variance-inflation-factor-vif-assessment)
    -   [7.2 Factors that significantly related to in-store
        purchases](#72-factors-that-significantly-related-to-in-store-purchases)
        -   [7.2.1 Data Partitioning](#721-data-partitioning)
        -   [7.2.2 Building the model and model
            performance](#722-building-the-model-and-model-performance)
        -   [7.2.3 Summarise the model](#723-summarise-the-model)
    -   [Lasso](#lasso)
    -   [7.3 Does US’s purchasing power significantly better than the
        rest of the world in terms of total purchases
        ?](#73-does-uss-purchasing-power-significantly-better-than-the-rest-of-the-world-in-terms-of-total-purchases-)
        -   [7.3.1 Comparing total purchases PER CUSTOMER in different
            country\*\*](#731-comparing-total-purchases-per-customer-in-different-country)
        -   [7.3.2 Assumption tests](#732-assumption-tests)
        -   [7.3.4 Kruskal Wallis statistical
            test](#734-kruskal-wallis-statistical-test)
        -   [7.3.5 Visualisation](#735-visualisation)
    -   [7.4 Are gold lovers prefer to shop in
        store?](#74-are-gold-lovers-prefer-to-shop-in-store)
        -   [7.4.1 Visualisation](#741-visualisation)
        -   [7.4.2 Building a model](#742-building-a-model)
        -   [7.4.3 Assumption tests](#743-assumption-tests)
        -   [7.4.4 Mann-Whitney test](#744-mann-whitney-test)
    -   [7.5 Consumption of married PhD candidates on
        Fish](#75-consumption-of-married-phd-candidates-on-fish)
        -   [7.5.1 Married PhD candidates vs others in amount spent on
            fish](#751-married-phd-candidates-vs-others-in-amount-spent-on-fish)
        -   [7.5.2 What other factors are significantly related to
            amount spent on
            fish?](#752-what-other-factors-are-significantly-related-to-amount-spent-on-fish)
    -   [7.6 Is there a significant relationship between geographical
        regional and success of a
        campaign?](#76-is-there-a-significant-relationship-between-geographical-regional-and-success-of-a-campaign)
-   [8 CONCLUSION](#8-conclusion)
-   [9 LEGALITY](#9-legality)
-   [10 REFERENCE](#10-reference)
-   [11 ACKNOWLEDGEMENT](#11-acknowledgement)

------------------------------------------------------------------------

![](https://raw.githubusercontent.com/KAR-NG/marketing/main/pic2_thumbnail.JPG.png)

------------------------------------------------------------------------

Reading time: 35 minutes

## 1 SUMMARY

This is a personal project uses a public dataset from *Kaggle* that
designed for students in MSc. in Business Analytics as their final
project. The dataset comprised of customer information, sales channels,
products sold by the company, and the acceptance data of marketing
campaigns. There are 4 tasks for visual exploration and 5 tasks for
statistical analysis.

All 9 business tasks have been solved by 18 graphs and 10 statistical
methods. Statistical methods used in this project include:

-   Exploratory data analysis (EDA)  
-   Multicollinearity test using correlation & VIF  
-   Data partitioning to create train & test for RMSE & R2  
-   Stepwise model selection  
-   Multiple linear regression (MLR)  
-   Generalised Linear Models (GLM)’s binomial for logistic regression  
-   Normality test using Q-Q plot and Shapiro-Wilk test  
-   Variance test with Levene’s test  
-   Omnibus test with Kruskal-Wallis Test  
-   Two-sample non-parametric test with Mann-Whitney test

Results from EDA reveal that most customer are in mature age between 30
to 55, 51% of customers are from Spain, half of the customers have
education level of “graduate” level, 71.5% of customers have a least 1
children home, half of the customers have income between $35k to $70k
and wine is the best selling product that contributing 50.15% to the
total revenue. All marketing campaigns weren’t doing very well with
acceptance rates of lower than 15%. In store sales is the most
performing channels.

Results from statistical analysis reveal in-store purchases is
significantly affected by products, deals, purchases made through web,
income, number of kids at home, sales through catalog and customer’s
visit frequency to company’s website. Purchasing power of customers from
the US do not significantly different from other countries (P-value
0.4004). Gold buyers have more store purchases (P-value &lt; 0.05).
Married PhD candidates spent significantly less than other customer
groups on fish, with a p-value of less than 0.05. Statistical analysis
also concluded that there is no significant relationship between
geographical regions and success of a campaign.

<br/>

*Highlights*

<br/>

![](https://raw.githubusercontent.com/KAR-NG/marketing/main/pic1_highlight.png)

<br/>

## 2 R PACKAGES

R packages loaded in this project include tidyverse packages (ggplot2,
dplyr, tidyr, readr, purrr, tibble, stringr, and forcats), skimr,
kableExtra, DT, lubridate, zoo, gridExtra, ggplotr, ggrepel, car, caret,
DescTools, multcomp, and olsrr.

``` r
library(tidyverse)
library(skimr)
library(kableExtra)
library(lubridate)
library(zoo) 
library(gridExtra)
library(qqplotr)
library(ggrepel)
library(car)     # For VIF
library(caret)
library(DescTools)
library(multcomp)
library(olsrr)
```

## 3 INTRODUCTION

The purpose of this project is to answer a series of general business
questions using R programming language. This project has a dataset that
provides many marketing data include general customer information,
products sold by the company, the company’s sale channels, and the
performance of a series of marketing campaigns that the company has
launched.

The business questions that I am tasked to answer are separated into 2
main bodies, one is for data exploration analysis, and the other one is
for statistical analysis.

Business questions for data exploration analysis (EDA) are:

-   What does the average customer look like for this company?  
-   Which products are performing best?  
-   Which marketing campaign is most successful?  
-   Which channels are underperforming?

Business questions for statistical analysis are:

-   What are the factors that significantly related to in-store
    purchases?  
-   Does US’s purchasing power significantly better than the rest of hte
    world in terms of total purchase?  
-   Are gold lovers prefer to shop in store?  
-   Do “Married PhD candidates” have a significant relation with amount
    spent on fish? What other factors are significantly related to
    amount spent on fish?  
-   Is there a significant relationship between geographical regional
    and success of a campaign?

This project uses a public dataset from *Kaggle*. *Kaggle* is a
professional website for data science community. The dataset was
supplied by Dr. Omar Romero-Hernandez for his students for their final
project in order to test their statistical analysis skills as part of a
MSc. in Business Analytics. Please click this
[Link](https://www.kaggle.com/jackdaoud/marketing-data) to the website.
All of the above business questions are actually questions for the
marketing students to answer, visit this
[Link](https://www.kaggle.com/jackdaoud/marketing-data/tasks?taskId=2986)
to the relevant website.

## 4 DATA PREPARATION

### 4.1 Data import

Following codes import the dataset. Table below is an indication of
successful data import.

------------------------------------------------------------------------

``` r
marketing_data <- read_csv("marketing_data.csv")
head(marketing_data)
```

    ## # A tibble: 6 x 28
    ##      ID Year_Birth Education  Marital_Status Income     Kidhome Teenhome Dt_Customer
    ##   <dbl>      <dbl> <chr>      <chr>          <chr>        <dbl>    <dbl> <chr>      
    ## 1  1826       1970 Graduation Divorced       $84,835.00       0        0 6/16/14    
    ## 2     1       1961 Graduation Single         $57,091.00       0        0 6/15/14    
    ## 3 10476       1958 Graduation Married        $67,267.00       0        1 5/13/14    
    ## 4  1386       1967 Graduation Together       $32,474.00       1        1 5/11/14    
    ## 5  5371       1989 Graduation Single         $21,474.00       1        0 4/8/14     
    ## 6  7348       1958 PhD        Single         $71,691.00       0        0 3/17/14    
    ## # ... with 20 more variables: Recency <dbl>, MntWines <dbl>, MntFruits <dbl>,
    ## #   MntMeatProducts <dbl>, MntFishProducts <dbl>, MntSweetProducts <dbl>,
    ## #   MntGoldProds <dbl>, NumDealsPurchases <dbl>, NumWebPurchases <dbl>,
    ## #   NumCatalogPurchases <dbl>, NumStorePurchases <dbl>,
    ## #   NumWebVisitsMonth <dbl>, AcceptedCmp3 <dbl>, AcceptedCmp4 <dbl>,
    ## #   AcceptedCmp5 <dbl>, AcceptedCmp1 <dbl>, AcceptedCmp2 <dbl>, Response <dbl>,
    ## #   Complain <dbl>, Country <chr>

------------------------------------------------------------------------

### 4.2 Data description

Following table describes all variables in the dataset, extracted from
the [Kaggle website](https://www.kaggle.com/jackdaoud/marketing-data).

``` r
Variable <- c("ID", 
              "Year_Birth", 
              "Education",
              "Marital_Status",
              "Income",
              "Kidhome",
              "Teenhome",
              "Dt_Customer",  
              "Recency",
              "MntWines",
              "MntFruits",
              "MntMeatProducts",
              "MntFishProducts",
              "MntSweetProducts",
              "MntGoldProds",
              "NumDealsPurchases",
              "NumWebPurchases",
              "NumCatalogPurchases",
              "NumStorePurchases",
              "NumWebVisitsMonth",
              "AcceptedCmp3",
              "AcceptedCmp4",
              "AcceptedCmp5",
              "AcceptedCmp1",
              "AcceptedCmp2",
              "Response",
              "Complain",
              "Country")

Description <- c("Customer's unique identifier",
                 "Customer's birth year",
                 "Customer's education level",
                 "Customer's marital status",
                 "Customer's yearly household income",
                 "Number of children in customer's household",
                 "Number of teenagers in customer's household",
                 "Date of customer's enrollment with the company",
                 "Number of days since customer's last purchase",
                 "Amount spent on wine in the last 2 years",
                 "Amount spent on fruits in the last 2 years",
                 "Amount spent on meat in the last 2 years",
                 "Amount spent on fish in the last 2 years",
                 "Amount spent on sweets in the last 2 years",
                 "Amount spent on gold in the last 2 years",
                 "Number of purchases made with a discount",
                 "Number of purchases made through the company's web site",
                 "Number of purchases made using a catalogue",
                 "Number of purchases made directly in stores",
                 "Number of visits to company's web site in the last month",
                 "1 if customer accepted the offer in the 3rd campaign, 0 otherwise",
                 "1 if customer accepted the offer in the 4th campaign, 0 otherwise",
                 "1 if customer accepted the offer in the 5th campaign, 0 otherwise",
                 "1 if customer accepted the offer in the 1st campaign, 0 otherwise",
                 "1 if customer accepted the offer in the 2nd campaign, 0 otherwise",
                 "1 if customer accepted the offer in the last campaign, 0 otherwise",
                 "1 if customer complained in the last 2 years, 0 otherwise",
                 "Customer's location")

data.frame(No = c(1:28), Variable, Description) %>% 
  kbl() %>% 
  kable_styling(bootstrap_options = c("bordered", "striped", "hover"))
```

<table class="table table-bordered table-striped table-hover" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:right;">
No
</th>
<th style="text-align:left;">
Variable
</th>
<th style="text-align:left;">
Description
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
1
</td>
<td style="text-align:left;">
ID
</td>
<td style="text-align:left;">
Customer’s unique identifier
</td>
</tr>
<tr>
<td style="text-align:right;">
2
</td>
<td style="text-align:left;">
Year\_Birth
</td>
<td style="text-align:left;">
Customer’s birth year
</td>
</tr>
<tr>
<td style="text-align:right;">
3
</td>
<td style="text-align:left;">
Education
</td>
<td style="text-align:left;">
Customer’s education level
</td>
</tr>
<tr>
<td style="text-align:right;">
4
</td>
<td style="text-align:left;">
Marital\_Status
</td>
<td style="text-align:left;">
Customer’s marital status
</td>
</tr>
<tr>
<td style="text-align:right;">
5
</td>
<td style="text-align:left;">
Income
</td>
<td style="text-align:left;">
Customer’s yearly household income
</td>
</tr>
<tr>
<td style="text-align:right;">
6
</td>
<td style="text-align:left;">
Kidhome
</td>
<td style="text-align:left;">
Number of children in customer’s household
</td>
</tr>
<tr>
<td style="text-align:right;">
7
</td>
<td style="text-align:left;">
Teenhome
</td>
<td style="text-align:left;">
Number of teenagers in customer’s household
</td>
</tr>
<tr>
<td style="text-align:right;">
8
</td>
<td style="text-align:left;">
Dt\_Customer
</td>
<td style="text-align:left;">
Date of customer’s enrollment with the company
</td>
</tr>
<tr>
<td style="text-align:right;">
9
</td>
<td style="text-align:left;">
Recency
</td>
<td style="text-align:left;">
Number of days since customer’s last purchase
</td>
</tr>
<tr>
<td style="text-align:right;">
10
</td>
<td style="text-align:left;">
MntWines
</td>
<td style="text-align:left;">
Amount spent on wine in the last 2 years
</td>
</tr>
<tr>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;">
MntFruits
</td>
<td style="text-align:left;">
Amount spent on fruits in the last 2 years
</td>
</tr>
<tr>
<td style="text-align:right;">
12
</td>
<td style="text-align:left;">
MntMeatProducts
</td>
<td style="text-align:left;">
Amount spent on meat in the last 2 years
</td>
</tr>
<tr>
<td style="text-align:right;">
13
</td>
<td style="text-align:left;">
MntFishProducts
</td>
<td style="text-align:left;">
Amount spent on fish in the last 2 years
</td>
</tr>
<tr>
<td style="text-align:right;">
14
</td>
<td style="text-align:left;">
MntSweetProducts
</td>
<td style="text-align:left;">
Amount spent on sweets in the last 2 years
</td>
</tr>
<tr>
<td style="text-align:right;">
15
</td>
<td style="text-align:left;">
MntGoldProds
</td>
<td style="text-align:left;">
Amount spent on gold in the last 2 years
</td>
</tr>
<tr>
<td style="text-align:right;">
16
</td>
<td style="text-align:left;">
NumDealsPurchases
</td>
<td style="text-align:left;">
Number of purchases made with a discount
</td>
</tr>
<tr>
<td style="text-align:right;">
17
</td>
<td style="text-align:left;">
NumWebPurchases
</td>
<td style="text-align:left;">
Number of purchases made through the company’s web site
</td>
</tr>
<tr>
<td style="text-align:right;">
18
</td>
<td style="text-align:left;">
NumCatalogPurchases
</td>
<td style="text-align:left;">
Number of purchases made using a catalogue
</td>
</tr>
<tr>
<td style="text-align:right;">
19
</td>
<td style="text-align:left;">
NumStorePurchases
</td>
<td style="text-align:left;">
Number of purchases made directly in stores
</td>
</tr>
<tr>
<td style="text-align:right;">
20
</td>
<td style="text-align:left;">
NumWebVisitsMonth
</td>
<td style="text-align:left;">
Number of visits to company’s web site in the last month
</td>
</tr>
<tr>
<td style="text-align:right;">
21
</td>
<td style="text-align:left;">
AcceptedCmp3
</td>
<td style="text-align:left;">
1 if customer accepted the offer in the 3rd campaign, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
22
</td>
<td style="text-align:left;">
AcceptedCmp4
</td>
<td style="text-align:left;">
1 if customer accepted the offer in the 4th campaign, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
23
</td>
<td style="text-align:left;">
AcceptedCmp5
</td>
<td style="text-align:left;">
1 if customer accepted the offer in the 5th campaign, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
24
</td>
<td style="text-align:left;">
AcceptedCmp1
</td>
<td style="text-align:left;">
1 if customer accepted the offer in the 1st campaign, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
25
</td>
<td style="text-align:left;">
AcceptedCmp2
</td>
<td style="text-align:left;">
1 if customer accepted the offer in the 2nd campaign, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
26
</td>
<td style="text-align:left;">
Response
</td>
<td style="text-align:left;">
1 if customer accepted the offer in the last campaign, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
27
</td>
<td style="text-align:left;">
Complain
</td>
<td style="text-align:left;">
1 if customer complained in the last 2 years, 0 otherwise
</td>
</tr>
<tr>
<td style="text-align:right;">
28
</td>
<td style="text-align:left;">
Country
</td>
<td style="text-align:left;">
Customer’s location
</td>
</tr>
</tbody>
</table>

It is a comprehensive dataset and it contains classifiable information.

-   1.  **Customer information**: ID, age, education, marital status,
        income, number of kids and teens at home, date of customer’s
        enrollment with the company, recency, complain(s) made in the
        last 2 years, country of the customer currently at (I assume),
        the number of purchases made during a discount, and customers’
        frequency of visiting company’s website.

-   2.  **Products of the company**: Wines, fruits, meat, fish, sweet,
        and gold.

-   3.  **Sale Channels**: Number of purchases made via company website,
        catalog, and in the store.

-   4.  Customers responses on **company’s marketing campaigns**. There
        are a total of 6 campaigns launched.

### 4.3 Data exploration

This dataset has 2,240 rows of observations and 28 columns of variables.
Among the variables, there are 5 character variables and 23 numerical
variables.

------------------------------------------------------------------------

``` r
skim_without_charts(marketing_data)
```

<table style="width: auto;" class="table table-condensed">
<caption>
Data summary
</caption>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Name
</td>
<td style="text-align:left;">
marketing\_data
</td>
</tr>
<tr>
<td style="text-align:left;">
Number of rows
</td>
<td style="text-align:left;">
2240
</td>
</tr>
<tr>
<td style="text-align:left;">
Number of columns
</td>
<td style="text-align:left;">
28
</td>
</tr>
<tr>
<td style="text-align:left;">
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Column type frequency:
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
character
</td>
<td style="text-align:left;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
numeric
</td>
<td style="text-align:left;">
23
</td>
</tr>
<tr>
<td style="text-align:left;">
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Group variables
</td>
<td style="text-align:left;">
None
</td>
</tr>
</tbody>
</table>

**Variable type: character**

<table>
<thead>
<tr>
<th style="text-align:left;">
skim\_variable
</th>
<th style="text-align:right;">
n\_missing
</th>
<th style="text-align:right;">
complete\_rate
</th>
<th style="text-align:right;">
min
</th>
<th style="text-align:right;">
max
</th>
<th style="text-align:right;">
empty
</th>
<th style="text-align:right;">
n\_unique
</th>
<th style="text-align:right;">
whitespace
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Education
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
10
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Marital\_Status
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Income
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:right;">
0.99
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1974
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Dt\_Customer
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
6
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
663
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Country
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
8
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>

**Variable type: numeric**

<table>
<thead>
<tr>
<th style="text-align:left;">
skim\_variable
</th>
<th style="text-align:right;">
n\_missing
</th>
<th style="text-align:right;">
complete\_rate
</th>
<th style="text-align:right;">
mean
</th>
<th style="text-align:right;">
sd
</th>
<th style="text-align:right;">
p0
</th>
<th style="text-align:right;">
p25
</th>
<th style="text-align:right;">
p50
</th>
<th style="text-align:right;">
p75
</th>
<th style="text-align:right;">
p100
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
ID
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
5592.16
</td>
<td style="text-align:right;">
3246.66
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
2828.25
</td>
<td style="text-align:right;">
5458.5
</td>
<td style="text-align:right;">
8427.75
</td>
<td style="text-align:right;">
11191
</td>
</tr>
<tr>
<td style="text-align:left;">
Year\_Birth
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
1968.81
</td>
<td style="text-align:right;">
11.98
</td>
<td style="text-align:right;">
1893
</td>
<td style="text-align:right;">
1959.00
</td>
<td style="text-align:right;">
1970.0
</td>
<td style="text-align:right;">
1977.00
</td>
<td style="text-align:right;">
1996
</td>
</tr>
<tr>
<td style="text-align:left;">
Kidhome
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.44
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Teenhome
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.51
</td>
<td style="text-align:right;">
0.54
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
Recency
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
49.11
</td>
<td style="text-align:right;">
28.96
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
24.00
</td>
<td style="text-align:right;">
49.0
</td>
<td style="text-align:right;">
74.00
</td>
<td style="text-align:right;">
99
</td>
</tr>
<tr>
<td style="text-align:left;">
MntWines
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
303.94
</td>
<td style="text-align:right;">
336.60
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
23.75
</td>
<td style="text-align:right;">
173.5
</td>
<td style="text-align:right;">
504.25
</td>
<td style="text-align:right;">
1493
</td>
</tr>
<tr>
<td style="text-align:left;">
MntFruits
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
26.30
</td>
<td style="text-align:right;">
39.77
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
8.0
</td>
<td style="text-align:right;">
33.00
</td>
<td style="text-align:right;">
199
</td>
</tr>
<tr>
<td style="text-align:left;">
MntMeatProducts
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
166.95
</td>
<td style="text-align:right;">
225.72
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
16.00
</td>
<td style="text-align:right;">
67.0
</td>
<td style="text-align:right;">
232.00
</td>
<td style="text-align:right;">
1725
</td>
</tr>
<tr>
<td style="text-align:left;">
MntFishProducts
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
37.53
</td>
<td style="text-align:right;">
54.63
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
3.00
</td>
<td style="text-align:right;">
12.0
</td>
<td style="text-align:right;">
50.00
</td>
<td style="text-align:right;">
259
</td>
</tr>
<tr>
<td style="text-align:left;">
MntSweetProducts
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
27.06
</td>
<td style="text-align:right;">
41.28
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
8.0
</td>
<td style="text-align:right;">
33.00
</td>
<td style="text-align:right;">
263
</td>
</tr>
<tr>
<td style="text-align:left;">
MntGoldProds
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
44.02
</td>
<td style="text-align:right;">
52.17
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
9.00
</td>
<td style="text-align:right;">
24.0
</td>
<td style="text-align:right;">
56.00
</td>
<td style="text-align:right;">
362
</td>
</tr>
<tr>
<td style="text-align:left;">
NumDealsPurchases
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
2.33
</td>
<td style="text-align:right;">
1.93
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1.00
</td>
<td style="text-align:right;">
2.0
</td>
<td style="text-align:right;">
3.00
</td>
<td style="text-align:right;">
15
</td>
</tr>
<tr>
<td style="text-align:left;">
NumWebPurchases
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
4.08
</td>
<td style="text-align:right;">
2.78
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
2.00
</td>
<td style="text-align:right;">
4.0
</td>
<td style="text-align:right;">
6.00
</td>
<td style="text-align:right;">
27
</td>
</tr>
<tr>
<td style="text-align:left;">
NumCatalogPurchases
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
2.66
</td>
<td style="text-align:right;">
2.92
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
2.0
</td>
<td style="text-align:right;">
4.00
</td>
<td style="text-align:right;">
28
</td>
</tr>
<tr>
<td style="text-align:left;">
NumStorePurchases
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
5.79
</td>
<td style="text-align:right;">
3.25
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
3.00
</td>
<td style="text-align:right;">
5.0
</td>
<td style="text-align:right;">
8.00
</td>
<td style="text-align:right;">
13
</td>
</tr>
<tr>
<td style="text-align:left;">
NumWebVisitsMonth
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
5.32
</td>
<td style="text-align:right;">
2.43
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
3.00
</td>
<td style="text-align:right;">
6.0
</td>
<td style="text-align:right;">
7.00
</td>
<td style="text-align:right;">
20
</td>
</tr>
<tr>
<td style="text-align:left;">
AcceptedCmp3
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.07
</td>
<td style="text-align:right;">
0.26
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
AcceptedCmp4
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.07
</td>
<td style="text-align:right;">
0.26
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
AcceptedCmp5
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.07
</td>
<td style="text-align:right;">
0.26
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
AcceptedCmp1
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.06
</td>
<td style="text-align:right;">
0.25
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
AcceptedCmp2
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.01
</td>
<td style="text-align:right;">
0.11
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Response
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.15
</td>
<td style="text-align:right;">
0.36
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
Complain
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.01
</td>
<td style="text-align:right;">
0.10
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
0.0
</td>
<td style="text-align:right;">
0.00
</td>
<td style="text-align:right;">
1
</td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

Insights:

-   This dataset is very complete. All variables have a
    **complete\_rate** of 1, which stands for 100%, indicating there is
    no any missing value their columns. It associated with the adjacent
    column **n\_missing**, which is almost 0 for all variables.

-   Except for the variable “Income”, it has a **complete\_rate** of
    0.989 (98.9%). Generally, an analyst will remove these NA rows
    because 98.9% is a level that is already high enough to accept.
    However, I will fill up these blank cells by looking for mean (if
    normality is observed) or median (if outlier is observed) from
    relevant information. This will be carried out in data manipulation
    section.

-   There are no white spaces among the 5 character variables that
    needed to clean as well, by examining the column **whitespace**.

Following summary provides a quick way to examine are the data types
assigned to each column rightfully.

``` r
glimpse(marketing_data)
```

    ## Rows: 2,240
    ## Columns: 28
    ## $ ID                  <dbl> 1826, 1, 10476, 1386, 5371, 7348, 4073, 1991, 4047~
    ## $ Year_Birth          <dbl> 1970, 1961, 1958, 1967, 1989, 1958, 1954, 1967, 19~
    ## $ Education           <chr> "Graduation", "Graduation", "Graduation", "Graduat~
    ## $ Marital_Status      <chr> "Divorced", "Single", "Married", "Together", "Sing~
    ## $ Income              <chr> "$84,835.00", "$57,091.00", "$67,267.00", "$32,474~
    ## $ Kidhome             <dbl> 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1,~
    ## $ Teenhome            <dbl> 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 1,~
    ## $ Dt_Customer         <chr> "6/16/14", "6/15/14", "5/13/14", "5/11/14", "4/8/1~
    ## $ Recency             <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ MntWines            <dbl> 189, 464, 134, 10, 6, 336, 769, 78, 384, 384, 450,~
    ## $ MntFruits           <dbl> 104, 5, 11, 0, 16, 130, 80, 0, 0, 0, 26, 4, 82, 10~
    ## $ MntMeatProducts     <dbl> 379, 64, 59, 1, 24, 411, 252, 11, 102, 102, 535, 6~
    ## $ MntFishProducts     <dbl> 111, 7, 15, 0, 11, 240, 15, 0, 21, 21, 73, 0, 80, ~
    ## $ MntSweetProducts    <dbl> 189, 0, 2, 0, 0, 32, 34, 0, 32, 32, 98, 13, 20, 16~
    ## $ MntGoldProds        <dbl> 218, 37, 30, 0, 34, 43, 65, 7, 5, 5, 26, 4, 102, 3~
    ## $ NumDealsPurchases   <dbl> 1, 1, 1, 1, 2, 1, 1, 1, 3, 3, 1, 2, 1, 1, 0, 4, 4,~
    ## $ NumWebPurchases     <dbl> 4, 7, 3, 1, 3, 4, 10, 2, 6, 6, 5, 3, 3, 1, 25, 2, ~
    ## $ NumCatalogPurchases <dbl> 4, 3, 2, 0, 1, 7, 10, 1, 2, 2, 6, 1, 6, 1, 0, 1, 1~
    ## $ NumStorePurchases   <dbl> 6, 7, 5, 2, 2, 5, 7, 3, 9, 9, 10, 6, 6, 2, 0, 5, 5~
    ## $ NumWebVisitsMonth   <dbl> 1, 5, 2, 7, 7, 2, 6, 5, 4, 4, 1, 4, 1, 6, 1, 4, 4,~
    ## $ AcceptedCmp3        <dbl> 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ AcceptedCmp4        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ AcceptedCmp5        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ AcceptedCmp1        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ AcceptedCmp2        <dbl> 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ Response            <dbl> 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1,~
    ## $ Complain            <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,~
    ## $ Country             <chr> "SP", "CA", "US", "AUS", "SP", "SP", "GER", "SP", ~

I will convert some of the variables into factor type. “Factor” is a
variable type that can be assigned to either character or numerical
variable when these variables are found useful for grouping the data.
For example, variables “Country”, “Marital\_Status”, and “Year\_Birth”
can be useful to group data. This feature is important during data
analysis processing for cleaning, computational and machine learning
techniques.

Following are a few conversions that I will perform in the next data
cleaning and manipulation section.

Variables that need to be converted into factor type (fct) are

-   Education  
-   Marital\_Status  
-   Country

Variables that need to be converted into numerical (dbl) type:

-   Income

Variable that need to be in date (date) data type:

-   Dt\_Customer

## 5 DATA CLEANING AND MANIPULATION

### 5.1 Data type conversion

This section continues with the work mentioned in the last section to
convert some variables into their rightfully type so that the data
analysis can be more efficient and accurate. Following codes complete
the task.

``` r
# I will retain the original dataset as marketing_data and give a new object named "md".

md <- marketing_data

# Start mutating the dataset to obtain the correct data type.

md <- md %>% 
  mutate(Education = as.factor(Education),
         Marital_Status = as.factor(Marital_Status),
         Country = as.factor(Country),
         Dt_Customer = mdy(Dt_Customer))

md <- md %>% 
  mutate(Income = gsub(",", "", Income),
         Income = gsub("\\$", "", Income),
         Income = str_sub(Income, end = -4),
         Income = as.numeric(Income))
```

Checking the type of these variables using following code. Following
results show that the conversions have been successful

``` r
check <- md %>% dplyr::select(Education, Marital_Status, Country, Dt_Customer, Income)
glimpse(check)
```

    ## Rows: 2,240
    ## Columns: 5
    ## $ Education      <fct> Graduation, Graduation, Graduation, Graduation, Graduat~
    ## $ Marital_Status <fct> Divorced, Single, Married, Together, Single, Single, Ma~
    ## $ Country        <fct> SP, CA, US, AUS, SP, SP, GER, SP, US, IND, US, SP, IND,~
    ## $ Dt_Customer    <date> 2014-06-16, 2014-06-15, 2014-05-13, 2014-05-11, 2014-0~
    ## $ Income         <dbl> 84835, 57091, 67267, 32474, 21474, 71691, 63564, 44931,~

### 5.2 Examing tricky missing value

Though the dataset was found very complete without any missing value,
however, if a missing value is filled up manually with character string
data such as “null”, or “missing value” into the cells by the dataset
provider, then it will not be detected by the exploration method I used
because R will recognise them as a part of the data in character type.

This section will examine the presence of these words (or relevant) in
the character and factor variables of the dataset.

``` r
check2 <- md %>% 
  dplyr::select(is.factor, -ID)

sapply(check2, levels)
```

    ## $Education
    ## [1] "2n Cycle"   "Basic"      "Graduation" "Master"     "PhD"       
    ## 
    ## $Marital_Status
    ## [1] "Absurd"   "Alone"    "Divorced" "Married"  "Single"   "Together" "Widow"   
    ## [8] "YOLO"    
    ## 
    ## $Country
    ## [1] "AUS" "CA"  "GER" "IND" "ME"  "SA"  "SP"  "US"

There are no any written form of missing value in all variables (such as
“Null”, “Missing\_value”, “Blank”, or whatever relevant). The column
“ID” has its original data type as numeric at the absence of any
alphabetical string data, hence it does not contain any written form of
missing value.

Still, I am able to check is there any character data (such as “Null”,
“Missing\_value”, “Blank”, or whatever relevant) falling into the **ID**
column as well, by running following code. The result is 0, which
indicates that there is no character data in the column of **ID**.

``` r
which(str_detect(md$ID, "[[:alpha:]]"))
```

    ## integer(0)

### 5.3 Fill up the blank salary cells

In the section of data preparation, I found that the column **income**
has 24 missing value.

------------------------------------------------------------------------

``` r
skim_without_charts(md$Income)
```

<table style="width: auto;" class="table table-condensed">
<caption>
Data summary
</caption>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Name
</td>
<td style="text-align:left;">
md$Income
</td>
</tr>
<tr>
<td style="text-align:left;">
Number of rows
</td>
<td style="text-align:left;">
2240
</td>
</tr>
<tr>
<td style="text-align:left;">
Number of columns
</td>
<td style="text-align:left;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Column type frequency:
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
numeric
</td>
<td style="text-align:left;">
1
</td>
</tr>
<tr>
<td style="text-align:left;">
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
</td>
<td style="text-align:left;">
</td>
</tr>
<tr>
<td style="text-align:left;">
Group variables
</td>
<td style="text-align:left;">
None
</td>
</tr>
</tbody>
</table>

**Variable type: numeric**

<table>
<thead>
<tr>
<th style="text-align:left;">
skim\_variable
</th>
<th style="text-align:right;">
n\_missing
</th>
<th style="text-align:right;">
complete\_rate
</th>
<th style="text-align:right;">
mean
</th>
<th style="text-align:right;">
sd
</th>
<th style="text-align:right;">
p0
</th>
<th style="text-align:right;">
p25
</th>
<th style="text-align:right;">
p50
</th>
<th style="text-align:right;">
p75
</th>
<th style="text-align:right;">
p100
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
data
</td>
<td style="text-align:right;">
24
</td>
<td style="text-align:right;">
0.99
</td>
<td style="text-align:right;">
52247.25
</td>
<td style="text-align:right;">
25173.08
</td>
<td style="text-align:right;">
1730
</td>
<td style="text-align:right;">
35303
</td>
<td style="text-align:right;">
51381.5
</td>
<td style="text-align:right;">
68522
</td>
<td style="text-align:right;">
666666
</td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

Though the proportion of missing data in the Income column is only 1.1%,
I will fill up these missing values with either mean or median to make
the dataset complete. It will rely on the normality of the data or the
presence of outliers. The computation will be affected by variables
**education level**, **age**, and **country of the customer**. These are
the only information I can rely on from the dataset.

Following table shows how many many missing values by country and
education.

``` r
# Examine the characteristics of individual missing salary. 

md_na <- md[is.na(md$Income),] %>% 
  dplyr::select(ID, Education, Country) %>% 
  group_by(Country, Education) %>% 
  count()

md_na
```

    ## # A tibble: 14 x 3
    ## # Groups:   Country, Education [14]
    ##    Country Education      n
    ##    <fct>   <fct>      <int>
    ##  1 AUS     2n Cycle       1
    ##  2 AUS     Graduation     6
    ##  3 AUS     Master         3
    ##  4 AUS     PhD            3
    ##  5 CA      Graduation     1
    ##  6 CA      PhD            1
    ##  7 GER     2n Cycle       1
    ##  8 GER     Graduation     1
    ##  9 GER     Master         1
    ## 10 GER     PhD            1
    ## 11 IND     2n Cycle       1
    ## 12 SP      Graduation     2
    ## 13 US      Graduation     1
    ## 14 US      Master         1

I have 2 options when filling up these missing values, either to use the
median or mean. I will use boxplot to help making the decision.

``` r
md_complete <- md[complete.cases(md),]

ggplot(md_complete, aes(x = Education, y = Income)) +
  geom_boxplot(outlier.shape = NA) +
  geom_jitter(colour = "blue", alpha = 0.5, width = 0.2) +
  facet_wrap(~Country, scale = "free") +
  stat_boxplot(geom = "errorbar")
```

![](marketing_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

Insights:

-   For **AUS** group, I will use *mean* for the missing value in the 2n
    Cycle, Graduation, Master, and PhD education levels.

-   For **CA**, it is better to use *median* to fill up the missing
    value in the PhD dataset because of the presence of extreme outlier.

-   For **GER**, I will use *mean* to fill up missing values in teh 2n
    Cycle, Graduation, Master, and PhD education levels.

-   For **IND**, I will use *mean* to fill up the missing value in the
    2n Cycle education level.

-   For **SP**, I will use *median* to fill up the missing value in the
    Graduation education level.

-   For **US**, I will use *mean* to fill up the missing value in the
    Graduation and Master education levels.

Following codes complete the compuations.

``` r
md2 <- md %>% 
  group_by(Country, Education) %>% 
  mutate(Income = ifelse(Country == "AUS" & is.na(Income), mean(Income, na.rm = T), Income),
         Income = ifelse(Country == "CA" & is.na(Income), median(Income, na.rm = T), Income),
         Income = ifelse(Country == "GER" & is.na(Income), mean(Income, na.rm = T), Income),
         Income = ifelse(Country == "IND" & is.na(Income), mean(Income, na.rm = T), Income),
         Income = ifelse(Country == "SP" & is.na(Income), median(Income, na.rm = T), Income),
         Income = ifelse(Country == "US" & is.na(Income), mean(Income, na.rm =T), Income)) %>% 
  ungroup()
```

Checking is there any more NA in the md2 dataset. The result shown 0
rows, meanning the conversion is successful.

``` r
# Checking is there any more NA in the md2 dataset
md2[!complete.cases(md2), ]  
```

    ## # A tibble: 0 x 28
    ## # ... with 28 variables: ID <dbl>, Year_Birth <dbl>, Education <fct>,
    ## #   Marital_Status <fct>, Income <dbl>, Kidhome <dbl>, Teenhome <dbl>,
    ## #   Dt_Customer <date>, Recency <dbl>, MntWines <dbl>, MntFruits <dbl>,
    ## #   MntMeatProducts <dbl>, MntFishProducts <dbl>, MntSweetProducts <dbl>,
    ## #   MntGoldProds <dbl>, NumDealsPurchases <dbl>, NumWebPurchases <dbl>,
    ## #   NumCatalogPurchases <dbl>, NumStorePurchases <dbl>,
    ## #   NumWebVisitsMonth <dbl>, AcceptedCmp3 <dbl>, AcceptedCmp4 <dbl>, ...

Checking the 24 rows that had no income data in the beginning. They have
now been filed up with newly computed income data based on mean or
median, based on country and education level. Following result shows
that the computation has been successful.

``` r
# Getting the 24 rows that had missing values

NA_locate <- which(!complete.cases(md))

# Checking newly computed Income. 

md2_check <- md2 %>% dplyr::select(Country, Education, Income)
md2_check[NA_locate,]
```

    ## # A tibble: 24 x 3
    ##    Country Education  Income
    ##    <fct>   <fct>       <dbl>
    ##  1 GER     PhD        57845.
    ##  2 US      Graduation 52576.
    ##  3 AUS     PhD        52770.
    ##  4 AUS     Graduation 53555.
    ##  5 CA      PhD        59187 
    ##  6 GER     2n Cycle   43183 
    ##  7 US      Master     54154.
    ##  8 GER     Graduation 55840.
    ##  9 AUS     2n Cycle   45892.
    ## 10 AUS     Master     51995.
    ## # ... with 14 more rows

### 5.4 Create Age Column

Since there is year of birth recorded in the dataset, an **“age”**
column can be pre-prepared just in case if this information is required
in the later stages. I compute the age by using the enrollment rate
minus the year of birth and synthese a column named
**“Age\_atRegister”**. A column **“age\_group”** has also been
synthesised base on the **“Age\_atRegister”** column.

Following code complete the creation.

``` r
# set up the data frame

md2 <- md2 %>% 
  mutate(age = year(Dt_Customer) - Year_Birth + 1,
         age_group = case_when(
           age < 1 ~ "baby",
           age > 1 & age < 14 ~ "youth",
           age > 15 & age < 24 ~ "young.adult",
           age > 25 & age < 44 ~ "middle.adult",
           age > 45 & age < 65 ~ "older.adult",
           TRUE ~ "senior"
         )) %>% 
  relocate(age, .after = Year_Birth) %>% 
  relocate(age_group, .after = age) %>% 
  rename("Age_atRegister" = "age")

# factorise the "age group" column and rearrange the sequence of levels

md2 <- md2 %>% mutate(age_group = factor(age_group, 
                                         levels = c("young.adult", "middle.adult", 
                                                    "older.adult", "senior")))
```

### 5.5 Data processing summary

-   I have converted the variables **Education**, **Marital\_Status**,
    and **Country** into *factor*.

-   I have converted the **Dt\_Customer** from character into *date*
    type.

-   I have removed the dollar and comma signs in the **Income** column
    and converted it into *numerical* type.

-   There are 24 out of 2240 rows of missing values in the **Income**
    column, I have filled them up with mean and median, with
    consideration of respective country and education level.

-   I created two new columns **Age\_atRegister** and **age\_group**.

The dataset is now analysis-ready.

## 6 EXPLORATORY DATA ANALYSIS (EDA)

### 6.1 What does the average customer look like for this company?

In section 6.1, I will explore customer information of the company by
age, country, education, marital status, family size, and income.

#### 6.1.1 Age

The company has customers from 8 different countries, and most of their
customers are aged between 30 to 55. The body of boxplots represent 50%
of the data. Boxplots of each country overlap each other indicating that
there is no difference in age among countries.

-   The country “SP” has the most customers followed by “SA” and “CA”.
    The country “ME” has the least customers with only data from 3
    customers.

-   All countries have similar spread in customer age.

``` r
# set up df

df611 <- md2 %>% 
  group_by(Country) %>% 
  mutate(x_lab = paste0(Country, "\n", "(n= ", n(), ")"))
  
# plot

ggplot(df611, aes(x = x_lab, y = Age_atRegister, fill = Country)) +
  geom_hline(yintercept = 30, linetype = 2, color = "blue") +
  geom_hline(yintercept = 55, linetype = 2, color = "blue") +
  geom_boxplot(outlier.shape = NA, alpha = 0.3) + 
  stat_boxplot(geom = "errorbar") +
  geom_jitter(aes(fill = Country) , shape = 21, alpha = 0.4, width = 0.2) +
  scale_y_continuous(lim = c(0, 80), breaks = seq( 0, 80, 10)) +
  theme(legend.position = "NA",
        axis.title.y = element_text(margin = margin(0, 10, 0, 0)),
        plot.title = element_text(face = "bold")) +
  labs(title = "Figure 1. Distribution of Customer's Age from Different Country",
       y = "Age at Registration") 
```

<img src="marketing_files/figure-gfm/unnamed-chunk-18-1.png" style="display: block; margin: auto;" />

#### 6.1.2 Country

Following pi-chart shows that nearly half of the customers are from
“SP”, which is Spain. The next largest pool of customer is from SA
(South Africa) at 15%, then followed by the third CA (Canada) at 12%.

``` r
# produce dataframe

df_coun <- md2 %>% 
  group_by(Country) %>% 
  summarise(count = n()) %>% 
  mutate(per = round(count / sum(count)*100, 1),
         per = paste0(per, "%"))

# plot

ggplot(df_coun, aes(x = "", y = count, fill = Country)) +
  geom_bar(stat = "identity") +
  coord_polar(theta = "y",
              start = 50) +  
  geom_text(aes(label = paste0(Country, " (", per, ")")), 
            position = position_stack(vjust = 0.5),
            size = 4) +
  theme_minimal() +
  theme(legend.position = "none",
        axis.title = element_blank(),
        plot.title = element_text(face = "bold")) +
  labs(title = "Figure 2. Distribution of Customers from Different Countries")
```

<img src="marketing_files/figure-gfm/unnamed-chunk-19-1.png" style="display: block; margin: auto;" />

#### 6.1.3 Education

-   Overall, most customers have a “Graduation” education level (50.3%).

-   “Graduation”, “PHD” and “Master” customers generally ranked the
    first 3 most important customer group in all country.

``` r
# Set up data frame

df613.1 <- md2 %>%
  group_by(Education) %>% 
  summarise(Count = n()) %>% 
  mutate(per = round(Count/sum(Count)*100, 1),
         per = paste(per,"%") )

# plot

plot_df613.1 <- ggplot(df613.1, aes(x = reorder(Education, -Count), y = Count, fill = Education)) +
  geom_bar(stat = "identity") +
  geom_text(aes(label = per, vjust = -1.2)) +
  scale_y_continuous(lim = c(0, 1200), breaks = seq(0, 1200, 200)) +
  theme(legend.position = "none",
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        plot.title = element_text(face = "bold"),
        axis.text.x = element_text(angle = 50, vjust = 0.75)) +
  labs(x = "Education",
       title = "Figure 3. Education") 


# set up faceted data frame

df613.2 <- md2 %>%
  group_by(Country, Education) %>% 
  summarise(Count = n()) %>% 
  mutate(per = round(Count/sum(Count)*100, 1),
         per = paste0(per, "%"))

# plot

plot_df613.2 <- ggplot(df613.2, aes(x = reorder(Education, -Count), y = Count, fill = Education)) +
  geom_bar(stat = "identity") +
  geom_text(aes(label = per, vjust = -1.2), size = 3) +
  scale_y_continuous(lim = c(0, 1200), breaks = seq(0, 1200, 200)) +
  theme(legend.position = "none",
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        axis.text.x = element_text(angle = 50, vjust = 0.75),
        plot.title = element_text(face = "bold")) +
  labs(x = "Education",
       title = "Figure 4. Education By Countries") +
  facet_wrap(~ Country)
      

# Combine

grid.arrange(plot_df613.1, plot_df613.2,
                         layout_matrix = rbind(c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2)))
```

<img src="marketing_files/figure-gfm/unnamed-chunk-20-1.png" style="display: block; margin: auto;" />

#### 6.1.4 Marital Status

Nearly 40% of the customers are married, 25.6% staying together, and
21.3% are single.

``` r
# set up dataframe

df614 <- md2 %>% 
  group_by(Marital_Status) %>% 
  summarise(count = n()) %>% 
  mutate(per = round(count/sum(count)*100, 1),
         per = paste0(per, "%"))


# plot

plot_df614.1 <- ggplot(df614, aes(x = reorder(Marital_Status, -count), y = count, fill = Marital_Status)) +
  geom_bar(stat = "identity") +
  geom_text(aes(label = per, vjust = -1.2)) +
  scale_y_continuous(lim = c(0, 1200), breaks = seq(0, 1200, 200)) +
  theme(legend.position = "none",
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        plot.title = element_text(face = "bold"),
        axis.text.x = element_text(angle = 50, vjust = 0.75)) +
  labs(x = "Marital_Status",
       title = "Figure 5. Marital_Status")


# set up dataframe2

df614.2 <- md2 %>% 
  group_by(Country, Marital_Status) %>% 
  summarise(count = n()) %>% 
  mutate(per = round(count/sum(count)*100, 1),
         per = paste0(per, "%"))


# plot 

plot_df614.2 <- ggplot(df614.2, aes(x = reorder(Marital_Status, -count), y = count, fill = Marital_Status)) +
  geom_bar(stat = "identity") +
  geom_text(aes(label = per, vjust = -1.2), size = 3) +
  scale_y_continuous(lim = c(0, 1200), breaks = seq(0, 1200, 200)) +
  theme(legend.position = "none",
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        plot.title = element_text(face = "bold"),
        axis.text.x = element_text(angle = 50, vjust = 0.75)) +
  labs(x = "Marital_Status",
       title = "Figure 6. Marital_Status by countries") +
  facet_wrap(~ Country)


# Combine

grid.arrange(plot_df614.1, plot_df614.2,
                         layout_matrix = rbind(c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2),
                                   c(1,1,1,2,2,2,2,2)))
```

<img src="marketing_files/figure-gfm/unnamed-chunk-21-1.png" style="display: block; margin: auto;" />

#### 6.1.5 Customer’s Family size

-   Only 28.5% of customers have no children (either at least a kid or
    teen in the family).

-   71.5% of customers have at least 1 kid or 1 teen in the family.

``` r
# set up df

df615_0 <- md2 %>% 
  mutate(Familysize = paste0(Kidhome, " Kid ", Teenhome, " Teen")) %>% 
  dplyr::select(Familysize)

df615_1 <- df615_0 %>% 
  group_by(Familysize) %>% 
  summarise(Count = n()) %>% 
  mutate(per = round(Count/sum(Count)*100, 1),
         per = paste(per, "%"),
         Familysize = factor(Familysize))

# plot

ggplot(df615_1, aes(x = reorder(Familysize, -Count), y = Count, fill = Familysize)) +
  geom_bar(stat = "identity") +
  geom_text(aes(label = per), size = 4, vjust = -0.8) +
  theme_bw() +
  theme(legend.position = "none",
        axis.text.x = element_text(angle = 25, vjust = 0.5),
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        axis.title.y = element_text(margin = margin(0, 10, 0, 0))) +
  scale_y_continuous(lim = c(0, 800)) +
  labs(title = "Figure 7. Bar Chart of Family Size among Customers",
       x = "Family Size")
```

<img src="marketing_files/figure-gfm/unnamed-chunk-22-1.png" style="display: block; margin: auto;" />

#### 6.1.6 Income

The average and median income of customer is $52,250 and $51,550. The
mean and median income is not very far away from each other, I would
assume a normal distribution around the mean and median. The maximum and
minimum incomes might be outliers.

``` r
summary(md2$Income)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1730   35539   51550   52250   68290  666666

-   I am 95% confidence that the true mean is falling between $51,212.46
    and $53,287.48.

``` r
t.test(md2$Income)
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  md2$Income
    ## t = 98.759, df = 2239, p-value < 2.2e-16
    ## alternative hypothesis: true mean is not equal to 0
    ## 95 percent confidence interval:
    ##  51212.46 53287.48
    ## sample estimates:
    ## mean of x 
    ##  52249.97

-   50% of customers have income falls approximately between $35k to
    $70k.

``` r
ggplot(md2, aes(x = Income)) +
  geom_boxplot(fill = "purple", alpha = 0.5, size = 1, width = 0.1)  +
  scale_x_continuous(lim = c(0, 200000),
                     breaks = seq(0, 200000, 20000),
                     labels = function(x)paste0("$", {x/1000}, "k")) +
  theme_classic() +
  theme(plot.title = element_text(face = "bold"),
        axis.text.y = element_blank(),
        axis.ticks.y = element_blank()) +
  labs(title = "Figure 8. Boxplot to show income distribution",
       subtitle = "A outlier point at $666,666 has been removed")
```

<img src="marketing_files/figure-gfm/unnamed-chunk-25-1.png" style="display: block; margin: auto;" />
\* Income among education levels are not obviously different from each
other except the customers from basic education level, they have the
lowest income.

``` r
ggplot(md2, aes(y = Income, x = age_group, fill = Education)) +
  geom_boxplot(alpha = 0.5, size = 1)  +
  scale_y_continuous(lim = c(0, 200000),
                     breaks = seq(0, 200000, 20000),
                     labels = function(x)paste0("$", {x/1000}, "k")) +
  theme_bw() +
  theme(plot.title = element_text(face = "bold"),
        axis.text.x = element_text(angle = 90, vjust = -0.15),
        axis.title.x = element_text(vjust = -2),
        legend.position = "none") +
  labs(title = "Figure 8. Boxplot to show income distribution",
       subtitle = "A outlier point at $666,666 has been removed",
       x = "Age Group") +
  facet_wrap(~ Education, nrow = 1) 
```

<img src="marketing_files/figure-gfm/unnamed-chunk-26-1.png" style="display: block; margin: auto;" />

### 6.2 Which products are performing the best?

Products of the company include wines, fruits, meat, fish, sweet, and
gold. Wine is the best selling products of the company which
contributing 50.15% to the total revenue, followed by 27.56% of meat and
then the 7.27% of gold.

``` r
# set up df

df6.2 <- md2 %>% 
  dplyr::select(MntWines, MntFruits, MntMeatProducts, 
         MntFishProducts, MntSweetProducts, MntGoldProds) %>% 
  rename("Wine" = "MntWines",
         "Fruit" = "MntFruits",
         "Meat" = "MntMeatProducts",
         "Fish" = "MntFishProducts",
         "Sweet" = "MntSweetProducts",
         "Gold" = "MntGoldProds") %>% 
  pivot_longer(c(Wine, Fruit, Meat, Fish, Sweet, Gold),
               names_to = "products",
               values_to = "amount_spent") %>% 
  group_by(products) %>% 
  summarise(total_revenue = sum(amount_spent)) %>% 
  mutate(per = round(total_revenue/sum(total_revenue)*100, 2),
         per = paste0(per, "%"),
         lbl = paste0("$", prettyNum(total_revenue,big.mark = ","), "\n", "(", per, ")"))

  
# plot

ggplot(df6.2, aes(x = reorder(products, -total_revenue), 
                  y = total_revenue, fill = products, colour = products)) +
  geom_bar(stat = "identity", alpha = 0.5) +
  geom_text(aes(label = lbl), colour = "black", vjust = -0.3) +
  theme_classic() +
  theme(legend.position = "none") +
  scale_y_continuous(lim = c(0, 800000),  
                     labels = function(x)paste0("$", {x/1000}, "k")) +
  labs(title = "Figure 9. Performance of Each Product Category",
       x = "Product Category",
       y = "Total Revenue")
```

<img src="marketing_files/figure-gfm/unnamed-chunk-27-1.png" style="display: block; margin: auto;" />

### 6.3 Which marketing campaign is most successful?

There are actually 6 marketing campaigns in the dataset, including the 5
campaigns that have already been launched and the last marketing
campaign is actually the column “Response”. Refer to section 4.2.

The last marketing campaign was the most successful campaign with
acceptance rate at 14.91%. It is a value that is nearly doubling the
acceptance rate of most of the other marketing campaigns launched.

``` r
# Set up data frame 

df6.3 <- md2 %>%
  dplyr::select(ID, AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, Response) %>% 
  pivot_longer(c(AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, Response),
               names_to = "Campaign",
               values_to = "Reaction")  # Reaction 1 = accepted the offer, 0 means otherwise

df6.3.2 <- df6.3 %>% 
  group_by(Campaign) %>% 
  summarise(Count = n(),
            Acceptance_rate = sum(Reaction)/Count*100,
            Acceptance_rate2 = paste0(round(sum(Reaction)/Count*100, 2), "%")) %>% 
  mutate(Campaign = fct_recode(Campaign,
         "First" = "AcceptedCmp1",
         "Second" = "AcceptedCmp2",
         "Third" = "AcceptedCmp3",
         "Fourth" = "AcceptedCmp4",
         "Fifth" = "AcceptedCmp5",
         "Last" = "Response"))
  

# plot

ggplot(df6.3.2, aes(x = Campaign, y = Acceptance_rate, group = 1)) +
  geom_point(stat = "identity", size = 3.5, colour = "purple") +
  geom_path(linetype = 2, size = 1, colour = "purple") +
  geom_label_repel(aes(label = Acceptance_rate2), nudge_y = 2) +
  theme_classic() +  
  scale_y_continuous(lim = c(0, 20), breaks = seq(0, 20, 4)) +
  labs(title = "Figure 10. Accentance Rates of Each Marketing Campaign",
       y = "Acceptance Rate (%)") +
  theme(axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        axis.title.y = element_text(margin = margin(0, 10, 0, 0)),
        plot.title = element_text(face = "bold"))
```

<img src="marketing_files/figure-gfm/unnamed-chunk-28-1.png" style="display: block; margin: auto;" />

### 6.4 Which channels are underperforming?

There are 3 sales channels recorded in the given dataset, the company
website, catalog, and in-store purchase. Catalog was the most
underperforming sale channel, followed by purchases made through company
web. Most purchases were made in store.

``` r
# set up dataframe for this section

df6.4 <- md2 %>% 
  dplyr::select(NumWebPurchases, NumCatalogPurchases, NumStorePurchases) %>% 
  rename("Web" = "NumWebPurchases",
         "Catalog" = "NumCatalogPurchases",
         "In_store" = "NumStorePurchases") %>% 
  pivot_longer(c(Web, Catalog, In_store),
               names_to = "channels",
               values_to = "No_of_purchases") 

df6.4 <- df6.4 %>% 
  group_by(channels) %>% 
  summarise(total_no_of_purchases = sum(No_of_purchases))

# plot the graph

ggplot(df6.4, aes(x = reorder(channels, -total_no_of_purchases), y = total_no_of_purchases)) +
  geom_bar(stat = "identity", fill = "white", aes(colour = channels), size = 1) +
  geom_text(aes(label = channels), 
            vjust = -2.5, fontface = "bold") +
   geom_text(aes(label = paste0("Count: ", prettyNum(total_no_of_purchases, big.mark = ","))), 
            vjust = -1) +
  theme_minimal() +
  labs(title = "Figure 11. Comparison of Sale Channels",
       x = "Sale Channels",
       y = "Total No. of Purchases") +
  theme(plot.margin = unit(c(1,1,1,1), "cm"),
        plot.title = element_text(vjust = 2, hjust = 0.5, face = "bold"),
        legend.position = "none") +
  scale_y_continuous(lim = c(0, 15000),
                     breaks = seq(0, 15000, 2000))
```

![](marketing_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

## 7 STATISTICAL ANALYSIS

### 7.1 Testing for multicollinearity

The preliminary step before statistical analysis is to check
correlations between numerical independent variables within the dataset
to avoid significant pairs being used in the same model, as it would
make coefficient estimates unstable and creating invalid statistical
results. It is known as multicollinearity,
[detail](https://blog.minitab.com/en/understanding-statistics/handling-multicollinearity-in-regression-analysis).

#### 7.1.1 Correlation assessment

The rule of thumb is that if **correlation is greater than 0.8** between
two independent variables, then multicollinearity would exist. Following
table successfully present the correlation between each numerical
variables in the dataset.

One can just look for correlation values that are 0.8 but not equal to
1, then refer to the variables that associated with this value. This
value range indicates possible existence of multicollinearity.

``` r
# Filter non-numerical and binary variable, to select only numerical variables (predictors) to test relationships among themselve. 

df7.1 <- md2 %>%  dplyr::select(Year_Birth, Age_atRegister, Income, Kidhome, Teenhome, MntWines, MntFruits, MntMeatProducts, MntFishProducts, MntSweetProducts, MntGoldProds, NumDealsPurchases, NumWebPurchases, NumCatalogPurchases, NumStorePurchases, NumWebVisitsMonth, Response) %>% 
  ungroup()

# Correlation test of each pair

round(cor(df7.1),2)
```

    ##                     Year_Birth Age_atRegister Income Kidhome Teenhome MntWines
    ## Year_Birth                1.00          -1.00  -0.16    0.23    -0.35    -0.16
    ## Age_atRegister           -1.00           1.00   0.16   -0.23     0.35     0.15
    ## Income                   -0.16           0.16   1.00   -0.43     0.02     0.58
    ## Kidhome                   0.23          -0.23  -0.43    1.00    -0.04    -0.50
    ## Teenhome                 -0.35           0.35   0.02   -0.04     1.00     0.00
    ## MntWines                 -0.16           0.15   0.58   -0.50     0.00     1.00
    ## MntFruits                -0.02           0.01   0.43   -0.37    -0.18     0.39
    ## MntMeatProducts          -0.03           0.03   0.58   -0.44    -0.26     0.56
    ## MntFishProducts          -0.04           0.04   0.44   -0.39    -0.20     0.40
    ## MntSweetProducts         -0.02           0.01   0.44   -0.37    -0.16     0.39
    ## MntGoldProds             -0.06           0.05   0.32   -0.35    -0.02     0.39
    ## NumDealsPurchases        -0.06           0.05  -0.08    0.22     0.39     0.01
    ## NumWebPurchases          -0.15           0.14   0.38   -0.36     0.16     0.54
    ## NumCatalogPurchases      -0.12           0.12   0.59   -0.50    -0.11     0.64
    ## NumStorePurchases        -0.13           0.12   0.53   -0.50     0.05     0.64
    ## NumWebVisitsMonth         0.12          -0.13  -0.55    0.45     0.13    -0.32
    ## Response                  0.02          -0.03   0.13   -0.08    -0.15     0.25
    ##                     MntFruits MntMeatProducts MntFishProducts MntSweetProducts
    ## Year_Birth              -0.02           -0.03           -0.04            -0.02
    ## Age_atRegister           0.01            0.03            0.04             0.01
    ## Income                   0.43            0.58            0.44             0.44
    ## Kidhome                 -0.37           -0.44           -0.39            -0.37
    ## Teenhome                -0.18           -0.26           -0.20            -0.16
    ## MntWines                 0.39            0.56            0.40             0.39
    ## MntFruits                1.00            0.54            0.59             0.57
    ## MntMeatProducts          0.54            1.00            0.57             0.52
    ## MntFishProducts          0.59            0.57            1.00             0.58
    ## MntSweetProducts         0.57            0.52            0.58             1.00
    ## MntGoldProds             0.39            0.35            0.42             0.37
    ## NumDealsPurchases       -0.13           -0.12           -0.14            -0.12
    ## NumWebPurchases          0.30            0.29            0.29             0.35
    ## NumCatalogPurchases      0.49            0.72            0.53             0.49
    ## NumStorePurchases        0.46            0.48            0.46             0.45
    ## NumWebVisitsMonth       -0.42           -0.54           -0.45            -0.42
    ## Response                 0.13            0.24            0.11             0.12
    ##                     MntGoldProds NumDealsPurchases NumWebPurchases
    ## Year_Birth                 -0.06             -0.06           -0.15
    ## Age_atRegister              0.05              0.05            0.14
    ## Income                      0.32             -0.08            0.38
    ## Kidhome                    -0.35              0.22           -0.36
    ## Teenhome                   -0.02              0.39            0.16
    ## MntWines                    0.39              0.01            0.54
    ## MntFruits                   0.39             -0.13            0.30
    ## MntMeatProducts             0.35             -0.12            0.29
    ## MntFishProducts             0.42             -0.14            0.29
    ## MntSweetProducts            0.37             -0.12            0.35
    ## MntGoldProds                1.00              0.05            0.42
    ## NumDealsPurchases           0.05              1.00            0.23
    ## NumWebPurchases             0.42              0.23            1.00
    ## NumCatalogPurchases         0.44             -0.01            0.38
    ## NumStorePurchases           0.38              0.07            0.50
    ## NumWebVisitsMonth          -0.25              0.35           -0.06
    ## Response                    0.14              0.00            0.15
    ##                     NumCatalogPurchases NumStorePurchases NumWebVisitsMonth
    ## Year_Birth                        -0.12             -0.13              0.12
    ## Age_atRegister                     0.12              0.12             -0.13
    ## Income                             0.59              0.53             -0.55
    ## Kidhome                           -0.50             -0.50              0.45
    ## Teenhome                          -0.11              0.05              0.13
    ## MntWines                           0.64              0.64             -0.32
    ## MntFruits                          0.49              0.46             -0.42
    ## MntMeatProducts                    0.72              0.48             -0.54
    ## MntFishProducts                    0.53              0.46             -0.45
    ## MntSweetProducts                   0.49              0.45             -0.42
    ## MntGoldProds                       0.44              0.38             -0.25
    ## NumDealsPurchases                 -0.01              0.07              0.35
    ## NumWebPurchases                    0.38              0.50             -0.06
    ## NumCatalogPurchases                1.00              0.52             -0.52
    ## NumStorePurchases                  0.52              1.00             -0.43
    ## NumWebVisitsMonth                 -0.52             -0.43              1.00
    ## Response                           0.22              0.04              0.00
    ##                     Response
    ## Year_Birth              0.02
    ## Age_atRegister         -0.03
    ## Income                  0.13
    ## Kidhome                -0.08
    ## Teenhome               -0.15
    ## MntWines                0.25
    ## MntFruits               0.13
    ## MntMeatProducts         0.24
    ## MntFishProducts         0.11
    ## MntSweetProducts        0.12
    ## MntGoldProds            0.14
    ## NumDealsPurchases       0.00
    ## NumWebPurchases         0.15
    ## NumCatalogPurchases     0.22
    ## NumStorePurchases       0.04
    ## NumWebVisitsMonth       0.00
    ## Response                1.00

Though inspecting the table visually is an option, I can also use codes
to help filtering the data for me. Following codes help me to check the
presence of correlation values that fall between 0.8 to 1.

-   There is no multicollinearity in the dataset.

``` r
# Checking.

cor.table <- data.frame(round(cor(df7.1),2))

cor.table <- cor.table %>% 
  rownames_to_column(var = "x1") %>% 
  pivot_longer(c(2:18),
               names_to = "x2",
               values_to = "correlation")

# filter to get correlation that is higher than 0.8 but is not 1

cor.table %>% filter(correlation > 0.8 & correlation < 1)
```

    ## # A tibble: 0 x 3
    ## # ... with 3 variables: x1 <chr>, x2 <chr>, correlation <dbl>

#### 7.1.2 Variance Inflation factor (VIF) assessment

As a rule of thumb, VIF should be less than 4 to have no
multicollinearity issue (the Pennsylvania State University 2018). The
result should be the same as previous correlation analysis. Apart from
the first two variables “Year\_Birth” and “Age\_atRegister”, there is no
multicollinearity exists in all variables. The two variables are
essentially the same thing, I created “age\_atRegister” from the
“Year\_Birth”. I will only use one of them in any model because they
represent the same information.

``` r
model_vif <- lm(NumStorePurchases ~. , data = df7.1)
vif(model_vif)
```

    ##          Year_Birth      Age_atRegister              Income             Kidhome 
    ##          378.833154          379.086706            2.159072            1.818572 
    ##            Teenhome            MntWines           MntFruits     MntMeatProducts 
    ##            1.604499            2.385003            1.908478            2.909310 
    ##     MntFishProducts    MntSweetProducts        MntGoldProds   NumDealsPurchases 
    ##            2.068151            1.893030            1.491667            1.591688 
    ##     NumWebPurchases NumCatalogPurchases   NumWebVisitsMonth            Response 
    ##            1.871632            2.960579            2.403747            1.147800

### 7.2 Factors that significantly related to in-store purchases

#### 7.2.1 Data Partitioning

Following codes split the data into 80% training set and 20% testing
set. The training set will be used to build the model to answer this
question. The quality of the model will be tested by the result of
prediction made on the testing set in terms of RSME (Root Mean Squared
Error) and R2. The model will then be used to look for factors that are
significantly related to in-store purchases.

``` r
set.seed(123) 

# Create Data partition

training.data <- md2$NumStorePurchases %>% createDataPartition(p = 0.8, list = F)

# Produce train and test set

train.data <- md2[training.data,] 
test.data <- md2[-training.data,]
```

#### 7.2.2 Building the model and model performance

Building the model with exclusion of variables: ID, Year\_Birth,
Age\_atRegister, Dt\_Customer, AcceptedCmp1, AcceptedCmp2, AcceptedCmp3,
AcceptedCmp4, AcceptedCmp5, Response. They are either redundant or
irrelevant of the context.

``` r
# Build the model

model721 <- lm(NumStorePurchases ~ . - ID - Year_Birth - Age_atRegister - Dt_Customer - AcceptedCmp1 - AcceptedCmp2 - AcceptedCmp3 - AcceptedCmp4 - AcceptedCmp5 - Response , data = train.data)

# Make the prediction based on the 20% test.data

predictions <- model721 %>% predict(test.data)
```

**Model Performance**

-   RMSE - the lower the RMSE, the lower the error, the better the
    model. The RMSE is 2.12, which is lower than the median of the
    responding variable, which indicating that it is a good model for
    prediction.

``` r
RMSE(predictions, test.data$NumStorePurchases)
```

    ## [1] 2.214403

``` r
median(test.data$NumStorePurchases)
```

    ## [1] 5

-   R2 - the higher the R2, the better the squared correlation, the
    better the model. The correlation is moderate. The best range is
    generally 0.75 and above. Since RMSE is indicating it is a good
    model, I will proceed to the next step.

``` r
R2(predictions, test.data$NumStorePurchases)
```

    ## [1] 0.527389

#### 7.2.3 Summarise the model

Factors that significantly related (P-value &lt; 0.05) to in-store
purchases in a positive way are:

``` r
model721_sum <- summary(model721)

# Extract significant variables (<0.05)

model721_sum_df <- model721_sum$coefficients %>% 
  data.frame() %>% 
  dplyr::select(Estimate, Pr...t..) %>% 
  rename("P_value" = Pr...t..) %>% 
  filter(P_value < 0.05) %>% 
  arrange(P_value)

# Positive related predictors

model721_sum_df %>% 
  filter(Estimate > 0) %>% 
  arrange(P_value) %>% 
  kbl %>% 
  kable_styling(bootstrap_options = c("hover", "bordered")) 
```

<table class="table table-hover table-bordered" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
Estimate
</th>
<th style="text-align:right;">
P\_value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
MntWines
</td>
<td style="text-align:right;">
0.0033677
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
NumDealsPurchases
</td>
<td style="text-align:right;">
0.2809073
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
NumWebPurchases
</td>
<td style="text-align:right;">
0.1513479
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
MntFruits
</td>
<td style="text-align:right;">
0.0071848
</td>
<td style="text-align:right;">
0.0000379
</td>
</tr>
<tr>
<td style="text-align:left;">
Income
</td>
<td style="text-align:right;">
0.0000194
</td>
<td style="text-align:right;">
0.0000607
</td>
</tr>
<tr>
<td style="text-align:left;">
MntFishProducts
</td>
<td style="text-align:right;">
0.0050058
</td>
<td style="text-align:right;">
0.0001911
</td>
</tr>
<tr>
<td style="text-align:left;">
MntSweetProducts
</td>
<td style="text-align:right;">
0.0050623
</td>
<td style="text-align:right;">
0.0026724
</td>
</tr>
</tbody>
</table>

-   For every 1 unit increase in the predictors, the number of store
    purchases will increase by respective estimate.

Factors that significantly related to In-store purchases in a negative
way are:

``` r
model721_sum_df %>% 
  filter(Estimate < 0) %>% 
  arrange(P_value) %>% 
  kbl %>% 
  kable_styling(bootstrap_options = c("hover", "bordered"))
```

<table class="table table-hover table-bordered" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
Estimate
</th>
<th style="text-align:right;">
P\_value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
NumWebVisitsMonth
</td>
<td style="text-align:right;">
-0.2559337
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Kidhome
</td>
<td style="text-align:right;">
-0.8559300
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
NumCatalogPurchases
</td>
<td style="text-align:right;">
-0.1005562
</td>
<td style="text-align:right;">
0.0007278
</td>
</tr>
<tr>
<td style="text-align:left;">
MntMeatProducts
</td>
<td style="text-align:right;">
-0.0009306
</td>
<td style="text-align:right;">
0.0160148
</td>
</tr>
</tbody>
</table>

-   For every 1 unit increment in the predictors, the number of store
    purchases will decrease by respective estimate.

------------------------------------------------------------------------

### Lasso

``` r
library(glmnet)
```

    ## Loading required package: Matrix

    ## 
    ## Attaching package: 'Matrix'

    ## The following objects are masked from 'package:tidyr':
    ## 
    ##     expand, pack, unpack

    ## Loaded glmnet 4.1-2

``` r
model_lasso <- train(NumStorePurchases ~., train.data,
                     method = "glmnet",
                     trControl = trainControl(method = "repeatedcv", 
                                              number = 10, 
                                              repeats = 3),
                     tuneGrid = expand.grid(alpha = 1,
                                            lambda = 10^seq(-3, 3, length = 100)))
```

    ## Warning in nominalTrainWorkflow(x = x, y = y, wts = weights, info = trainInfo, :
    ## There were missing values in resampled performance measures.

``` r
model_lasso$bestTune
```

    ##    alpha     lambda
    ## 25     1 0.02848036

``` r
plot(model_lasso$finalModel, xvar = "dev", label = T)
```

![](marketing_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

``` r
summary(model_lasso$bestTune)
```

    ##      alpha       lambda       
    ##  Min.   :1   Min.   :0.02848  
    ##  1st Qu.:1   1st Qu.:0.02848  
    ##  Median :1   Median :0.02848  
    ##  Mean   :1   Mean   :0.02848  
    ##  3rd Qu.:1   3rd Qu.:0.02848  
    ##  Max.   :1   Max.   :0.02848

``` r
plot(varImp(model_lasso))
```

![](marketing_files/figure-gfm/unnamed-chunk-39-2.png)<!-- -->

### 7.3 Does US’s purchasing power significantly better than the rest of the world in terms of total purchases ?

#### 7.3.1 Comparing total purchases PER CUSTOMER in different country\*\*

A column of new variable “total\_purchases” will be synthesied using
“NumWebPurchases”, “NumCatalogPurchases”, and “NumStorePurchases”.
Following codes create the new variable.

``` r
# set up data frame

df7.3 <- md2 %>% 
  dplyr::select(Country, NumWebPurchases, NumCatalogPurchases, NumStorePurchases) %>% 
  mutate(total_purchases = NumWebPurchases + NumCatalogPurchases + NumStorePurchases) %>% 
  dplyr::select(-NumWebPurchases, -NumCatalogPurchases, -NumStorePurchases)
```

**Building the model**

Following codes build the model.

``` r
model7.3 <- aov(total_purchases ~ Country, data = df7.3)
```

#### 7.3.2 Assumption tests

**Normality test with Q-Q plot**

The assumption of residuals normality is violated based on following Q-Q
plot.

``` r
df7.3$residuals <-  model7.3$residuals

ggplot(df7.3, aes(sample = residuals)) +
  stat_qq_band() +
  stat_qq_line() +
  stat_qq_point() +
  labs(title = "Figure 12. QQ-plot",
       subtitle = "Shaded region = 95% confidence interval for Normality") +
  theme(plot.title = element_text(face = "bold"))
```

![](marketing_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

**Variance test with Levene’s test**

Levene’s test shows that the variance of total purchase in each country
are the similar, without significant differences with a p-value of
larger than 0.05.

``` r
leveneTest(df7.3$total_purchases, df7.3$Country)
```

    ## Levene's Test for Homogeneity of Variance (center = median)
    ##         Df F value Pr(>F)
    ## group    7  1.1192 0.3479
    ##       2232

#### 7.3.4 Kruskal Wallis statistical test

A kruskal wallies test is selected as the omnibus test. The result shows
that there is no significant difference (P-value = 0.4004) among
countries in term of total purchases per customer.

Therefore, we have not enough significant evidence to say that customer
in a country can purchase more items than another country in this
dataset. Customers located in a country that has less customers from the
company is able to purchase similar or more items than a country that
has many customers from the company.

``` r
kruskal.test(df7.3$total_purchases, df7.3$Country)
```

    ## 
    ##  Kruskal-Wallis rank sum test
    ## 
    ## data:  df7.3$total_purchases and df7.3$Country
    ## Kruskal-Wallis chi-squared = 7.2796, df = 7, p-value = 0.4004

#### 7.3.5 Visualisation

In term of total purchase by count, US ranked the second last country.

``` r
df7.3.2 <- df7.3 %>% 
  group_by(Country) %>% 
  summarise(total_purchases_country = sum(total_purchases))


ggplot(df7.3.2, aes(x = reorder(Country, -total_purchases_country), y = total_purchases_country, fill = Country)) +
  geom_bar(stat = "identity") +  
  scale_fill_manual(values = c("darkgreen", "darkgreen", "darkgreen", "darkgreen",
                               "darkgreen", "darkgreen", "darkgreen", "orange")) +      # the location of US level is 7th
  geom_text(aes(label = total_purchases_country), vjust = -1) +
  scale_y_continuous(lim = c(0, 15000)) +
  labs(x = "Country",
       y = "Total Purchases (Count)",
       title = "Figure 13. Comparison of Total purchases in each Country") +
  theme(legend.position = "none",
        plot.title = element_text(face = "bold"))
```

<img src="marketing_files/figure-gfm/unnamed-chunk-45-1.png" style="display: block; margin: auto;" />
However, US ranked the second in term of average purchase per customer
(figure 14). It suggests that US customers have slightly better
purchasing power than the rest of the World in terms of total purchases,
but not statistical significance.

``` r
df7.3.3 <- df7.3 %>% 
  group_by(Country) %>% 
  summarise(count = n(),
            total_purchase_country = sum(total_purchases),
            average_purchase_customer = round(total_purchase_country/count, 2)) %>% 
  mutate(x_label = paste0(Country, "\n", "(n = ", count, ")"))

ggplot(df7.3.3, aes(x = x_label, y = average_purchase_customer, colour = Country)) +
  geom_point(shape = 21, size = 5) +
  geom_text_repel(aes(label = average_purchase_customer), fontface = "bold") +
  theme_classic() +
  theme(legend.position = "none",
        plot.title = element_text(face = "bold", vjust = 2),
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        axis.title.y = element_text(margin = margin(0, 10, 0, 0))) +
  scale_colour_manual(values = c("darkgreen", "darkgreen", "darkgreen", "darkgreen",
                               "darkgreen", "darkgreen", "darkgreen", "orange")) +
  labs(title = "Figure 14. US Customer Buy More in Average than Most of Country",
       x = "Country",
       y = "Average purchase per Customer")
```

<img src="marketing_files/figure-gfm/unnamed-chunk-46-1.png" style="display: block; margin: auto;" />

### 7.4 Are gold lovers prefer to shop in store?

One of the supervisors associated with the dataset insists that people
who buy gold are more conservative. Therefore, people who spent an above
average amount on gold in the last 2 years would have more in store
purchases. I will justify or refute this statement using an appropriate
statistical test in this section.

The average (mean) amount spent on gold is 44.02. Therefore, the
supervisor is claiming that any customer who spent above this amount of
money on gold will have more in store purchases.

``` r
# set up data frame

df7.4 <- md2 %>% 
  dplyr::select(MntGoldProds, NumStorePurchases)

# average 

summary(df7.4$MntGoldProds)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00    9.00   24.00   44.02   56.00  362.00

#### 7.4.1 Visualisation

Following graph shows that many customers who have spent above average
amount on gold "“Above\_average”" purchased more items in the store than
who spent less than the average on gold. The mean and median of the
group “Above\_average” are higher than the group “Below\_average”.
However, is it statistically significant?

``` r
# set up dataframe

df7.4 <- df7.4 %>% 
  mutate(
    Group = case_when(
    MntGoldProds > 44.02 ~ "Above_average", 
    TRUE ~ "Below_average"),
    Group = factor(Group)
    ) %>% 
  group_by(Group) %>% 
  mutate(count = n(),
         xlab = paste0(Group, "\n", "(n = ", count, ")"))


# plot

ggplot(df7.4, aes(x = xlab, y = NumStorePurchases, colour = xlab)) +
  geom_jitter(alpha = 0.5) +
  geom_boxplot(alpha = 0.5, colour = "black", size = 1.5, outlier.shape = NA) +
  theme_classic() +
  theme(legend.position = "none",
        plot.title = element_text(face = "bold", vjust = 2),
        plot.subtitle = element_text(vjust = 2),
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        axis.title.y = element_text(margin = margin(0, 10, 0, 0))) +
  labs(title = "Figure 15. Number of Store Purchase vurses 2 Categories of Gold Buyer",
       subtitle = "Gold buyers categorised into 1) Who spend above, (2) and who spend below average amount on gold",
       y = "Number of Store Purchases (Count)",
       x = "Gold Buyer") +
  stat_boxplot(geom = "errorbar", size = 1.5, colour = "black") +
  stat_summary(fun = "mean", shape = 4, colour = "black", size = 3, stroke = 2)
```

<img src="marketing_files/figure-gfm/unnamed-chunk-48-1.png" style="display: block; margin: auto;" />

It can be argued that “Below\_average” has a lot more data points than
“Above\_average”, the comparison might be unfair. To make it become a
fairer comparison, I randomly select 694 samples from the 1546 samples
in the group of “Below\_average”, and creating following figure.

``` r
# set up data frame 

df7.4.2 <- df7.4 %>%
  dplyr::select(Group, NumStorePurchases) %>% 
  group_by(Group) %>% 
  sample_n(694) %>% 
  mutate(count = n(),
         xlab = paste0(Group, "\n", "(n = ", count, ")"))

# plot

ggplot(df7.4.2, aes(x = xlab, y = NumStorePurchases, colour = xlab)) +
  geom_jitter(alpha = 0.5) +
  geom_boxplot(alpha = 0.5, colour = "black", size = 1.5, outlier.shape = NA) +
  theme_classic() +
  theme(legend.position = "none",
        plot.title = element_text(face = "bold", vjust = 2),
        plot.subtitle = element_text(vjust = 2),
        axis.title.x = element_text(margin = margin(10, 0, 0, 0)),
        axis.title.y = element_text(margin = margin(0, 10, 0, 0))) +
  labs(title = "Figure 16. Number of Store Purchase vurses 2 Categories of Gold Buyer",
       subtitle = "Gold buyers categorised into 1) Who spend above, (2) and who spend below average amount on gold",
       y = "Number of Store Purchases (Count)",
       x = "Gold Buyer") +
  stat_boxplot(geom = "errorbar", size = 1.5, colour = "black") +
  stat_summary(fun = "mean", shape = 4, colour = "black", size = 3, stroke = 2)
```

<img src="marketing_files/figure-gfm/unnamed-chunk-49-1.png" style="display: block; margin: auto;" />
Now, two groups have equal sample size. Reduction of sample size from
1546 to 694 in the group of “Below\_average” leads to a slight reduction
of mean by 0.105. Still, the interpretation of the graph remains the
same as figure 15.

``` r
df7.4 %>% group_by(Group) %>% summarise(ave = mean(NumStorePurchases))
```

    ## # A tibble: 2 x 2
    ##   Group           ave
    ##   <fct>         <dbl>
    ## 1 Above_average  7.77
    ## 2 Below_average  4.90

``` r
df7.4.2 %>% group_by(Group) %>% summarise(ave = mean(NumStorePurchases))
```

    ## # A tibble: 2 x 2
    ##   Group           ave
    ##   <fct>         <dbl>
    ## 1 Above_average  7.77
    ## 2 Below_average  4.93

``` r
4.903622 - 4.798271
```

    ## [1] 0.105351

#### 7.4.2 Building a model

``` r
model742 <- aov(NumStorePurchases ~ Group, data = df7.4.2)
summary(model742)
```

    ##               Df Sum Sq Mean Sq F value Pr(>F)    
    ## Group          1   2782  2781.9     307 <2e-16 ***
    ## Residuals   1386  12558     9.1                   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

#### 7.4.3 Assumption tests

**Normality test with Q-Q plot and Shapiro-Wilk test**

Large amount of data points are out of the shaded region of following
Q-Q plot, and do not form and match the straight line. It suggests that
the data residuals are not normality distributed.

``` r
df7.4.2$residuals <-  model742$residuals

ggplot(df7.4.2, aes(sample = residuals)) +
  stat_qq_band() +
  stat_qq_line() +
  stat_qq_point() +
  labs(title = "Figure 16. QQ-plot",
       subtitle = "Shaded region = 95% confidence interval for Normality") +
  theme(plot.title = element_text(face = "bold"))
```

<img src="marketing_files/figure-gfm/unnamed-chunk-52-1.png" style="display: block; margin: auto;" />

A shapiro-wilk test is also carried out and show the same result that
the residuals in the dataset are not normally distributed.

``` r
by(df7.4.2$NumStorePurchases, df7.4.2$Group, shapiro.test)
```

    ## df7.4.2$Group: Above_average
    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  dd[x, ]
    ## W = 0.96161, p-value = 1.674e-12
    ## 
    ## ------------------------------------------------------------ 
    ## df7.4.2$Group: Below_average
    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  dd[x, ]
    ## W = 0.8331, p-value < 2.2e-16

**Variance test with Levene’s test**

The variance between two gold buyer groups is also significant different
based on following Levene’s test (P-value &lt; 0.05). The variance
between both groups are not equal.

``` r
leveneTest(df7.4.2$NumStorePurchases, df7.4.2$Group)
```

    ## Levene's Test for Homogeneity of Variance (center = median)
    ##         Df F value    Pr(>F)    
    ## group    1  12.176 0.0004992 ***
    ##       1386                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

#### 7.4.4 Mann-Whitney test

For testing groups that do not have their data points normality
distributed and do not have their variances equal to each other,
Mann-Whitney test is selected.

``` r
wilcox.test(df7.4.2$NumStorePurchases ~ df7.4.2$Group)          
```

    ## 
    ##  Wilcoxon rank sum test with continuity correction
    ## 
    ## data:  df7.4.2$NumStorePurchases by df7.4.2$Group
    ## W = 368979, p-value < 2.2e-16
    ## alternative hypothesis: true location shift is not equal to 0

``` r
# default of wilcox.test is for unpaired test, non-normally distributed, unequal variances pair.
```

Statistical result from the test supports the supervisor’s claim that
people who spent an above average amount on gold in the last 2 years
would have more in store purchases, with a p-value of less than 0.05.

### 7.5 Consumption of married PhD candidates on Fish

Fish has Omega 3 fatty acids which are good for the brain. Accordingly,
do “Married PhD candidates” have a significant relation with amount
spent on fish? What other factors are significantly related to amount
spent on fish?

#### 7.5.1 Married PhD candidates vs others in amount spent on fish

Following summary shows that the sample size between the married PhD
group and the other customer groups have a substantial different in
total sample count. To make the comparison fairer, I will randomly
select 192 samples from the 2048 samples of the “Others” group.

``` r
# set up data frame

df751 <- md2 %>% 
  dplyr::select(Education, Marital_Status, MntFishProducts) %>%
  mutate(group = paste0(Education, Marital_Status)) %>% 
  mutate(group2 = case_when(
    group == "PhDMarried" ~ "Married_PhD_candidates",
    TRUE ~ "Others"
  ),
  group2 = as.factor(group2))

# summarise sample count

df751 %>% 
  group_by(group2) %>% 
  summarise(count = n()) 
```

    ## # A tibble: 2 x 2
    ##   group2                 count
    ##   <fct>                  <int>
    ## 1 Married_PhD_candidates   192
    ## 2 Others                  2048

**Random Sampling**

Following codes complete the random sampling of 192 samples from the
“Others” group.

``` r
df751_192 <- df751 %>% 
  dplyr::select(group2, MntFishProducts) %>% 
  group_by(group2) %>% 
  sample_n(192) 
```

**Visualisation**

Figure belows show that the mean and median of the group “Others” are
slightly higher than the group of married PhD.

``` r
# set up x label

df751_192 <- df751_192 %>% 
  group_by(group2) %>% 
  mutate(count = n(),
         label_x = paste0(group2, "\n", "(n =", count, ")"))

# plot

ggplot(df751_192, aes(x = label_x, y = MntFishProducts, fill = group2)) +
  geom_jitter() +
  geom_boxplot(outlier.shape = NA, alpha = 0.9, size = 1) +
  stat_summary(fun = "mean", shape = 4, size = 2, colour = "blue", stroke = 2) +
  labs("Figure 17. Married PhD Candidates have lesser mean and median") +
  theme(legend.position = "none",
        plot.title = element_text(face = "bold"),
        axis.title.x = element_blank(),
        axis.title.y = element_text(margin = margin(0, 10, 0, 0))) +
  labs(y = "Amount spent on fish",
       title = "Figure 17. Married PhD Candidates spent less on Fish",
       subtitle = "In term of mean (x sign) and median (the thicker line in boxplots)")
```

<img src="marketing_files/figure-gfm/unnamed-chunk-58-1.png" style="display: block; margin: auto;" />

**Model building**

Codes below build the model for this section.

``` r
model_192 <- aov(MntFishProducts ~ group2, data = df751_192)
```

**Normality testing with Shapiro-Wilk test**

Shapiro-Wilk test suggests that data between the two groups are not
normally distributed.

``` r
by(df751_192$MntFishProducts, df751_192$group2, shapiro.test)
```

    ## df751_192$group2: Married_PhD_candidates
    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  dd[x, ]
    ## W = 0.69269, p-value < 2.2e-16
    ## 
    ## ------------------------------------------------------------ 
    ## df751_192$group2: Others
    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  dd[x, ]
    ## W = 0.68351, p-value < 2.2e-16

**Variance test with Levene’s test**

Levene’s test concludes that the spread of variance between the two
groups of data are not equal, with a P-value of lower than 0.05, and
rejects the null hypothesis that the variances between the groups are
equal.

``` r
leveneTest(df751_192$MntFishProducts, df751_192$group2)
```

    ## Levene's Test for Homogeneity of Variance (center = median)
    ##        Df F value Pr(>F)
    ## group   1  2.4118 0.1213
    ##       382

**Mann-Whitney test**

Base on above assumption tests, Mann-Whitney test is selected as the
two-sample test, it is written as wilcox.test in R as below.

-   The P-value of 0.0003503 concludes that married PhD candidates spent
    significantly less than other customers on fish.

``` r
wilcox.test(df751_192$MntFishProducts ~ df751_192$group2)
```

    ## 
    ##  Wilcoxon rank sum test with continuity correction
    ## 
    ## data:  df751_192$MntFishProducts by df751_192$group2
    ## W = 15380, p-value = 0.004733
    ## alternative hypothesis: true location shift is not equal to 0

#### 7.5.2 What other factors are significantly related to amount spent on fish?

There are many variables in the dataset can be related to the amount
spent on fish. However, some variables can be either redundant or
irrelevant to this context. I am removing them using following code.

``` r
# set up df

df752 <- md2 %>% dplyr::select(-c(ID, Year_Birth, Age_atRegister, Dt_Customer, AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, Response))
```

**Create Dummy variables**

Linear regressions need variables to be continuous, and assigning dummy
variables (0 or 1) to the levels of categorical variable is a common
practice. Fortunately, R will automatically assign dummy data to
categorical variables that are in factor type. Alternatively, one create
dummy data manually in R. In this section, I will assign dummy data to
categorical variables manually to demonstrate my codes.

Following table indicates successful conversion. The number of variables
has been increased from 20 to 41 because each level of categorical data
had been extracted and formed their own column with value of 1 (yes for
the observation) and 0 (no for the observation).

``` r
# Create the dummy data frame

dummy_object <- dummyVars("~.", data = df752)
dummy752 <- as_tibble(predict(dummy_object, newdata = df752))
dummy752 <- dummy752 %>% rename("Education.2n_Cycle" = "Education.2n Cycle")

# Display the data frame

head(dummy752)
```

    ## # A tibble: 6 x 41
    ##   age_group.young.adult age_group.middle.adult age_group.older~ age_group.senior
    ##                   <dbl>                  <dbl>            <dbl>            <dbl>
    ## 1                     0                      0                0                1
    ## 2                     0                      0                1                0
    ## 3                     0                      0                1                0
    ## 4                     0                      0                1                0
    ## 5                     0                      1                0                0
    ## 6                     0                      0                1                0
    ## # ... with 37 more variables: Education.2n_Cycle <dbl>, Education.Basic <dbl>,
    ## #   Education.Graduation <dbl>, Education.Master <dbl>, Education.PhD <dbl>,
    ## #   Marital_Status.Absurd <dbl>, Marital_Status.Alone <dbl>,
    ## #   Marital_Status.Divorced <dbl>, Marital_Status.Married <dbl>,
    ## #   Marital_Status.Single <dbl>, Marital_Status.Together <dbl>,
    ## #   Marital_Status.Widow <dbl>, Marital_Status.YOLO <dbl>, Income <dbl>,
    ## #   Kidhome <dbl>, Teenhome <dbl>, Recency <dbl>, MntWines <dbl>, ...

**Data Partitioning**

Following codes split the entire dataset (2240 rows) into 80% (1793
rows) train dataset that will be used to build the model and 20% (447
rows) of test dataset to test the model built from the train dataset.

``` r
set.seed(123)

# split the dataset base on the responding variable of this section.

training.data <- dummy752$MntFishProducts %>% createDataPartition(p = 0.8, list = F)

# create training and test dataset

train.data <- dummy752[training.data,]
test.data <- dummy752[-training.data,]
```

**Model building with step-wise model selection**

There are too many independent variables (40 variables) in the dataset,
I will apply a step-wise model selection method that will incorporate
forward and backward procedure at the same time. Results show that
following 13 variables are significantly related (p-value &lt; 0.05) to
the responding variables. These variables will be used to build the
model.

``` r
# Building the model 
model752 <- lm(MntFishProducts ~., data = train.data)

# stepwise model selection that select models based on P-value (0.05)

ols_step_both_p(model = model752,
                pent = 0.05,
                prem = 0.05)
```

    ## 
    ##                                       Stepwise Selection Summary                                       
    ## ------------------------------------------------------------------------------------------------------
    ##                                   Added/                   Adj.                                           
    ## Step          Variable           Removed     R-Square    R-Square      C(p)         AIC         RMSE      
    ## ------------------------------------------------------------------------------------------------------
    ##    1          MntFruits          addition       0.367       0.367    600.8360    18631.5143    43.6225    
    ##    2      MntSweetProducts       addition       0.449       0.448    294.7480    18386.0503    40.7250    
    ##    3       MntMeatProducts       addition       0.488       0.487    148.9490    18256.0071    39.2637    
    ##    4        MntGoldProds         addition       0.506       0.505     81.8720    18192.7929    38.5669    
    ##    5     NumCatalogPurchases     addition       0.511       0.510     64.6800    18176.2443    38.3787    
    ##    6    Marital_Status.Absurd    addition       0.516       0.514     49.9680    18161.9356    38.2152    
    ##    7        Education.PhD        addition       0.519       0.517     40.5030    18152.6604    38.1059    
    ##    8      NumWebVisitsMonth      addition       0.522       0.519     32.1730    18144.4407    38.0081    
    ##    9          Teenhome           addition       0.524       0.521     25.6900    18138.0050    37.9294    
    ##   10      NumStorePurchases      addition       0.526       0.524     17.9260    18130.2447    37.8370    
    ##   11     Education.2n_Cycle      addition       0.528       0.525     14.1680    18126.4650    37.7866    
    ##   12         Country.ME          addition       0.529       0.526     12.0400    18124.3094    37.7535    
    ##   13          MntWines           addition       0.530       0.527      9.9610    18122.1937    37.7208    
    ## ------------------------------------------------------------------------------------------------------

Building the model using above variables.

``` r
model752_selected <- lm(MntFishProducts ~ MntFruits + MntSweetProducts + MntMeatProducts + NumCatalogPurchases + Marital_Status.Absurd + Education.PhD + NumWebVisitsMonth + Teenhome + NumStorePurchases + Education.2n_Cycle + Country.ME + MntWines, data = train.data)
```

**Model performance**

-   RMSE - the lower the RMSE, the better the model. The RMSE is 38.15
    which is higher than the median 12. It indicating a higher error
    rate.

``` r
predictions <- model752_selected %>% predict(test.data)

# RMSE

RMSE(predictions, test.data$MntFishProducts)
```

    ## [1] 38.15102

``` r
median(test.data$MntFishProducts)
```

    ## [1] 12

-   R2 has a moderate squared correlation of 0.497.

``` r
R2(predictions, test.data$MntFishProducts)
```

    ## [1] 0.4975092

**Summarise the model**

``` r
summary(model752_selected)
```

    ## 
    ## Call:
    ## lm(formula = MntFishProducts ~ MntFruits + MntSweetProducts + 
    ##     MntMeatProducts + NumCatalogPurchases + Marital_Status.Absurd + 
    ##     Education.PhD + NumWebVisitsMonth + Teenhome + NumStorePurchases + 
    ##     Education.2n_Cycle + Country.ME + MntWines, data = train.data)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -140.57  -12.63   -3.35    6.11  205.66 
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             8.473659   3.975505   2.131 0.033187 *  
    ## MntFruits               0.362973   0.030285  11.985  < 2e-16 ***
    ## MntSweetProducts        0.288567   0.029599   9.749  < 2e-16 ***
    ## MntMeatProducts         0.033231   0.006530   5.089 3.99e-07 ***
    ## NumCatalogPurchases     2.719104   0.508698   5.345 1.02e-07 ***
    ## Marital_Status.Absurd 119.807442  27.090835   4.422 1.03e-05 ***
    ## Education.PhD          -7.956403   2.253784  -3.530 0.000426 ***
    ## NumWebVisitsMonth      -1.010556   0.472208  -2.140 0.032485 *  
    ## Teenhome               -5.020162   1.788790  -2.806 0.005063 ** 
    ## NumStorePurchases       1.639473   0.398505   4.114 4.07e-05 ***
    ## Education.2n_Cycle      7.156059   3.288580   2.176 0.029684 *  
    ## Country.ME             59.926465  27.001135   2.219 0.026585 *  
    ## MntWines               -0.006110   0.004205  -1.453 0.146412    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 38.1 on 1780 degrees of freedom
    ## Multiple R-squared:  0.5204, Adjusted R-squared:  0.5172 
    ## F-statistic:   161 on 12 and 1780 DF,  p-value: < 2.2e-16

Base on the best model from the step-wise selection, variables that
significantly related to “MntFishProducts” (Amount spent on fish in the
last 2 years) in a **positive** way are:

``` r
model752_sum <- summary(model752_selected)

model752_sum$coefficients %>% 
  data.frame() %>%
  dplyr::select(Estimate, Pr...t..) %>% 
  rename("P_value" = Pr...t..) %>% 
  filter(Estimate > 0) %>% 
  arrange(P_value) %>% 
  kbl(align = "c") %>% 
  kable_styling(bootstrap_options = c("hover", "bordered")) 
```

<table class="table table-hover table-bordered" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:center;">
Estimate
</th>
<th style="text-align:center;">
P\_value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
MntFruits
</td>
<td style="text-align:center;">
0.3629726
</td>
<td style="text-align:center;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
MntSweetProducts
</td>
<td style="text-align:center;">
0.2885674
</td>
<td style="text-align:center;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
NumCatalogPurchases
</td>
<td style="text-align:center;">
2.7191037
</td>
<td style="text-align:center;">
0.0000001
</td>
</tr>
<tr>
<td style="text-align:left;">
MntMeatProducts
</td>
<td style="text-align:center;">
0.0332306
</td>
<td style="text-align:center;">
0.0000004
</td>
</tr>
<tr>
<td style="text-align:left;">
Marital\_Status.Absurd
</td>
<td style="text-align:center;">
119.8074418
</td>
<td style="text-align:center;">
0.0000103
</td>
</tr>
<tr>
<td style="text-align:left;">
NumStorePurchases
</td>
<td style="text-align:center;">
1.6394734
</td>
<td style="text-align:center;">
0.0000407
</td>
</tr>
<tr>
<td style="text-align:left;">
Country.ME
</td>
<td style="text-align:center;">
59.9264645
</td>
<td style="text-align:center;">
0.0265848
</td>
</tr>
<tr>
<td style="text-align:left;">
Education.2n\_Cycle
</td>
<td style="text-align:center;">
7.1560589
</td>
<td style="text-align:center;">
0.0296839
</td>
</tr>
<tr>
<td style="text-align:left;">
(Intercept)
</td>
<td style="text-align:center;">
8.4736590
</td>
<td style="text-align:center;">
0.0331873
</td>
</tr>
</tbody>
</table>

-   Insights:

    -   The amount spent on fish will increase with increasing amount
        spent on fruits, sweet, amd meat.

    -   The amount spent on fish will increase with increasing sales
        through catalog and store.

    -   Marital Status of absurd, country (ME) and Education of
        2n\_Cycle are also significant related the the amount that
        customers spent on fish.

Variables that significantly related to “MntFishProducts” (Amount spent
on fish in the last 2 years) in a **negative** way are:

``` r
model752_sum$coefficients %>% 
  data.frame() %>%
  dplyr::select(Estimate, Pr...t..) %>% 
  rename("P_value" = Pr...t..) %>% 
  filter(Estimate < 0) %>% 
  arrange(P_value) %>% 
  filter(P_value < 0.05) %>% 
  kbl(align = "c") %>% 
  kable_styling(bootstrap_options = c("hover", "bordered")) 
```

<table class="table table-hover table-bordered" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:center;">
Estimate
</th>
<th style="text-align:center;">
P\_value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Education.PhD
</td>
<td style="text-align:center;">
-7.956403
</td>
<td style="text-align:center;">
0.0004257
</td>
</tr>
<tr>
<td style="text-align:left;">
Teenhome
</td>
<td style="text-align:center;">
-5.020162
</td>
<td style="text-align:center;">
0.0050635
</td>
</tr>
<tr>
<td style="text-align:left;">
NumWebVisitsMonth
</td>
<td style="text-align:center;">
-1.010555
</td>
<td style="text-align:center;">
0.0324851
</td>
</tr>
</tbody>
</table>

-   Insights:

    -   Increase of customers with PhD background, number of teenagers
        at home, and number of web visiting month by customers
        negatively related with the amount spent on fish.

    -   The increase of any of these variables will lead to decrease in
        the amount spent on fish by customers.

### 7.6 Is there a significant relationship between geographical regional and success of a campaign?

Graph below shows that most campaigns across countries have low
acceptance rate and are mostly less than 15%. The country “ME” has only
3 customers, the sample size is too small to represent the acceptance
rate of the country. Other countries that have minimum of 100 customers.

**Visualisation**

``` r
# set up dataframe

df76 <- md2 %>% 
  dplyr::select(Country, AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, Response)

df76_viz <- df76 %>%
  rename("Camp1" = AcceptedCmp1,
         "Camp2" = AcceptedCmp2,
         "Camp3" = AcceptedCmp3,
         "Camp4" = AcceptedCmp4,
         "Camp5" = AcceptedCmp5,
         "LastCamp" = Response) %>% 
  pivot_longer(c(Camp1, Camp2, Camp3, Camp4, Camp5, LastCamp),
               names_to = "Cmp", 
               values_to = "result") %>% 
  mutate(Cmp = as.factor(Cmp)) %>% 
  group_by(Country, Cmp) %>% 
  summarise(count = n(), 
            rate = round(sum(result)/count*100, 1)) %>% 
  mutate(xlabel = paste0(Country, "\n", "(n =", count, ")"),
         barlabel = paste0(rate, "%"))
  
# plot

ggplot(df76_viz, aes(x = xlabel, y = rate, fill = Cmp)) +
  geom_hline(yintercept = 15, linetype = 2, colour = "grey") +
  geom_bar(stat = "identity", position = position_dodge(), colour = "black") +
  theme_bw() +
  theme(legend.position = c(0.1, 0.75),
        legend.background = element_rect(colour = "black"),
        plot.title = element_text(face = "bold", vjust = 2),
        axis.title.y = element_text(margin = margin(0, 8, 0, 0))) +
  scale_y_continuous(labels = function(x){paste0(x, "%")},
                     lim = c(0, 70)) +
  labs(title = "Figure 18. Acceptance Rate of Marketing Campaigns Across Countries",
       fill = "Campaign",
       y = "Acceptance Rate",
       x = "Country") 
```

![](marketing_files/figure-gfm/unnamed-chunk-73-1.png)<!-- -->

**Generalised Linear Models (GLM)**

Logistic regression is performed using GLM’s binomial family on the
effect of countries to 6 respective marketing campaign.

The results show that there is no significant relationship between
geographical regions and the success of a campaign, with a P-value of
all countries in all marketing campagins being higher than 0.05. It
indicates insufficient evidence to reject the null hypothesis that
geographical regionas has no relation to the success of marketing
campaign.

1.  Compare campaign 1 across countries.

-   Result: There is not enough evidence to reject the null hypothesis
    and I conclude that in campaign 1, there is no effect of country on
    campaign success. P value of all countries are higher than 0.05.

``` r
# Set up data frame

df76_2 <- df76 %>% 
  rename("Camp1" = AcceptedCmp1,
         "Camp2" = AcceptedCmp2,
         "Camp3" = AcceptedCmp3,
         "Camp4" = AcceptedCmp4,
         "Camp5" = AcceptedCmp5,
         "LastCamp" = Response) %>%
  mutate_if(is.double, as.factor)

# Use the binomial family of GLM to make the glm model carry out logistic regression 

model1 <- glm(Camp1 ~ Country, data = df76_2, family = "binomial")
summary(model1)
```

    ## 
    ## Call:
    ## glm(formula = Camp1 ~ Country, family = "binomial", data = df76_2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.3844  -0.3844  -0.3729  -0.3498   2.5017  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)  -3.08453    0.38651  -7.980 1.46e-15 ***
    ## CountryCA     0.45344    0.45711   0.992    0.321    
    ## CountryGER    0.30305    0.54873   0.552    0.581    
    ## CountryIND    0.08168    0.54712   0.149    0.881    
    ## CountryME   -11.48154  509.65227  -0.023    0.982    
    ## CountrySA     0.32136    0.45005   0.714    0.475    
    ## CountrySP     0.51662    0.40398   1.279    0.201    
    ## CountryUS     0.40547    0.54959   0.738    0.461    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1068.9  on 2239  degrees of freedom
    ## Residual deviance: 1065.4  on 2232  degrees of freedom
    ## AIC: 1081.4
    ## 
    ## Number of Fisher Scoring iterations: 13

2.  Compare campaign 2 across countries.

-   Result: There is not enough evidence to reject the null hypothesis
    and I conclude that in campaign 2, there is no effect of country on
    campaign success. P value of all countries are higher than 0.05.

``` r
model2 <- glm(Camp2 ~ Country, data = df76_2, family = "binomial") 
summary(model2)
```

    ## 
    ## Call:
    ## glm(formula = Camp2 ~ Country, family = "binomial", data = df76_2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.2128  -0.1716  -0.1716  -0.1545   2.9779  
    ## 
    ## Coefficients:
    ##               Estimate Std. Error z value Pr(>|z|)
    ## (Intercept) -1.957e+01  8.502e+02  -0.023    0.982
    ## CountryCA    1.579e+01  8.502e+02   0.019    0.985
    ## CountryGER   1.549e+01  8.502e+02   0.018    0.985
    ## CountryIND   1.528e+01  8.502e+02   0.018    0.986
    ## CountryME   -3.570e-09  6.267e+03   0.000    1.000
    ## CountrySA    1.514e+01  8.502e+02   0.018    0.986
    ## CountrySP    1.535e+01  8.502e+02   0.018    0.986
    ## CountryUS   -3.406e-09  1.336e+03   0.000    1.000
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 318.38  on 2239  degrees of freedom
    ## Residual deviance: 309.41  on 2232  degrees of freedom
    ## AIC: 325.41
    ## 
    ## Number of Fisher Scoring iterations: 18

3.  Compare campaign 3 across countries.

-   Result: There is not enough evidence to reject the null hypothesis
    and I conclude that in campaign 3, there is no effect of country on
    campaign success. P value of all countries are higher than 0.05.

``` r
model3 <- glm(Camp3 ~ Country, data = df76_2, family = "binomial") 
summary(model3)
```

    ## 
    ## Call:
    ## glm(formula = Camp3 ~ Country, family = "binomial", data = df76_2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.9005  -0.3971  -0.3971  -0.3587   2.3992  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)  -2.8201     0.3431  -8.219   <2e-16 ***
    ## CountryCA     0.1890     0.4211   0.449   0.6536    
    ## CountryGER    0.4222     0.4763   0.886   0.3754    
    ## CountryIND    0.4797     0.4495   1.067   0.2859    
    ## CountryME     2.1269     1.2719   1.672   0.0945 .  
    ## CountrySA     0.1088     0.4105   0.265   0.7909    
    ## CountrySP     0.3192     0.3616   0.883   0.3774    
    ## CountryUS     0.2844     0.5026   0.566   0.5715    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1168.1  on 2239  degrees of freedom
    ## Residual deviance: 1164.2  on 2232  degrees of freedom
    ## AIC: 1180.2
    ## 
    ## Number of Fisher Scoring iterations: 5

4.  Compare campaign 4 across countries.

-   Result: Apart from country “Ca”, there is not enough evidence to
    reject the null hypothesis and I conclude that in campaign 4, there
    is no effect of country on campaign success. P value of all
    countries are higher than 0.05.

-   Most countries have no relation to the success of marketing
    campaign. Only Canada has a week significant P value of 0.0478 that
    very close to 0.05 to reject the null hypothesis.

``` r
model4 <- glm(Camp4 ~ Country, data = df76_2, family = "binomial") 
summary(model4)
```

    ## 
    ## Call:
    ## glm(formula = Camp4 ~ Country, family = "binomial", data = df76_2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.4385  -0.4118  -0.4118  -0.3498   2.5626  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)  -3.2452     0.4161  -7.799 6.26e-15 ***
    ## CountryCA     0.9261     0.4679   1.979   0.0478 *  
    ## CountryGER    0.9517     0.5227   1.821   0.0686 .  
    ## CountryIND    0.7231     0.5209   1.388   0.1651    
    ## CountryME   -11.3209   509.6523  -0.022   0.9823    
    ## CountrySA     0.4820     0.4757   1.013   0.3109    
    ## CountrySP     0.8201     0.4306   1.905   0.0568 .  
    ## CountryUS     0.4022     0.5912   0.680   0.4963    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1188.4  on 2239  degrees of freedom
    ## Residual deviance: 1180.2  on 2232  degrees of freedom
    ## AIC: 1196.2
    ## 
    ## Number of Fisher Scoring iterations: 13

5.  Compare campaign 5 across countries.

-   Result: There is not enough evidence to reject the null hypothesis
    and I conclude that in campaign 5, there is no effect of country on
    campaign success. P value of all countries are higher than 0.05.

``` r
model5 <- glm(Camp5 ~ Country, data = df76_2, family = "binomial") 
summary(model5)
```

    ## 
    ## Call:
    ## glm(formula = Camp5 ~ Country, family = "binomial", data = df76_2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.4118  -0.4118  -0.4117  -0.3587   2.5320  
    ## 
    ## Coefficients:
    ##               Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept) -2.425e+00  2.894e-01  -8.382   <2e-16 ***
    ## CountryCA   -3.938e-02  3.680e-01  -0.107    0.915    
    ## CountryGER  -2.136e-01  4.665e-01  -0.458    0.647    
    ## CountryIND  -7.386e-01  5.074e-01  -1.456    0.145    
    ## CountryME   -1.214e+01  5.097e+02  -0.024    0.981    
    ## CountrySA   -2.857e-01  3.668e-01  -0.779    0.436    
    ## CountrySP    3.822e-04  3.098e-01   0.001    0.999    
    ## CountryUS   -6.095e-01  5.416e-01  -1.125    0.260    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1168.1  on 2239  degrees of freedom
    ## Residual deviance: 1161.6  on 2232  degrees of freedom
    ## AIC: 1177.6
    ## 
    ## Number of Fisher Scoring iterations: 13

6.  Compare the last marketing campaign across countries.

-   In the last Campaign, only the country “ME” is significantly
    different from other countries in term of relation to the acceptance
    rate, however the there are only 3 samples in this country to
    generate the statistical outcome, the sample size is too small, and
    the result can be inaccurate.

-   Result: In most country, there is not enough evidence to reject the
    null hypothesis and I conclude that in the last campaign, there is
    no effect of country on campaign success. P value of all countries
    are higher than 0.05.

``` r
modelLast <- glm(LastCamp ~ Country, data = df76_2, family = "binomial") 
summary(modelLast)
```

    ## 
    ## Call:
    ## glm(formula = LastCamp ~ Country, family = "binomial", data = df76_2)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.4823  -0.5920  -0.5789  -0.5040   2.2056  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept) -1.78449    0.22534  -7.919 2.39e-15 ***
    ## CountryCA   -0.01601    0.28538  -0.056   0.9553    
    ## CountryGER  -0.01703    0.34541  -0.049   0.9607    
    ## CountryIND  -0.55584    0.36751  -1.512   0.1304    
    ## CountryME    2.47763    1.24530   1.990   0.0466 *  
    ## CountrySA    0.08324    0.27114   0.307   0.7588    
    ## CountrySP    0.13168    0.23989   0.549   0.5830    
    ## CountryUS   -0.21491    0.37164  -0.578   0.5631    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1886.8  on 2239  degrees of freedom
    ## Residual deviance: 1875.4  on 2232  degrees of freedom
    ## AIC: 1891.4
    ## 
    ## Number of Fisher Scoring iterations: 4

## 8 CONCLUSION

Conclusion for exploratory data analysis (EDA):

-   Most customers are in mature age between 30 to 55.

-   51% of the customers are from Spain, which is the largest pool of
    customer.

-   50.3% of customers have education level of “graduation” level.

-   71.5% of customers have at least 1 children at home (being either 1
    kid or 1 teen in the family).

-   50% of customers have income falls approximately between $35k to
    $70k.

-   Wine is the best selling products of the company which contributing
    50.15% to the total revenue, followed by 27.56% of meat and then the
    7.27% of gold.

-   All 6 marketing campagins are not doing very well with acceptance
    rates of lower than 15%. The last marketing campaign was the most
    successful with acceptance rate 14.91%. The rest of all other
    campaigns have acceptance rate close to or below 7%.

-   In store sales is the most performing channels, followed by web, and
    then the last sale channel, catalog.

Conclusion for statistical analysis:

-   Number of in-store purchase has a significant positive relationship
    with the amount of wine, fruit, fish, and sweet sold, as well as
    deals, purchases made through web and the income of customers.
    Number of in-store purchase has a significant negative relationship
    with number of visits to company’s website by the customer, number
    of kid at home, sales through catelog and interestingly, the amount
    of meat sold.

-   Purchasing power of customers from the US do not significantly
    different from the rest of the world in terms of total purchase per
    customer, at a P-value of 0.4004. In term of total purchase, US
    ranked the second last country. However, purchasing power of US
    customers ranked the second in term of average purchase per customer
    (13.51).

-   People who spent an above average amount on gold in the last 2 years
    have more in store purchases, with a p-value of less than 0.05.

-   Married PhD candidates spent significantly less than other customer
    groups on fish, with a p-value of less than 0.05. Other factors that
    significantly related to amount spent on fish in a positive way are
    the amount spent on fruits, sweet, amd meat, numbers of purchases
    made through catalog and store, marital status of absurd, country
    (ME), and Education of 2n\_Cycle. Other factors that significantly
    related to amount spents on fish in a negative way are the number of
    PhD customers, number of teens at home, and number of web visits by
    the customers.

-   Logistic regression was carried out for 6 marketing campaigns and
    result shows that there is no significant relationship between
    geographical regional and success of a campaign.

## 9 LEGALITY

This is a personal project created and designed for skill demonstration
and non-commercial use only. All photos in this project, such as those
that applied as the thumbnail are only for demonstration, they are not
related to the dataset, the location where the data were collected, and
the results of this analysis.

## 10 REFERENCE

Australia Bureau of Statistics 2014, *Age Standard*, viewed 26 July
2021,
<https://www.abs.gov.au/statistics/standards/age-standard/latest-release>

Daoud J 2021, *EDA & Statistics Analysis with Marketing Data*, viewed 26
July 2021,
<https://www.kaggle.com/jackdaoud/eda-statistics-analysis-with-marketing-data>.

Crockett J 2021, *Marketing Analytics EDA task \[Final\]*, viewed 28
July 2021,
<https://www.kaggle.com/jennifercrockett/marketing-analytics-eda-task-final>

Minitab Blog Editor 2013, *Enough Is Enough! Handling Multicollinearity
in Regression Analysis*, viewed 26 July 2021,
<https://blog.minitab.com/en/understanding-statistics/handling-multicollinearity-in-regression-analysis>

The Pennsylvania State University 2018, *10.7 - Detecting
Multicollinearity Using Variance Inflation Factors*， viewed 27 July
2021, <https://online.stat.psu.edu/stat462/node/180/>

## 11 ACKNOWLEDGEMENT

-   Thank you Dr. Omar Romero-Hernandez for providing this dataset.
