# Small-Logisic-Regression-SUV-data
Good starting point showing the breakdown of logistic regression on a small dataset to predict SUV purchase data.
This is an extension of the SUV data logistic regression analysis listed [here](https://medium.com/analytics-vidhya/suv-purchase-prediction-using-logistic-regression-ca79bae6f3d5).
What you will see in this rendition is an implementation of a larger confussion matrix, indexing of columns, adding new columns, and an explination regarding __why we might want 
explore the splitting of the data based on a larger confusion matrix__. This also explores the use of the multilabel confussion matrix that is part of the sklearn package. Finally, this separates the purchasing data into Male and Female purchases and demonstrates the methods you would use to explore how other models migth fare for the less-accurately predicted male data. 

[Confusion Matrix Basic Logistic Regression](https://github.com/AxisMeetsWorld/Small-Logisic-Regression-SUV-data/blob/main/SUV_Confusion_Orig.png)

## More details and building blocks
  The first thing that needs to be performed differently to accomplish this is to enumerate the gender column and in this instance, *likely due to alphabetical order*, you will see male purchasers identified by a "1", and female by a "0". Here are the first 10 colyumns of the modified set:
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
