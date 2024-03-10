# NBA-Analysis-Project-2

## Introduction
In this assignment, we are interested in predicting the Player Efficiency Rating (PER) of a NBA basketball player by using their in-game statistics, such as points, turnovers, field goals. Since PER is a continuous variable, we are going to build a Decision Tree Regression model, instead of a classification model, based on relevant features available in our dataset. We gathered our dataset which contains in-game statistics of 539 NBA players in the 2022-2023 season with 52 columns (we combined two player stats tables: ‘total’ and ‘advanced’) from basketball-reference.com (2022-23 NBA Player Stats: 
Totals: https://www.basketball-reference.com/leagues/NBA_2023_totals.html /
Advanced: https://www.basketball-reference.com/leagues/NBA_2023_advanced.html ).

## Preliminary Analysis
Once we uploaded our dataset to Google Colab, we began analyzing the basics of our dependent variable. By using ‘describe()’ command, we learned that our response variable, ‘PER’, averaged at 13.32 with lowest at -20.90 (Alondes Williams) and highest at 65.60 (Stanley Umude). Attached is the output of the code.

![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/86994884-2349-4d76-9f49-f1ea426c4f1b)


![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/e9cd18c2-5a3c-49f4-9f44-00d3adeb0ba0)


## Data Processing
Before running our Decision Tree Regression model, we encountered two main problems: the strings columns and NaN values. Using ‘dtypes’ command allowed us to find the string columns, such as player’s name, positions, and teams, which should be excluded from our model.

![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/f17fa34d-34c3-4209-a8df-e9f2edfc5ca7)

Next, we noticed there are a few of NaN values in our dataset which obstructed us to train and test our model. When we looked into the NaN values, we found that all of them represent the value of 0 divide by 0. For example, we have 16 observations (players) that have NaN values in ‘3P%’, which stands for three-point field goal percentage, because none of them have made a single three-point attempt in the season. To handle this problem, we chose to simply replace NaN values with zeros before proceeding to the next step. An alternative approach would be using imputation (replacing NaN values with mean or median). However, we don’t think it is appropriate in this case. We wanted to penalize players who didn’t take a field-goal attempt (offensive) and reward players who didn’t have turnovers (defensive).

![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/992ade19-a703-488c-88c7-bdd3bff6d2d8)

## Model Building and Performance
After data processing, we began building our decision tree regressor model. For our features, we ended up with 46 variables after purposely dropped the dependent variable, ‘PER’, the string columns, and the ‘rank’ column. Our model had achieved a high R-squared of 0.86 with a low MSE of 3.29 with validation-set method. Even though we product good predictions on the training set, it is likely to overfit the data using more than 40 features in the model, leading to poor test set performance. To mitigate overfitting, we employed pruning technique by tunning the model’s hyperparameters using GridSearchCV with 5-fold cross-validation. We primarily focused on the ‘max_depth’ hyperparameter for enhanced interpretability. Although experimenting with 'min_sample_leaf' and 'min_samples_split' resulted in lower MSE and higher 'max_depth', we ultimately chose a model with a 'max_depth' of 5, incorporating 14 variables, which achieved a score of 13.72 (see appendix(1) for details).

![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/91d947c4-d541-4446-9765-71704399a708)

![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/a9e0e92c-82f6-4b4b-bac2-aef0d6316f26)

In appendix(2), we presented all the variables in the model along with their corresponding feature importance. Among the 14 variables included in the model, we learned that ‘WS/48’ is the most important factor in determining player’s efficiency, followed by ‘OBPM’, ‘BPM’, ‘FG%’, etc. One explanation would be: given a player with higher wins shares per 48 minutes (WS/48 > 0.113) and higher Box Plus/Minus (BPM > 17.4) are more efficient players. Although this smaller, pruned tree produces a greater error, we assume it will perform better and more consistently across different datasets.

In summary, we believe our model would be a useful tools for the team’s player scouting and recruitment team to find the most efficient player.

## Limitations
We acknowledge several limitations in our analysis. Firstly, the interpretability of our model remains a challenge despite reducing the number of variables to 14. One potential improvement involves re-running the GridSearchCV process, starting with the 14 variables from our current model, to further prune the tree.
Secondly, the size of our dataset, limited to the 2023-2024 season with data from 539 players, may affect the accuracy of our model. Expanding the dataset to include player stats from the past decade could enhance model performance.

## Appendix
### (1): Final Model Demonstration
![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/f45b2b85-0672-4115-a52b-4a5440ba621e)

### (2): Features Included
![image](https://github.com/Jecoc907/NBA-Analysis-Project-2/assets/71363412/7642b359-183e-4e2b-9c5f-da6ffc8c22e3)



























