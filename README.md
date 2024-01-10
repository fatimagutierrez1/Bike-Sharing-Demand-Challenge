# Bike-Sharing-Demand-Challenge
This repository is an attempt to join historical usage patterns with weather data to forecast bike rental demand in the Capital Bikeshare Program in Washington D.C https://www.kaggle.com/c/bike-sharing-demand/overview
## Overview
* As stated before, the task is to develop a predictive model that combines historical bike-sharing usage patterns with weather data to forecast the demand for bike rentals in the Capital Bikeshare program in Washington, D.C.
* The analysis is divided into two parts:
    * the initial exploration focuses on discovering patterns between variables
    * the second part delves into model building, dealing with basic regression to methods such as ridge/lasso regression, random forest and gradient boosting methods.
* The model that emerged the most effective was the random forest model, with an RMSLE value of 0.1040. For my submission, the RMSLE score obtained was 0.43499, and the top-performing model on Kaggle had a RMSLE score of 0.33756.
## Work done
* Data:
    * Input: train.csv file
         * datetime: hourly date + timestamp
         * holiday: if a day is considered a holiday  
         * season:  1 = spring, 2 = summer, 3 = fall, 4 = winter 
         * workingday:  the day is neither a weekend nor holiday
         * weather: 1: Clear, Few clouds, Partly cloudy, Partly cloudy, 2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist, 3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds, 4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog 
         * temp: in Celsius
         * atemp: "feels like" temp in Celsius
         * humidity: its humidity
         * windspeed: speed of wind
         * casual: number of non-registered user rentals initiated
         * registered: number of registered user rentals initiated
         * count: number of total rentals
  * Size: 1.12 MB
  * Hourly rental data are provided spanning two years. The training set is comprised of the first 19 days of each month, while the test set is from the 20th to the end of the month.
       * 6493 instances in test.csv
       * 10886 instances in train.csv
       * 6493 instances in submission.csv 
## Clean Up
1) Feature Engineering:
   * Added new features from the "datetime" column, being "date", "hour", "weekday", "month", and mapped "season" and "weather" to descriptive categories. Those variables were converted to the category data type

2) Data Visualization:
   * Plot matrix of the missing values by using msno.matrix to see the completness of the data
   * Subplots for box plots to visualize the distribution of the target variable "count" across different features
   * Box plots for "count" which are the total number of rentals alone, "count" across seasons, "count" across hours of the day, and "count" across working days

3) Outlier Removal:
   * Detected and removed outliers using the criteria that the absolute difference between "count" and its mean should be within three times the stand dev
   * Displayed the shapes of the data before and after outlier removal
   * The original dataset had a shape of (10886, 15), and after removing outliers, the shape became (10739, 15).
## Data Visualization
* Correlation Matrix
   1) Temperature/Humidity Correlation: "temp" has a positive correlation with the target variable "count" and humidity has a negative correlation.
        
   2) Windspeed: The correlation says that "count" and windspeed are not really related.
           
   3) Atemp/temp Multicollinearity:
            "atemp" is not considered since it has a strong correlation with "temp."
            "atemp" or "temp" should be dropped.
** Box Plots
   1)  Spring Season and Lower Count: Spring season has a relatively lower count and the dip in the median value in the box plot provides evidence for this observation.
   
   2)  Hour of the Day Boxplot: The boxplot analysis of the "Hour of the Day" has higher median values observed at 7 AM - 8 AM and 5 PM - 6 PM. This can be attributed to these peaks in regular school and office users during these times.
   
   3)  Outliers and Working Days: Most of the outlier points are contributed by "Working Day" rather than "Non-Working Day" and can be seen evidently in Figure 4.
## Problem Formulation
  * Input: Hourly rental data spanning two years, including features such as "datetime", "season", "holiday", "workingday", "weather", "temperature", "humidity", "windspeed", etc.
  * Output: Prediction of the total count of bikes rented during each hour covered by the test set.
 ** Models:
 1) Linear Regression:
  A simple model assuming a linear relationship between input features and bike rental counts
  Used as a baseline model due to its simplicity and interpretability
       * Loss: Mean Squared Error (MSE).
       * Optimizer: Ordinary Least Squares (OLS).

2) Ridge Regression and Lasso Regression:
   Regularized linear regression models are used to prevent overfitting by penalizing large coefficients
   Employed to handle potential multicollinearity and prevent overfitting
        * Loss: Mean Squared Error (MSE) with regularization term.
        * Optimizer: Gradient Descent.
3) Random Forest:
    Ensemble model combining multiple decision trees to capture complex relationships in the data
    Chosen for its ability to handle non-linear relationships and capture interactions between features
        * Loss: Mean Squared Logarithmic Error (RMSLE).
        * Optimizer: Not applicable (ensemble method).

## Training
  * Overfitting: Regularization to address overfitting.
  * Hyperparameter Tuning: Grid search was used.
  * Data Quality: Addressed issues like missing or inconsistent data through preprocessing.
** Key Performance Metric: Root Mean Squared Logarithmic Error (RMSLE)
## Conclusion
* In the context of bike-sharing demand prediction, the model that worked best was the random forest, with a RMSLE value of 0.104. The model's way to capture complex patterns in the data implies that it can effectively identify peak usage times when the demand for bikes is the highest. This is important to bike-sharing service providers to make sure they have enough bikes available during high-demand times.
## Future Work
* Explore additional combinations of features like incorporating external data sources, such as events happening in the area
## Citations
https://www.kaggle.com/c/bike-sharing-demand 
