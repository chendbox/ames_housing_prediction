# Project 2 - Ames Housing Data and Kaggle Challenge

# Problem Statement
Ames housing data is very specific. We will use the data provided by Kaggle to conduct feature engineering and train a model to predict the house sale price. We will validate few models and narrow to the best prediction model. We also make recommendation to Ames homeowners how to invest and maintain their housing properties values.

# Summary
Contents:
 - background
 - train.csv & test.csv Data cleaning
 - feature engineering
 - model validation and prediction
 - recommendation

# Background
The primary learning objective is to create and refine your regression model.
The Kaggle challenge website [Kaggle](https://www.kaggle.com) provides two data sets: train.csv, which is used for training a model. The test.csv file is used for predicting housing price based on the model from train file. I will create a machine learning model and use it to prodict the sale price. Kaggle also provides data_description.txt, which help us to understand the features columns and sample_submission.csv, which is the format that my prediciton data should be orgainized.

# train.csv & test.csv
train data sets, 2051 rows and 81 columns (79 features to describe the detailed aspects of ames house). since not all of the features is rational as predictor to sale price, we will have to refine the columns later.
test data sets with 878 rows and 80 columns, have the exact same feature columns as train, except for price, which we need to predict and submission the prediction.

# Review the [data description](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).


# Data Cleaning
 1. check the missing values first and check the column features, int, float, str...
 2. if the column is categorical, fill in 'NONE', if the column is numeric, fill in '0'
 3. there are few columns with fewer missing values, fill with the column values mean
 4. Observe the columns, drop 'Pool QC', 'Misc Feature', 'Alley', 'Fence', 'Fireplace Qu' obvisouly wont' signiicantly impact the price
 5. Match 'Garage Yr Blt' column with same year bilt and mark as int
 6. I will also create a column 'HouseAge' to indicate the hosue age, which possible a strong predictor
 
# EDA and feature engineering
 1. The 'SalePrice' distribution is right scewed and transform into log to minimize the large range effect
 2. Plot the 'SalePrice' and modify to normal distribution by remove few outliers
 3. Differentiate the categorical and numeric features
 3. Dealing with categorical: I need to check if each categorical feature is related with Saleprice, so I define a function FP_plot that can run through all the columns and plot with 'Saleprice' to understand the features. 
 4. Define a function anova to conduct ANOVA analysis on catgorical features and remove the non significant features: landslope, this step is very effective and lead to good rsme score
 5. Dealing with numeric: conduct the correlation and remove columns less than 0.15 ( very weak correlation)
 6. Final clean: remove ID PID, combine numeric columns to make new columns which possiblly own the same features to correlate with SalePrice
 7. I will dummify the categorical columns of train data into numerical columns to set up model.
 8. Processing the test data with the exact same steps. 
 
# modeling and validations
 1. Before split data, train and test data set should have same columns. Remove the missing features that is not at both sets.
 2. Split training and testing data with 75:25 ratio and set up random state 42 for repeatness
 3. Feature scaling will minimize and normalize features with relatively same weight. Apply standardscaler to transform all the train sets
 4. set up modeling: linear regression, ridge regression, lasso regression, and elasticnet regression
 5. conduct CV to optimize the hyperparameters to get the best fit model
 6. Compare the scores from each model and LINE assumptions
 
R2 Score in Each Model
train\n
test

linear regression train score: 0.9399908466933058,  test score 0.8989640682616913

Ridge regression train score:  0.9346789503876216,  test score 0.9023453814813689

lasso regression train score:  0.9399908466765434,  test score 0.8989641638195849

ElasticNet regression train score: 0.8451523632391718, test score 0.8237486833999439

Random Forest regression train score: 0.9846959076478049, test score 0.878616832655227

XGBoost regression train score: 0.9233090353962546, test score 0.871349257274084

 
 # prediction and recommendation
 7. Use ridge regression to predict the test price and analyze the residuals , RSME, R2 and explain the coefficients
 8. Create new kaggle submission by adding id and sale price columns with values.
 9. check the strength of each features correlated with saleprice to make assumptions and recommendation in buisness terms

RIDGE RMSE:  18179.71

# Conclusion and Recommendations
I reviewed the top 20 most influenctive features to make recommendation to home owner or investment agency where to increase the housing vlaue. Neighborhood is definitely predictor to influence the saleprice. Invest in good neighborhood such as crawfor, northridge, rather than bad neighborhood. Funcitonal Type strongly related indicates the midwest people prefer a life life with typical fucntion sections. Be sure you improve the functionallity to get a good price. Kitchen quality is also good predictor, but some may negatively predictor, such as fair ktichen which in Iowa the lowest kitchen condition, indirectly associate with the housing condition. (but i didnot analyze the interaction in this analysis). Some buiding type are also negative predictor, such as townhouse, duplex. Improve the building type and invest other buidling type such as single family. Sell or refinance house payment type in ome just constructed and sold can increase the house value.
Improve the overall quality as well. 
