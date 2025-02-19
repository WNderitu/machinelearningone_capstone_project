# Predicting churn risk for PowerCO
---
## Introduction
The purpose of the project is to advise PowerCo on how to retain their customers. PowerCo is a Major gas & electricity utility company that supplies to small & medium sized enterprises. Powerco has consulted BCG X, a consulting company to advise them on how to retain their customers. 

This is a capstone project for a Supervised Machine learning module done for a data science course. 

### Methods Used
- Descriptive statistics
- Bivariate and multivariate statistics
- Data visualization
- Machine learning

### Technologies
 - Python
 - Pandas
 - Seaborn
 - Matplotlib
 - Jupyter
 - Scikit learn

---
## Project Description
The project will entail conduct of the following:
1. Determination of the business problem
2. Generation of a hypothesis
3. Importation of the datasets
4. Conduct of exploratory data analysis using different statistical techniques and visualization of the data
5. Conduct data pre-processing & feature engineering
6. Development and evaluation of a predictive model using random forest classification model
7. Generation of insights, recommendations and the next steps. 

## Business Problem
There has been a lot of change in the energy market in recent years, with increasing availability of more energy options than ever for customers to choose from. PowerCo is concerned about their customers leaving for better offers from other energy providers, which is now a big problem. Therefore the need to determine reasons for customers churning. 

BCG has hypothesised that churn is driven by customers’ sensitivity to price. 

## Dataset
The dataset is derived from a data science job simulation exercise provided by BCG X on the forage website https://www.theforage.com/simulations/bcg/data-science-ccdz. The job simulation involves using using data to advise the client, PowerCo on how to retain their customers together with the team at BCG X.

The datasets used are saved in this repository. 

## Exploratory Data Analysis
The data was analysed using pandas. Descriptive statistics was used to summarise the numerical variables. Seaborn and matplotlib were used for data visualization. Stacked bar plots were used to visualize churn rate and churn per variable. Distribution plots were used to describe distribution of the data for the numerical variables. 

## Machine Learning Based Exploratory analysis
Boxplots were used to check for outliers in the numerical variables. KDE plots was used to check for a linear decison boundary between the churn and retailed labels for the numerical variables.  A correlation matrix for the numerical features was computed to check for multicollinearity.  Frequency tables were generated to determine the number and proportion of unique values for the categorical features. 

## Data Pre-processing and Feature engineering
The dataset provided for feature engineering by BCG had 18 features added which were on yearly and 6 monthly variation in off peak price variance, peak price variance, mid peak price variance, off peak fixed price variance, peak fixed price variance, mid peak fixed price variance and yearly and 6 monthly variation in prices for off peak, mid peak and peak times. Preprocessing included conversion of the date columns to datetime dtype in the cleaned_data_after_eda and price_data  datasets.

Feature engineering included computation and creation of features that show changes in off peak prices between December and January of the preceding year, differences between prices for off peak, mid peak and peak periods for each company/customer, differences in average prices per period per company per price date using the price dataset and then merging with the cleaned dataset. Another new feature added was tenure for how long a company has been a client for the power company. Columns containing data on dates were converted to months, to create new features as datetime is not used in classification models. The date columns were then dropped from the mereged dataframe. 

Features with a high correlation of more than 0.99 were dropped from the dataframe. Values for categorical variables/features were changed to boolean values. Two nominal categorical variables were encoded using one hot encoding. Numerical columns with skewed data were transformed using log transformation. The target variable had class immbalance which was handled using SMOTE. 

Additional feature engineering was done after developing a base model which included deletion of unnecessary features after generation of feature importance and robust scaling of features with outliers. 

## Insights

The churn rate was high, 9.7% of customers churned in the next 3 months.

<img width="443" alt="image" src="https://github.com/user-attachments/assets/c78dda0f-05cb-445a-84fb-b31b118cacdc" />


Customers with 1 active product & services had the highest churn rate. Customers with > 2 active products & services did not churn

<img width="416" alt="image" src="https://github.com/user-attachments/assets/807fc0c7-87d0-414f-a2f9-6e7520237598" />


Customers with 4 years of antiquity had the highest churn rate. Customers with 8 - 12 years of antiquity did not churn. Customers with no gas service churned more than the ones with electricity & gas. 

<img width="612" alt="image" src="https://github.com/user-attachments/assets/5a816ff2-bed4-430a-8bb0-5a135f4cd7bb" />


Churning customers distributed over 5 different categories of channel_sales

<img width="612" alt="image" src="https://github.com/user-attachments/assets/bc1c9837-41ca-46ac-a15d-bdf1434fc9f7" />


Churning customers distributed over 4 different categories of code of electricity campaign of first subscription

<img width="612" alt="image" src="https://github.com/user-attachments/assets/5eb910cd-b420-4bd5-b915-0e0ba9b37e8a" />


The largest proportion of customers that have churned had lower consumptions. With increase in consumption, there was decrease in churning. At high consumption, there was no churning

<img width="720" alt="image" src="https://github.com/user-attachments/assets/43df5d90-7ba0-4a72-bc05-64dc9363b20a" />


At low values of subscribed power, there was the highest proportion of churned customers

<img width="756" alt="image" src="https://github.com/user-attachments/assets/fae957fc-1482-4bee-8c29-1bda9e22aa98" />

## Machine learning Modelling
A random forest classifier was used to develop a model to predict customer churn. Evaluation metrics used were accuracy, precision, recall, f1-score and average precision score. A confusion matrix and correlation report were also generated. A base random forest classifier model was created with default paramteres. Feature importance was determined for the base model and unnecessary features dropped. 

### Model tuning
Hyperparameter tuning was done using RandomizedSearchCV. Probability thresholds were optimised through threshold tuning. 

The best parameters for the random forest classifer model were;
 - n_estimators: 300
 - min_samples_split: 5
 - min_samples_leaf: 1
 - max_features': sqrt
 - max_depth: None
 - criterion: entropy

The best threshold was: 0.5061

The model evaluation metrics for the final random forest classifer model were;
- Accuracy: 0.9510
- Precision: 0.9774
- Recall: 0.9241
- F1-Score: 0.9500
- PR-AUC: 0.9873

Confusion matrix for the final model:

![image](https://github.com/user-attachments/assets/9a5a5311-e02d-4fd6-8dfe-0d81467303f9)

The model can predict churn, however churn is not driven by customers’ sensitivity to prices. 

Recommendations
- Check the past 12 months consumption, gross margins on power subscription, subscribed power & forecast meter rentals for the next 12 months for the following:
  - 5 sales channels that had customers who churned in the next 3 months
  - 4 codes of the electricity campaign that companies first subscribed to that had customers who churned in the next 3 months

Next Steps
- Explore other supervised classification models on the dataset

## Export model

Final model saved using pickle. 

## Folder structure
The folder contains the following files:
1. 1.0-powerco_eda notebook
2. 2.0-powerco_feature engineering&model notebook
3. Data description
4. Prediciting churn risk project presentation
5. clean_data_after_eda csv file - data used for feature engineering
6. client_data csv file - data used for exploratory data analysis
7. price_data csv file - data used for exploratory data analysis & feature engineering
   
## Acknowledgements & Attributions
1. https://www.theforage.com/simulations/bcg/data-science-ccdz
![image](https://github.com/user-attachments/assets/78d352c2-9af1-47e0-8ded-dd3cbf33590d)

