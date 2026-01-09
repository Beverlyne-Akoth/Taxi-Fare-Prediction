# Project Description
Using Python and Python libaries for data science to predict taxi fares for the New York City Taxi and Limousine Commission (TLC).

# Project Overview
The objective of the project is to build a machine learning model that can be used to predict taxi fares for the New York City Taxi and Limousine Commission (TLC).
The TLC data comes from over 200,000 taxi and limousine licensees, making approximately one million combined trips per day. 
The tasks involved in the project are;
* Model building
* Model evaluation
* Summarize findings for Automatidata and the stakeholders at TLC

</br> While analyzing the ethical considerations of the model, it was discovered that Drivers who didn't receive tips will probably be upset that the app told them a customer would leave a tip. If it happened often, drivers might not trust the app. Drivers are unlikely to pick up people who are predicted to not leave tips. Customers will have difficulty finding a taxi that will pick them up, and might get angry at the taxi company. Even when the model is correct, people who can't afford to tip will find it more difficult to get taxis, which limits the accessibility of taxi service to those who pay extra.
</br> Since it's not good to disincentivize drivers from picking up customers. It could also cause a customer backlash. The problems seem to outweigh the benefits.
</br> To counter the problem, we can build a model that predicts the most generous customers. This could accomplish the goal of helping taxi drivers increase their earnings from tips while preventing the wrongful exclusion of certain people from using taxis.

# EDA and Feature Engineering
While conducting EDA, it was discovered that customers who pay cash generally have a tip amount of $0. To meet the modeling objective, the data was sampled to select only the customers who pay with a credit card.
</br> Additional columns that were created during feature engineering to improve model performance were: month column, tip percentage, generous column to classify the tips, am_rush, and pm_rush hour columns.
</br> After this, categorical variables were encoded, and the data split into training (50%), validation (25%), and test(25%) sets.

# Model Building
Two models were used and the results from both were compared to see which one had the best results. These were RandomForest and XGBoost.
The cross-validation process used the F1 score as the metric to determine the best hyperparameters, and subsequently, the final model trained (refitted) on the entire dataset using those best parameters. 
The best parameters for the RF model after hyperparameter were: 
{'max_depth': None,
 'max_features': 1.0,
 'max_samples': 0.7,
 'min_samples_leaf': 5,
 'min_samples_split': 2,
 'n_estimators': 300}
 </br> This had a best score of 0.7332670669367042
 
 The best parameters for the XGBoost were
 {'learning_rate': 0.1,
 'max_depth': 8,
 'min_child_weight': 2,
 'n_estimators': 500}
 </br> This had a best score of 0.699273635433734

</br> Below is a summary of the model's performance on the validation and test sets.
model    	  precision 	recall	    F1	  accuracy
0	RF CV	    0.685192	0.788734	0.733267	0.698001
0	RF test	  0.692926	0.804605	0.744601	0.709466
0	XGB test	0.679062	0.738643	0.707601	0.678677
0	XGB CV	  0.673282	0.727442	0.699274	0.670652

</br>As it can be seen, the RF model performs better and is therefore the champion model.
 </br>After computing feature importance, the strongest features to the model are VendorID, predicted_fare, mean_duration, and mean_distance. It is interesting that VendorID is the most predictive feature. This seems to indicate that one of the two vendors tends to attract more generous customers. It may be worth performing statistical tests on the different vendors to examine this further.
