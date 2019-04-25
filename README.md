# Ames Housing Data and Kaggle Challenge

### Problem Statement

Houses come in all shapes and sizes and with endless number of features (or lack of). As a realtor, how does one look at these features and characteristics and determine how they affect the price of any given house. In Ames, IA, a small town located in central Iowa, we would like to identify just that - what are the most important variables that go into real estate prices. This analysis will provide valuable insights for real estate companies in the area as well as to homeowners considering how to maximize the value of their home. Through the use of a linear regression model I will make predictions on houses given their unique characteristics.

### Data Collection

The Ames Housing dataset contains 82 variables and 2930 observations from the Ames Assessor’s Office used in computing assessed values for individual residential properties sold in Ames, IA from 2006 to 2010.


### Executive Summary

The initial inspection of the data quickly told me that this data was dirty and there were many columns that needed to be cleaned. I began the cleaning process by imputing all the nulls. The majority of nulls were easily fixed by replaced NaNs for a string of 'NA' where I confirmed in the data dictionary that the correct value was indeed 'NA'; however, the data was getting read in as a null. There were a few cases in which 'NA' was not the appropriate value to replace the null and if there was not a clear replacement value based on the available data, I dropped the row. To fill in the many missing values in the Lot Frontage column I built a linear regression using the values from Lot Area and Lot Shape to predict the missing values. Lastly, I turned any categorical column that was on a scale from Poor to Excellent into a numerical scale from 0 to 5 (where 0 = Doesn't Exist, 1 = Poor, and 5 = Excellent). Additionally, I dropped all rows of data where 'Gr Liv Area' > 4,000 and 'SalePrice' < 20,000 as these were causing my data to appear heteroskedastic and an unnormal distributed.

After cleaning the data, I moved on to exploratory data analysis and feature engineering. As expected, features such as 'Overall Quality' and 'Gr Liv Area' (Above Ground Living Area Square Feet) were highly correlated to the 'Sale Price'. Features such as the age of the home and 'Enclosed Porch' were negatively correlated. By plotting the average price of homes in various neighborhoods I decided to map the neighborhood names to a numerical value by dividing the 28 neighborhoods into seven categories. Upon looking at the data it is clear that there are many groupings of features, such as basements, garages, baths, quality, etc. I combined many of the numerical features in these categories to create one feature that represented them all. Additionally, I searched for any two variables that when multiplied together to create an interaction term yielded a high correlation to 'SalePrice'. I found that 'Total Quality' (a summation of all the quality features) and 'Above Ground SF' (1st Floor SF + 2nd Floor SF) when multiplied together have a 0.88 correlation with 'SalePrice

With the cleaned data and my new features, I began modeling. I first began with a linear model in which I used all the features available to me. With this model I achieved an R2 score of 0.93. I was happy with the score but hoped to improve it. Using the Lasso regression technique, I examined my features to see which were the most important. I picked the features I felt were most valuable to my model and put together a new linear regression model using limited variables. This model, while returning a lower R2 score (0.92 with power transformer), offers the ability for me to explain what is happening and which variables affect housing prices.

The features I determined most effect housing prices are:
- Interaction Term: Total Quality * Above Ground SF
- Finished Basement
- Bsmt Unf SF
- Neighborhood Quality
- Sale Type_New
- Year Remod/Add
- Garages
- Mas Vnr Area
- Lot Area
- Fireplaces

This model returns a lower R2 score (0.92 with power transformer) than the model I first created with many, many features. However, I decided to move forward with this model as it offered important inferences. Given a model with too many features, it is difficult to understand how each feature contributes to the model and ultimately alters the prediction. With my chosen model I have 10 features and by using the coefficients of my model I can see exactly how those features effect the model.

Through the repetitive process of data cleaning, feature engineering and modeling my data I was able to achieve a model with an R2 score of 0.92. While I believe my model has both a low bias and a low variance, I do not believe it is the best possible model. I was hoping for a better R2 score but changes only made small alterations. With more time I would like to do some additional data investigation and feature engineering. In looking back on the process, I would have spent more time digging deeper into each feature - both in the data and outside the data  - to understand what it represented and how I could best use it to my advantage.

### Data Dictionary: Original Features

see: http://jse.amstat.org/v19n3/decock/DataDocumentation.txt

### Data Dictionary: Newly Engineered Features
|Feature|Type|Description|
|---|---|---|
|Total Quality|int|Overall Quality + Exterior Quality + Basement Quality + Kitchen Quality|
|Above Ground SF|float|1st Floor SF + 2nd Floor SF|
|Neighborhood Quality|int|1-7 (low-high) scale of neighborhood quality by median house price|
|Baths|float|1.05xFull Bath + 0.5xHalf Bath + 0.65xBsmt Full Bath + 0.20xBsmt Half Bath|
|Home Age|int|2010 - Year Built|
|Finished Basement|float|BsmtFin Type 1 (scale 0-5) * BsmtFin SF 1 + BsmtFin Type 2 (scale 0-5) * BsmtFin SF 2|
|Outdoor SF|float|Open Porch SF + Wood Deck SF|
