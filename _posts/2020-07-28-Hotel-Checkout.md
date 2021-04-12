---
layout: post
title: Hotel Checkout Project
subtitle: Determining whether a person will check out or cancel a book in a hotel in Portugal
cover-img: /assets/img/hotel_chekout.jpeg
tags: [books, test]
---

### Project Goals:
Construct classification models that are able to predict whether a hotel guest will end up canceling or checking out from his/her booked hotel in Portugal.
Build a [Heroku App](https://hotelcheckout.herokuapp.com) that is user friendly and implements the best machine learning model.

### Background:
The data set was collected from a publication in Science Direct but was aggregated in Kaggle(1,2). It consists of data from a resort hotel and a city hotel in Portugal. It also consists of data from the years 2015, 2016, and 2017. The data set was fairly cleaned but I still had to do some data wrangling to remove features that were redundant, leaked information of my target set, or features that ended up having low permutation importance.

### Processes:
I began this project by doing some exploratory analysis and looking at the descriptive statistics of both numerical and categorical features. Since each observation represented a booking, I choose the Reservation Status column as my target vector. It's important to note that the original data had 3 classes in the target vector. The classes consisted of 'No-Show," "Cancelled," and "Check Out". I grouped "No-Shows" with "Cancelled " as "No-Shows" are typically canceled by the hotel, so I assume a late cancellation whenever there was a "No Show". This model works best when this assumption is taken to account. Additionally, this data is limited to resort and city hotels in Portugal, so the model, likely works differently, if we were dealing with motels, apartment hotels, taken place elsewhere. Lastly, this data set is limited to 3 years; it would be helpful if in the future if I could aggregate more data from other hotels, and see if I can better generalize or even improve the accuracy of my models.

![image](/assets/img/hotel_project_photos/bar_graph.png)




During my exploratory analysis, I encounter data leakage; this occurs whenever there is information about the target set, that gets leaked into your features, influencing your model to overfit. Consequently, it poorly generalizes to other data. I notice leakage with the is_canceled feature; this feature has binary values of 0 and 1, where 1 represents the person canceled the booking and 0 that he did not.

![image](/assets/img/hotel_project_photos/wrangle_data.png)

This was a time-series data set so I split the data into 3 different data sets, training, validation, and testing set based on years 2015,2016, and 2017. The shapes of the data set were the following:

![image](/assets/img/hotel_project_photos/shape_of_train.png)   


The baseline represents the simplest prediction. As a result, I choose the majority class ("Check-Out"), which also represents the positive class in the rest of my models.

![image](/assets/img/hotel_project_photos/baseline.png)



### Model Building & Evaluation Metrics

### Model Definitions
Random Forest Classifier: a classification model that uses a machine-learning algorithm to fit multiple decision trees to subsets of the data. It then takes the averages of the predictions made in these decision trees to improve accuracy and control overfitting(3).
Logistic Regression: a linear model for classification that uses the logistic function to predict probabilities for individual observations in the data set. It predicts classes based on these probabilities(4).
XGBoost Classifier: is a classification model that takes advantage of gradient boosting and improves upon it. Gradient boosting is a machine learning algorithm that systematically produces weak ensemble models (often decision trees), and gradually corrects and builds on these weak models; ultimately it produces a prediction model(5).

Although I used accuracy to measure the effectiveness of the model, I was still considerate of the slight class imbalance. So on top of accuracy, I used the AUC score and AUCROC curve to measure which model was the best.

### Model Optimization Techniques:
I mainly used the Random Search CV technique to optimize the hyperparameters in my Random Forest Classifier; this hyper tunning technique involves testing a random set of hyperparameters and then choosing the best parameters that result in the best score (such as accuracy) for the model (6).

![image](/assets/img/hotel_project_photos/model0_randomforest.png)

![image](/assets/img/hotel_project_photos/randomforestclassification.png)
)
I was able to optimize my XGBoost model and improve my AUC score with early stopping and permutation importance. Early stopping involves picking the best number of n-estimators or iterations that the XGBoost model can run until it stops improving (7). This helps one save time, and reduce overfitting.

To further optimize the XGBoost model, I used permutation importances. This technique involves shuffling the values of the features/columns and testing the accuracy of the model; if this shuffling results in a model with significantly lower accuracy, then this feature is considered to be important (8). The best features are represented as bigger weights, and they are the features with the most predictive power.

Using this technique, I was able to reduce the number of features in this model, from 22 to 9. Reducing the features, helped me create a better Heroku app as well, and allowed my models to run faster.

![image](/assets/img/hotel_project_photos/model1.png)

