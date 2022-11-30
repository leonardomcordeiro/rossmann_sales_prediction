<h1> Rossmann  Sales Prediction </h1>

<h3> Sales Prediction with Machine Learning </h3>

![cover](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/cover_rossmann3.jpg)

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

**False.** Stores with closer competitors sold more, and distance from competitors does not seem to correlate with sales.

![competitors_distance](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/competitors_distance_insight.png)




2. **Stores should sell more after the 10th of each month.**

**False.** On average, stores sell less after the 10th day of each month.

![sales_over_time](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/sales_over_days.png)




3. **Stores with a larger assortment should sell more.**

**True.** Stores with a larger assortments sell more.

![sales_over_time](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/assortments_insight.png)




The other insights can be visualized in the notebook with exploratory data analysis - [EDA](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/notebooks/Rossmann_Etapa04_EDA.ipynb)



## 5. Machine Learning Models


The data were properly treated before data modeling, and the selection of features was done with the Boruta algorithm, more details you can find in the project notebooks.

Machine learning models used:

- Average Model (base line)
- Linear Regression
- Regularized Linear Regression
- Random Forest Regressor
- Xgboost Regressor


The results after cross-validation are:

| Model Name | MAE CV | MAPE CV | RMSE CV |
| --- | --- | --- | --- |
| Random Forest Regressor | 838.23 +/- 218.1 | 0.12 +/- 0.02 | 1257.07 +/- 318.2 |
| XGBoost Regressor | 1039.91 +/- 178.11 | 0.15 +/- 0.02 | 1487.57 +/- 239.4 |
| Linear Regression | 2081.73 +/- 295.63 | 0.3 +/- 0.02 | 2952.52 +/- 468.37 |
| Lasso | 2116.38 +/- 341.5 | 0.29 +/- 0.01 | 3057.75 +/- 504.26 |


###### MAE = mean absolute error;

###### MAPE = mean absolut percentage error;

###### RSME = root mean squared error.



After the fine tunning this is the final result:

| Model Name | MAE | MAPE | RMSE |
| --- | --- | --- | --- |
| XGBoost Regressor | 659.07 | 0.10 | 949.57 |



## 6. Error Interpretation

### Machine Learning Performance:

![residuals](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/residual_analysis.png)


### Business Performance:

![mape](https://github.com/leonardomcordeiro/rossmann_sales_prediction/blob/main/images/mape_by_store.png)


### Total Performance

| Scenario | Values |
| --- | --- |
| predictions | $ 286,124,621.76 |
| worst_scenario | $ 285,385,730.85 |
| best_scenario | $ 286,863,512.67 |


## 6. Deploy of Model
Having developed the model locally, it's time to make its predictions accessible to Rossmann's CFO, that is, to put it in a production environment. For this, the Flask framework and the Heroku cloud server were used. Below you can see the [Telegram bot](https://t.me/rossmannlc_bot) working.





https://user-images.githubusercontent.com/93056781/204028594-e7f19ae6-c294-4dfd-b8da-3c4673b4ae20.mp4



## 7. Conclusion

The project performed very well for the first CRISP cycle, an end-to-end solution was delivered capable of generating value to the business, and creating a data-driven environment, allowing the CFO to make more accurate decisions regarding the company's budget and cash flow. Rossmann.

## 8. Next Steps

• Evaluate the new demands of the business team
 
• Starting a new CRISP-DS cycle
 
• Evaluate new business hypotheses and generate new insights
 
• Create new features
 
• Improve selection of hyperparameters
 
• Test other Machine Learning models

• Add new information in Telegram bot

## Contacte me

[<img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />](https://www.linkedin.com/in/leonardo-mcordeiro/)
[![Yahoo!](https://img.shields.io/badge/Yahoo!-6001D2?style=for-the-badge&logo=Yahoo!&logoColor=white&link=mailto:leonardoaai@yahoo.com.br)](mailto:leonardoaai@yahoo.com.br)
[![Gmail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white&link=mailto:tdbinvestimentos@gmail.com)](mailto:tdbinvestimentos@gmail.com)



