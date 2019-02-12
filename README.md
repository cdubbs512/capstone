# Christopher Williams Capstone

# TITLE: Predicting Footballers Market Values

# README and Executive Summary


 

### Christopher Williams

### General Assembly DSI 2018
### February 12, 2018



## Contents of Capstone (folder)

README and Executive Summary

Jupyter Workbooks
- Part 1: Data Collection 
- Part 2: Data Cleaning Visualization
- Part 3: Regression Model Without Dummied Features
- Part 4: Regression Model With Dummied Features 
- Part 5: Classification Model 
  
   
Datasets (folder)
- df.csv                             (main dataframe, 2008 - 2017 data)
- df_master.csv                      (all data cleaned)
- df_master_2008_2012_cleaned.csv    (after cleaning function applied)
- df_master_2013_2017_cleaned.csv    (after cleaning function applied)
- df_master_2008_2012_uncleaned.csv  (before cleaning function applied)
- df_master_2013_2017_uncleaned.csv  (before cleaning function applied)



Presentation
- CW Capstone - Presentation - Predicting Footballers Market Values.pptx
Covered in Power Presentation

The Data Science Process
- Data Science Problem
- Data Collection Cleaning and EDA
- Modeling
- Evaluation
- Conclusion





## Executive Summary & Report

**Data Science Problem**
Create regression models to predict the market value of the players using the annual players' stats collected on transfermarkt.co.uk.
 
Market Value estimates on transfermarkt.co.uk are crowd sourced and ultimately depend on the wisdom of the crowds and moderators discretion. This a decent proxy for market value as there are no other sources of data of this type, size or caliber. 

As Global soccer, aka football, is a large sport that is not as obviously data driven across all player positions in terms of game stats that are widely collected and analyzed, like in American sports such as basketball, baseball, and American football. I thought that this would be an interesting topic to dive into to learn how predictive a player's market value might be as there seem to be so much more than goals and assists that determine player value.
 

Regression: How well do football statistics predict a player's potential market value?
Classification: Using market values and footballer's stats, how accurately can you classify if one is a forward, defender, midfielder or goalie?



**Data Collection Cleaning and EDA**
For more information on how data was gathered, see (Part 1: Data Collection Workbook)

To collect the data I scrapped data and utilized selenium webdriver via Chrome to go to the various team's urls that were created via a formula using their url names and ids gathered from league tables. 

To collect data on 10 years from 2008 - 2017, I collected data from 98 teams of the top five European football leagues in Spain, France, Italy, England, and Germany. The web scrapper went to 980 different webpages to collect the players annual stats and 980 webpages to collect their market value estimates. In total the web scrapper got about 25,000 annual observations of about 7000 unique players, with some player having 10 observations and others just 1. As market valuation changes, I decided to consider each as a individual observation to be used for modeling. I decided for the modeling part to drop all observations that had no market value and no playing time for the year. 



**Target**
My target variable is market value of a player which ranged from low thousands to 108,000,000 (units pounds sterling). 

**Data**
For a total of about 25,000 player observations. 

**Features In Model without Dummied Variables**
- Age
- Market -Value (not included when target)
- Transfer-Fee (not included when target)
- In-Squad (included on bench) 
- Appearances (games played)
- Goals
- Assists
- Yellow Cards
- Second Yellow Cards
- Red Cards
- Substituted On
- Substituted Off
- PPM
- Minutes Played

**Features In Model with Dummied Variables**
All the above features and the following:
- Dummies of general position
    - Forward, Midfielder, Defender, Goalkeeper
- Dummies of teams
    - 98 teams
- Dummies of foot
    - right, left, both


Top features is transfer fee when left in at 51% correlation with market value, otherwise it is assist and goals at .45 and .44 correlation with market value. I decided to break up the data by position, by time played and several other factors to see if their were subsets of the data that regression models showed more promise in predicting market value. 



