# WillLivezeyCorrDSFinal
Data Science Fundamentals Final Project - Will Livezey-Corr

## Introduction

As it is more expensive to aqcuire new customers than it is to mantain old ones, managing customer churn is a necessity for businesses to stay afloat.

My goal was twofold:
Create the most accurate model for a bank that can accurately predict when a customer may leave the bank given the current number of years they have had an account.
Indicate factors of customers which increase the risk of churn.

Through the creation of a model that can predict whether a customer is likely to leave a bank, the bank can potentially attempt to develop policies targeting at risk inidividuals to entice them to stay. By determining which features correspond to higher churn rates, banks can also develop policies to target certain demographics.

## Necessary Imports

![image](https://user-images.githubusercontent.com/91287263/206081031-d5c6a12b-3f77-4c9b-a95c-df2931e04ba0.png)

Pandas is used for the storage of bank customer information within a dataframe. Numpy is necessary for pandas to work.
Matplotlib and Seaborn are used for making all of the various plots of my dataset. Plots will be used for determining which features have the greatest impact on churn, which variables may be correlated, contributing to collinearity and therefore overfitting of the model, determining the optimal number of neighbors for testing the KNN classifier model, and determining feature importance.

## Selection of Data

The data was downloaded from Kaggle. (Link: https://www.kaggle.com/datasets/santoshd3/bank-customers)

It contained information on 13 different characteristics of 10,000 different customers. There was no missing data. There was a large proportion of categorical data, including Gender, Country, Number of Bank Products Purchased (Which ranges from 1-4, and I treated as categorical due to its narrow range), Whether the customer had a credit card, Whether the customer was an active member, and Whether the customer had churned. There was also information on the Customer's surname, customer ID, age, estimated salary, account balance, credit score, and account tenure. There was also a column dedicated to the row ID of the data set.

![image](https://user-images.githubusercontent.com/91287263/206081502-2fe03e42-189d-4822-bfac-b87dfd4fceb3.png)

Upon importing the data, Row Index, Customer ID, and Surname were all removed, as none of these features will be relevant to churn prediction.

![image](https://user-images.githubusercontent.com/91287263/206081760-db903d1f-7026-4c3a-9372-30e162e6a109.png)

To gain initial impressions on the factors that might impact churn, several bar plots were made, taking each potential value for every categorical feature, calculating the % of customers with any given value who churned, and plotting it. It appears that whether or not a customer is from Germany has a significant impact on the churn rate of customers, and that females are more likely to churn than males.