![image](/assets/img/hotel_project_photos/xgboost_permutation_importances.png)

![image](/assets/img/hotel_project_photos/classification_xgboost_report.png)

The last model I worked was was Logistic Regression; I optimize the model by changing the default max_iter from 100 to 200. I mainly used the model to compare against XGBoost and Random Forest Classifier.

### Evaluation Metrics
Note that the validation scores were included inside the classification reports. This allows me to be concise in reporting all the validation scores for all three models. I also summarize the AUC validation scores for all three models in the AUCROC curve below.

Quick Definition on the AUC-ROC curve: The AUC represents the area of the curve or the summary of ROC. On the other hand, ROC represents the probability curve itself; this curve plots the true positive rate against false-positive rates. In other words, ROC is checking at different probabilistic thresholds for how good the model is able to maximize true positives against false positives. Ideally, the AUC would be 1, and we would always be correctly predicting true positives and true negatives. True positives represent the main class I was interested in predicting ("Check-Out"), while true negatives represent the other class ("Canceled") I predicted, and correctly classified (9).

It's important to note, that the Random Forest and Logistic Regression used 22 features, while XGBoost only used 9, so I was ultimately able to create an XGBoost model that used fewer features and had better predictive power. As you can see from the curve below, the best classification model ended up being XGBoost with respect to AUC score.

![image](/assets/img/roc_for_all_models_validation_set.png)

### Visualizations for Model Interpretation
Using XGBoost on the validation data set

### Partial Dependence Plot
The x-axis represents the types of deposits made: number 1 == "no-deposit", 2 == "refundable", 3=="no refundable". The y-axis represents the impact on whether someone will check out.

![image](/assets/img/pdp_xgboost.png)

In this Partial Dependence Plot, non-refundable deposits are negatively impacting the probability that guest checks out. It turns out those who choose to make non-refundable deposits represent a minority class, and out of that minority class, the vast majority ended up canceling. The fact a lot of people aren't doing non-refundable deposits explains this negative impact on this model.
From the validation data set alone, we can also see that people are already likely to cancel if the made a Non Refund deposit. Similar distributions can be seen in the Training data set as well.Interactive Partial Dependence Plot

Deposit 1, represents no deposit, while 3 represents a non-refundable deposit. The iris scale represents the probability someone will check out based on what country and type of deposit are made.Countries are labeled by numbers (e.g PRT == 1).The y-axis represents countries encoded by numbers. This interactive partial dependence plot above shows that the model cares more about what type of deposit is being made than where the booking took place. Given more bookings come from Portugal, it makes sense that the XGBoost model tends to penalize Portugal bookings heavier when they involve non-refundable deposits.
Value counts of where the bookings took place from the training data set.Shapley Values

The red chevron arrows represent features that positively impact whether someone will end up checking out. While, the blue arrows represent negative impact, influencing someone to more likely cancel. Someone from country 1 or PRT (Portugal), having picked 0 parking spaces, negatively impacts whether this person checks out.

In this shapley values plot, a non-refundable deposit, with a lead time of 113, and the person coming from a country of PRT determine with a 100% probability that he will end up canceling. It's important to note the model has a 77% accuracy and a .79 AUC.
Test Results:

Conclusion:
Throughout this process, I went over 3 models and explain their importance. I used the training data to fit my models and used the validation data set to evaluate my model's performance. The AUC-ROC curves did a good job at summarizing this point.
The most important features that influence if someone checked out or not were: deposit type, followed by country, and lead time. On top of that, I looked at individual observations and tried to make sense out of them using Partial Dependence Plots. Lastly, using Shapley Values, we saw how using different combinations of features influenced the prediction;
Lastly, the XGBoost and Random Forest had similar accuracy and ROC-AUC scores. Ultimately I used my Random Forest model to construct my Heroku app you can test below.

Predict for yourself if a guest ends up checking out here:
https://hotelcheckout.herokuapp.com/predictions

GitHub Notebook:
https://github.com/JonRivera/Hotel_Check_Out_Project/tree/master/notebooks

References:
1)https://www.sciencedirect.com/science/article/pii/S2352340918315191#bib6
2)https://www.kaggle.com/jessemostipak/hotel-booking-demand
3)https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html
4)https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression
5)https://en.wikipedia.org/wiki/Gradient_boosting
6)https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html
7)https://xgboost.readthedocs.io/en/latest/python/python_intro.html
8)https://eli5.readthedocs.io/en/latest/blackbox/permutation_importance.html
9)https://www.analyticsvidhya.com/blog/2020/06/auc-roc-curve-machine-learning/