**Modeling**
I choose to focus on developing vanilla models at first of many regression modeling techniques in order to first see what different slices and modifications of the data showed promise to being able to predict market value on. My assumptions considering the most goal winning determinate data features available of goals and assists were most slanted to forwards and midfielders, that they would be most likely the general positions that one could model most easily rather than defenders and goalkeepers. 


I used vanilla regression models and their underlying algorithms to make predictions and score the accuracy of the models. Model performances ranged from .10 to .675 in their R2 Scores, which is a measure of how much of the variance in the predictions is explained by the model. The purpose of this project is to see if there is more promise in this area to investigate further. As I notice that the assumptions I made had a direct impact on the models and had to let my intuition guide me to place the data in a manner were the attributes of it address the players' purpose, and thus their value and contribution, I fully realized that I must get data for defenders and goalkeepers. Unfortunately, that was not within the time restraints I have at this point. 

**Baseline Model**
Baseline Model scores without dummied categorical features:

LinearRegression model R2 Score: 0.585
LinearRegression model MSE: 42765455460624.98
LinearRegression model RMSE Train: 6819546.765
LinearRegression model RMSE Test: 6539530.217

RandomForestRegressor model R2 Score: 0.607
RandomForestRegressor model MSE: 40548077649726.484
RandomForestRegressor model RMSE Train: 2792440.133
RandomForestRegressor model RMSE Test: 6367737.247

**Curated Model Selection**

With what I was able to discern and model on there was much better performance using players with more than 540 minutes played or play time of about 6 full matches per season. That left about 16183 observations with 130 features - dummied included

The key differences in the models were that the more basic LinearRegression models, Lasso and Ridge models often had lower R2 scores, but less difference in the train and test RMSE (Root Mean Squared Error). As the Mean Squared Error was in the Trillions, it looks intimating, but dealing with market values that range from the low 10,000s of thousands to 100 million, it makes sense that there would be a high MSE. So MSE can be discounted and we can focus on RMSE and R2 score to guide our future decisions on modeling and where to place attention. 

Best performance for Train / Test RMSE difference

LinearRegression model R2 Score: 0.621
LinearRegression model MSE: 23950821762912.28
LinearRegression model RMSE Train: 4860018.106
LinearRegression model RMSE Test: 4893957.679

Best performance for R2 Score

RandomForestRegressor model R2 Score: 0.675
RandomForestRegressor model MSE: 20523282524001.484
RandomForestRegressor model RMSE Train: 2036772.958
RandomForestRegressor model RMSE Test: 4530262.964



** Classification **
As far as classification of the 4 main positions using the general player positions of Forward, Midfielder, Defender and Goalie: 
The support vector machine classifier score well on train and test compared with the other models:

SVC model Training Accuracy Score: 0.733
SVC model Testing Accuracy Score: 0.722

Where for instances some where way overfit like the RandomForestClassifier and others, had too much bias like the AdaBoostClassifier, but was not overfit on training data.

RandomForestClassifier model Training Accuracy Score: 0.978
RandomForestClassifier model Testing Accuracy Score: 0.679
 
AdaBoostClassifier model Training Accuracy Score: 0.556
AdaBoostClassifier model Testing Accuracy Score: 0.561




**Conclusion**

With more time I would do the following: collect data that is more specific to all players individual playing roles. For instance with goalkeepers better data would include shots saved, shots saved to left or right of keeper, penalties stopped versus taken, etc. For defenders better stats would include tackles and balls recovered, passes completed, passes given away, blocked / deflected shots, etc. This type of data is available, but scattered in various websites and a much harder webscrapping task as most of the data is kept on individual players pages rather than on team's aggregate pages. 

However, with the data collected, there are areas were regression modeling can be beneficial to explore further on predicting the market value prices of players. We still have to hold into consideration that the values were crowd sourced. It is a proxy, not a definitive value. However, the definitive values to explore that I am looking at now, are the transfer fee. I will begin to explore regression modeling for predicting transfer fee with what I have learned on predicting market value.

