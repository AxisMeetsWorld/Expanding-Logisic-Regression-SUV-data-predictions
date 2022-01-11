# Improve on Logistic Regression Prediction Data (SUV Purchases)
Good starting point showing the breakdown of logistic regression on a small dataset to predict SUV purchase data.
This is an extension of the SUV data logistic regression analysis listed [here](https://medium.com/analytics-vidhya/suv-purchase-prediction-using-logistic-regression-ca79bae6f3d5). *Note this was a rather small dataset so it is difficult to find too much to implement but this process would be useful for larger datasets.*
What you will see in this rendition is an implementation of a larger confussion matrix, indexing of columns, adding new columns, and an explination regarding __why we might want 
explore the splitting of the data based on a larger confusion matrix__. This also explores the use of the multilabel confussion matrix that is part of the sklearn package. Finally, this separates the purchasing data into Male and Female purchases and demonstrates the methods you would use to explore how other models migth fare for the less-accurately predicted male data. If you were to run the logistic regression after scaling the data, this is the basic breakdown you will see of true positives, false positives, false negatives and ture negatives:

![Confusion Matrix Basic Logistic Regression](https://github.com/AxisMeetsWorld/Small-Logisic-Regression-SUV-data/blob/main/SUV_Confusion_Orig.png)

## More details and building blocks
  The first thing that needs to be performed differently to accomplish a deeper dive into the data is to enumerate the gender column and in this instance, *likely due to alphabetical order*, you will see male purchasers identified by a "1", and female by a "0". Here are the first 10 colyumns of the modified set:
  |User ID|Gender_int|Age|EstimatedSalary|Purchased|
|---|---|---|---|---|
|15624510|1|19|19000|0|
|15810944|1|35|20000|0|
|15668575|0|26|43000|0|
|15603246|0|27|57000|0|
|15804002|1|19|76000|0|
|15728773|1|27|58000|0|
|15598044|0|27|84000|0|
|15694829|0|32|150000|1|
|15600575|1|25|33000|0|
|15727311|0|35|65000|0|

Then, with the help of setting up an array of conditions and using the "logical_and" as well as the numpy "select" function we can create the new column categorizing male, female, purchased, and non-purchased data:
  
|User ID|Gender_int|Age|EstimatedSalary|Purchased|Gender_purchase_even = Purchased|
|---|---|---|---|---|---|
|15624510|1|19|19000|0|1|
|15810944|1|35|20000|0|1|
|15668575|0|26|43000|0|3|
|15603246|0|27|57000|0|3|
|15804002|1|19|76000|0|1|
|15728773|1|27|58000|0|1|
|15598044|0|27|84000|0|3|
|15694829|0|32|150000|1|2|
|15600575|1|25|33000|0|1|
|15727311|0|35|65000|0|3|  

## Setting Up a More Granular Matrix:
  The next hurdle is to rerun the testing and training data with regard to the newly added column. In this example this column was assigned a variable (Z) when the original confusion matrix was created. Simply run the LogisticRegression() model with this new data as your target column, rename the columns and rows with the .columns(), and .index() properties of your new dataframe, and apply labels that describe whether it was a man, woman, and whether they purchased or not to those properties. In this example, in order to see how all of the numbers break down percentagewise, use the dataframe.sum() method, and re-writing the values of the dataframe as the ratio of each cross-calculated value over the sum (DF = DF.astype('float')/DF.sum()). Here you can see the confusion matrix:
  ![Male and Female Prediction Results](https://github.com/AxisMeetsWorld/Small-Logisic-Regression-SUV-data/blob/main/SUV_Granular_Matrix.png)
  
If you want to see a little breakdown of the numbers for each category, you can create a small bar chart. Simply be careful to label correctly as you will see the values are presorted based on which category is present the most. 
![Barchart Breakdown of Male and Female Predictions](https://github.com/AxisMeetsWorld/Small-Logisic-Regression-SUV-data/blob/main/Purchase_Breakdown_Barchart.png)

From the expanded confusion matrix, it should be pretty clear that the models are better at predicting Female purchasers (just over 1% error for female data, but over 7% of the error is attributed to male data), than Male purchasers, so it is worth exploring if we could improve the Male data only. In case you want to see the counts, you can see the breakdowns here by constructing a title for each category, constructing selected values of that 4 category column, and constructing 2X2 confusion matricies from there. You can see these counts here: ![Counts by category](https://github.com/AxisMeetsWorld/Small-Logisic-Regression-SUV-data/blob/main/Actual%20Counts%20by%20category.png)

## Process to improve with other models; what you would do if you have enough data.

This next step is to set up a list of classification models with 2 columns; one with the models and the other with the arguments for each model. Another task is to create a function that utilizes the "eval()" function to concatenate the models in your list, with the arguments, then fit and transform those models to come up with prediction data for each model. Have the function return the accuracy percentages. Then, create a new list, and a for loop that will run through the initial list using the function created and capture the accuracy results. For this process, I tried the Random Forest Classifier, Naive Bayes, Support Vector Machines (linear and polynomial), and Linear Regression. Here is a chart of the accuracy results, and there were minor improvements for all models with the exception of Gaussian Naive Bayes:
![Model Accuracy](https://github.com/AxisMeetsWorld/Small-Logisic-Regression-SUV-data/blob/main/Male%20model%20prediction%20accuracy.png)

**This methodology will allow you to try different models, and split your accuracy results to see what data might benefit from a different model.**
