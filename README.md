
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
- Easy to implement.
- Works well with samll dataset.

Disadvantages:
- Change in original variance.
- This method adds bias and variance.
- Only works for numeric data.

3. Most Frequent Imputation

This approach is used for filling missing values in categorical columns. Its quite simple actually, just replace the missing values by the most frequent value in a column. This approach has the same advantages and disadvantages as the Mean / Median imputation. 

TODO: Photo 2

According to the above count plot, any missing values in Embarked column can be replaced by 'S' category. 

4. Unknown Value Imputation

In this approach we fill the missing value with an unique category, lets suppose 'U' for unknown. This approach works well in limited cases. Let's suppose you are collecting data from different victims aboard the titanic when it sank, you want to analyse the data to if there was any particular reason as to why the passenger survived. There is a column in your dataset which tells you the location of the passenger on the ship when the iceberg hit. Unfortunately, you cannot collect this data for all the passengers that didnt survive the incident. In this case making a unique category might be usefull to develop insights in the data. Maybe the passengers in location 'U' had a very less chance of survival. 

In other cases, after we perform one-hot encoding we will have a new feature in our dataset, which might result in decreased accuracy of our data. This is the case when data is missing in the dataset because of completely random reasons.

TODO: Photo 4

In the above photo you can see that the Cabin column has many values and also nan. From initial analysis we know that Cabin column has 687 missing values. 

TODO: Photo 5
We perform the Unknown Value Imputation for this column. 

TODO: Photo 3

After replacing known values with 'K' and unknown values with 'U' we can see that more people that didnt survive have unknown cabin types.

5. Prediction of Missing Values

Note: In case of regression make sure there is no multicolinearity, check for VIF and Tolerance before continuing with this approach.

In this approach we predict the missing values. This approach is explained in following steps:

a) X Training data = all the columns except the independent variable (dont want data leakage) having rows with nan
b) y Training data = the column whose missing values you want to predict, having only rows without nan
c) X Prediction data = the column whose missing values you want to predict, having only rows with nan
d) train the model on X_train and y_train
e) make predictions on X_pred
f) replace all the rows with nan in original dataset with step e (just for the column whose missing values you are imputing)

The code for this approach can be seen here: 

TODO: Code

This is the kde plot of an Age column on both original data and data after we have replaced missing values with predictions.

TODO: Photo 6

6. Using Algorithms Robust to Missing Values

There are many algorithms that can handle missing values on there own, some of them like RandomForest and K Nearest Neighbours are commonly known, and CatBoost is not very commonly known. I recommend going through the documentation of CatBoost once: https://catboost.ai/. 

7. Miscellaneous ways

- Datawig library
This is the documentation for <a href="https://github.com/awslabs/datawig">DataWig</a>, a framework for learning models to impute missing values in tables.

- Last Observation Carried Forward (LOCF)
In this method the last known value is carried to the missing value and can be implemented easily using pandas.

data.fillna(method='ffill')

other methods availabe are: 'backfill', 'bfill', 'pad', 'ffill'

pad / ffill: propagate last valid observation forward to next valid and backfill / bfill: use next valid observation to fill gap.

- Interpolation
Interpolation is a mathematical method that adjusts a function to your data and uses this function to extrapolate the missing data. The most simple type of interpolation is the linear interpolation, that makes a mean between the values before the missing data and the value after.

TODO: Photo 7

## Conclusion

