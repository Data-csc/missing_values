
# Handing Missing Values

## This repository will be used to discuss various methods to handle missing values

There are two type of columns which will have missing values: 
1. Categorical Columns
2. Continuous Columns

We will handle these columns seperately.

Ways to handle missing values are:

1. Drop the Column or Row

data.dropna(axis=1, inplace=True) #drop columns
data.dropna(axis=0, inplace=True) #drop row


ahh!! the simplicity in this approach, I mean you gotta love it!! Life would have been soo simple if we could have used this approach for all datasets. This approach leads to an accurate and robust model, this is because we have no used any imputation techniques to 'guess' the missing value. I would not recommend using this approach in your projects as they result in loss of 'valuable' data, few situtations where you can even think about using this approach are described below: 

a. When you have a column or a row with no relevant information.
b. When you have billions of rows and deleting 10 rows wont make much of a difference.
c. When you have a column with large proportion of data missing.

2. Mean / Median Imputation

This method is very easy to compute and is widely used to replace missing values in dataset. This method is best used when data is Missing Completely at Random (MCAR), i.e. there  exist equal probability of any observation to be missing. Median imputation is robust to outliers, however mean imputation is not. You can see in the following image the difference in kde plots when we replace the missing value with mean or median. 

TODO: Graph -1 

Advantages: 
1. Easy to implement.
2. Works well with samll dataset.

Disadvantages:
1. Change in original variance.
2. This method adds bias and variance.
3. Only works for numeric data.

3. Most Frequent Imputation

This approach is used for filling missing values in categorical columns. Its quite simple actually, just replace the missing values by the most frequent value in a column. This approach has the same advantages and disadvantages as the Mean / Median imputation. 

TODO: Photo 2

According to the above count plot, any missing values in Embarked column can be replaced by 'S' category. 

4. Unknown Value Imputation

In this approach we fill the missing value with an unique category, lets suppose 'U' for unknown. This approach works well in limited cases. Let's suppose you are collecting data from different victims aboard the titanic when it sank, you want to analyse the data to if there was any particular reason as to why the passenger survived. There is a column in your dataset which tells you the location of the passenger on the ship when the iceberg hit. Unfortunately, you cannot collect this data for all the passengers that didnt survive the incident. In this case making a unique category might be usefull to develop insights in the data. Maybe the passengers in location 'U' had very less chance of survival. 

In other cases, after we perform o

