<h1> Rossmann  Sales Prediction </h1>

<h3> Sales Prediction with Machine Learning </h3>

![cover](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/cover_rossmann2.jpg)

<a> This repository contains the code for the Rossmann drugstore chain sales forecast.
The data used is available in [Kaggle](https://www.kaggle.com/c/rossmann-store-sales) and additional information was created to contextualize the problem. </a>

## 1. Business Problem

Rossmann is a pharmacy chain that operates more than 3,000 stores in 7 European countries. The stores will be renovated and the CFO needs to know how much he can invest in each one.

The development of a sales forecast model for the next 6 weeks was requested for each store.

The CFO would like to consult the forecast results directly from his smartphone or computer, and for this purpose it was agreed that a Telegram bot would send the forecast as soon as the store ID was consulted.

To solve the problem, the sales history of 1,115 stores was made available, corresponding to the period from 2015 to 2017. The dataset has the following features:

- **Id** - an Id that represents transaction
- **Store** - a unique Id for each store
- **Sales** - Sales volume on the day (target variable)
- **Customers** - the number of customers on a given day
- **Open** - Indicates whether the store is open (1) or closed (0)
- **StateHoliday** - indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None
- **SchoolHoliday** - indicates if the (Store, Date) was affected by the closure of public schools
- **StoreType** - differentiates between 4 different store models: a, b, c, d
- **Assortment** - describes an assortment level: a = basic, b = extra, c = extended
- **CompetitionDistance** - distance in meters to the nearest competitor store
- **CompetitionOpenSince[Month/Year]** - gives the approximate year and month of the time the nearest competitor was opened
- **Promo** - indicates whether a store is running a promo on that day
- **Promo2** - Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating
- **Promo2Since[Year/Week]** - describes the year and calendar week when the store started participating in Promo2
- **PromoInterval** - describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb, May, Aug, Nov" means each round starts in February, May, August, November of any given year for that store

## 2. Business Assumptions

The assumption about the business is as follow:

- The days when stores were closed were removed from the analysis.

- Only stores with sales values bigger than 0 were considered.

- For stores that did not have Competition Distance information, it was assumed that the distance would be 200000 meters (without competition nearby).



## 3. Solution Strategy

The project management method for Data Science chosen for the development of the solution was the Cross Industry Process - Data Science (CRISP-DS), which consists of a cyclical development method, based on very well defined steps. With each complete CRISP-DS cycle it will be possible to:

- Have an End-to-End version of the solution
- Speed in value creation
- Mapping of all possible problems in the development of the solution

![crisp_cycle](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/crisp_ds.png)


Therefore, the project will be carried out according to the following steps:

1. Data Description
2. Feature Engineering
3. Data Filtering
4. Exploratory Data Analysis
5. Data Preparation
6. Feature Selection
7. Machine Learning Modeling
8. Hyper Parameter Fine Tuning
9. Model-to-Business Interpretation
10. Model Deploy


## 4. Top 3 Data Insights

1. **Stores with closer competitors should sell less.**

*False*. Stores with closer competitors sold more, and distance from competitors does not seem to correlate with sales.


















