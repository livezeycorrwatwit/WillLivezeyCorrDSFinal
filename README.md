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

![image](https://user-images.githubusercontent.com/91287263/206082233-9b7f2b39-e1b4-4d5e-91e0-9e18d5b555e7.png)

It appears there is a slight decrease in overall churn rates as tenure increases. Customers who purchase only 1 or 2 products from the bank are much less likely to churn than those who purchased 3-4 products.

![image](https://user-images.githubusercontent.com/91287263/206082473-c57df201-4633-4c33-9e3d-807c2b5519ea.png)

While having a credit card had no discernible impact on churn, customers who were not active members were more likely to churn. (0=No, 1=Yes)

![image](https://user-images.githubusercontent.com/91287263/206083260-d77cc2de-24d5-4239-b5c6-24c18d7df2f9.png)

To check for multicollinearity of continuous variables, a pairplot was made. However, instead of finding multicollinearty, it appeared as though there may be an association between having no money in an account and churn. To check, a bar char was made.

![image](https://user-images.githubusercontent.com/91287263/206083479-0cc457de-c33a-4568-9352-5c27c0b70964.png)

It seems as though people were more likely to churn given they had any money at all in their bank account. As there does not appear to be a significant relationship between churn and balance for those who do have money in their accounts, Balance will instead become a categorical variable, denoting only whether or not a particular customer has any balance at all.

After removing all data points with no balance, multicollinearty was checked for again:

![image](https://user-images.githubusercontent.com/91287263/206083902-bdfa9b28-c2f8-4233-b8b1-9cafc0633913.png)

While no multicollinearity was found, it was observed that age seems to impact churn, with older customers being more likely to churn.

![image](https://user-images.githubusercontent.com/91287263/206084752-d4d0479f-04be-4651-912d-b666770eea25.png)

At long last, feature selection. Columns unrelated to churn (Credit score, Having a Credit Card, Estimated Salary) are removed. The columns Gender and Geography are encoded in terms of 0 and 1, as the classification algorithms we will be using cannot interpret non numerical data. Ultimately, we end up with a column "Female" (0 if not female, 1 otherwise) and "IsGermany" (0 if not Germany, 1 otherwise). As Spain and France were similar in their impact on churn, all that matters for analysis is whether a customer is from Germany. All other factors remain the same, if they were not dropped. Some columns were renamed for clarity.

## Methods

With our data finally selected and tweaked, it is time to see if an accurate model predicting churn per each tenure year can be made. As a customer can either churn or not, we can use classification algorithms to predict churn based on our factors impacting it. The models in use included the RandomForest, LogisticRegression, NaiveBayers, and DecisionTree classifiers.

![image](https://user-images.githubusercontent.com/91287263/206086041-c444ec8f-ba65-4a56-aca2-528fcfeded57.png)

Running each test on different training/test data splits 40 times per tenure and averaging the results gave a good indication of the accuracy of each model. However, I also wanted to run the KNN classifier algorithm, which requires more steps to determine an optimal number of nearby neighbors to use for classification.

![image](https://user-images.githubusercontent.com/91287263/206086402-0b30be3c-bf74-4a6b-8c3d-9787c298dd87.png)

![image](https://user-images.githubusercontent.com/91287263/206087010-88e09791-56af-4614-a8bd-4fccfebbc8d5.png)

Plotting the maximum attained average accuracy per neighbor paramter revealed an optimal neighbor count of 17

![image](https://user-images.githubusercontent.com/91287263/206087164-be9b07d4-d6d6-4908-84e4-936b85095a31.png)

After acquiring a potential optimal neighbor count, using the same trial methodology for the other types of classification algorithms gave the KNN model an accuracy prediction. The final results are below.

## Results












