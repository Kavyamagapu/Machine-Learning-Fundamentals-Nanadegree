# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### NAME HERE
Kavya Magapu

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
TODO: Add your explanation

when I tried to submit the predictions, I realize that some predictions may be negative and kaggle won't accept that so I set the negative values to ZERO

### What was the top ranked model that performed?
TODO: Add your explanation
My top ranked model is Weighted_Ensemble_L3 with lowest root mean square error with the new feature added data. 

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
TODO: Add your explanation
I find some features were nearly normally distributed such as [temp, atemp, humidity, windspeed],some features were categorical such as [season, weather] it also seemed that the data was nearly uniformly distributed among the 4 seasons.

I followed the notebook suggestion of adding the hour feature to the data which seemed reasonable since it is a more general feature and might give the trained models more intuition to which hours of the day in general might have the largest bike share demand without specifying a certain year, month or day.

### How much better did your model preform after adding additional features and why do you think that is?
TODO: Add your explanation
After adding new feature, evaluation metric root mean square error changed from 53.143607 to 30.904446.I thought it is a good change.  

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
TODO: Add your explanation
After performing hyperparameter optimization using the data with the added hour feature, the model's training rmse changed from -30.904446 to -39.229699.I consider this as a better change in model score. 

### If you were given more time with this dataset, where do you think you would spend more time?
TODO: Add your explanation

I spend time to find and add new features as adding hour feature gives a better result and also transform the season column.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|     model    | hpo1                                                                                                                                        | hpo2                                                                   | hpo3         | score   |
|:------------:|---------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|--------------|---------|
| initial      | default_vals                                                                                                                                | default_vals                                                           | default_vals | 1.78405 |
| add_features | default_vals                                                                                                                                | default_vals                                                           | default_vals | 0.72913 |
| hpo          | NN : epochs = 10,lrn_rate:(1e-4, 1e-2,  default=5e-4, log=True),  activation: (relu, softrelu, tanh), dropout_prob: (0.0, 0.5, default=0.1) | GBM : num_boost_round:100, num_leaves:(lower=26, upper=66, default=36) | default_vals | 0.49800 |

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_train_score.png](nd009t-c1-intro-to-ml-project-starter/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](nd009t-c1-intro-to-ml-project-starter/model_test_score.png)

## Summary
TODO: Add your explanation

Strating from the data,I have two files train.csv for training and test.csv for generating predictions.Here train.csv contains season, holiday, workingday, weather, temp, atemp, humidity, windspeed, casual, registered as features and count as the target label. But in test.csv there is no casual, registered columns.So, I ignored these two columns while training the model.

In the next step, I trained the model with time_limit = 600 and used root mean square error as evaluation metric with presets as best_quality.After training the model, WeightedEnsemble_L3 performed well according to fit_summary() and have model score -53.143607.
Then created predictions and transformed them in a way that if any negative values are there then set them to zero as kaggle did not accept negative values.

After reviewing the model score, Performed EDA and added new feature to the data which is hour extracted from datetime column and changed season and weather to category type.Then again trained the model with data including new feature and got some improvement in model score.

Finally performed hyperparameter tuning and analyzed all the model scores for each runs and autogluon ia a good model to work with.I learned that EDA and Hyperparameter tuning plays a key role and helps to increace model performance.

