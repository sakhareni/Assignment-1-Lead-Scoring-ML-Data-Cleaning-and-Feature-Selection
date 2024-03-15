An education company named X Education sells online courses to industry professionals. On any given day, many professionals who are interested in the courses land on their website and browse for courses.

The company markets its courses on several websites and search engines like Google. Once these people land on the website, they might browse the courses or fill up a form for the course or watch some videos. When these people fill up a form providing their email address or phone number, they are classified to be a lead. Moreover, the company also gets leads through past referrals. Once these leads are acquired, employees from the sales team start making calls, writing emails, etc. Through this process, some of the leads get converted while most do not.

In this classification notebook we are trying to predict whether the lead will be converted or not

Below are some of the steps I followed 

1)Data Cleaning 

2)Exploratory Data Analysis

3)Label Encoding for Categorical Values

4)Outlier Removal

5)Normalization

6)Feature Selection

7)Linear Regression

8)Variable significance using
  a)Random forest(RFE)

9)Model Training using Logistic regression (Confusion Matrix)

10)Regularization using VIF

11)Data imputation using KNN

12)L2 Regularization named Ridge for Classification Dataset

13)Logloss - Log loss, also known as cross-entropy loss, is a commonly used metric to evaluate the performance of probabilistic classification models.

Conclusion: 

**1) Is the relationship significant?**
Yes the relationship is significant since

the p value for most values apart from TotalVisits which is 0.043 is zero and also acceptable limit of 0.05 means TotalVisits is also in threshold

Accuracy as per Gradient boosting is Accuracy: 92.42%

Accuracy as per L2 regularization: Accuracy: 82.50%

R-squared (uncentered): 0.646 which is high and in between 0 and 1 which is acceptable

since this is a classification data set Gradient boosting, L2 regularization also help us understand relationship

**2) Are any model assumptions violated?**
No, the dependent variable is 0/1, so the question is a classification question which make sense to all models in AutoML.

**3) Is there any multicollinearity in model**
Based on the provided Variance Inflation Factor (VIF) values, which measure multicollinearity, here's an assessment:

Multicollinearity Assessment: No or Low Multicollinearity:

Do Not Call has a VIF close to 1 (1.000858), indicating no significant multicollinearity with other variables.TotalVisits (VIF = 1.369135), Do Not Email (VIF = 1.062313), What is your current occupation (VIF = 1.062538), and Tags (VIF = 1.078851) also exhibit low multicollinearity.Moderate Multicollinearity:
Lead Origin (VIF = 1.232737), Lead Source (VIF = 1.243336), Total Time Spent on Website (VIF = 1.239124), and Specialization (VIF = 1.302815) have moderate VIF values but still generally acceptable.
Potential Concern for Multicollinearity:Page Views Per Visit (VIF = 1.525026), Lead Quality (VIF = 1.216500), Last Notable Activity (VIF = 2.359150), and Last Activity (VIF = 2.379227) have relatively higher VIF values. These variables might be associated with each other to some extent.
Later on we will regularize these values using PCA
VIF multicoliinearity shows that value of dependent variable is less than 5 which is the treshold hence there is a lack of multicollinearity hence lack of it

**4) In the multivariate models are predictor variables independent of all the other predictor variables?**
Yes

The VIF values are a measure of how much the variance of the estimated regression coefficients increases when predictor variables are correlated. A VIF greater than 5 or 10 is often considered an indication of multicollinearity.

the VIF values are generally low, ranging from approximately 1 to 2.38. This suggests that there is not ** severe multicollinearity among the predictor variables in the logistic regression model **. The VIF values below 5 indicate that the predictor variables are not highly correlated with each other.

the assumption of independence among predictor variables is reasonably met in the multivariate logistic regression model.

**5) In multivariate models rank the most significant predictor variables and exclude insignificant ones from the model.**

In the multivariate model as discussed in class by the professor according to random forest

Using the top 10 values for calculating in H20 instance

Random Forest Feature Importance:

Lead Quality 0.234205
Tags 0.187346
Total Time Spent on Website 0.181603
Last Notable Activity 0.074967
Last Activity 0.047844
Specialization 0.046484
Lead Origin 0.046345
Lead Source 0.041348
Page Views Per Visit 0.037835
TotalVisits 0.037129
Discarding the below features:

What is your current occupation 0.028997
City 0.027003
Do Not Email 0.008699
Do Not Call 0.000195

**6) Does the model make sense?**
Reported on test data.

MSE: 0.05036686593649161
RMSE: 0.22442563564907556
MAE: 0.11525583859865761
RMSLE: 0.1586263024675848
Mean Residual Deviance:0.05036686593649161
Performance Metrics: The provided metrics (MSE, RMSE, MAE, RMSLE, Mean Residual Deviance) offer insights into the model's accuracy and performance on the test data. Lower values for these metrics generally indicate better performance. the metrics suggest a reasonably good fit
Variable Importance: The variable importances indicate the significance of different features in making predictions. Features such as "Lead Quality," "Tags," and "Total Time Spent on Website" are identified as crucial predictors, aligning with expectations and providing insights into the factors influencing the model.

Training Progression: The scoring history shows a systematic improvement in performance as the number of trees increases, indicating that the model is learning from the data.

The log loss value of approximately 0.3921 indicates that, on average, the model's predicted probabilities are relatively close to the actual outcomes. The model's predicted probabilities have relatively low uncertainty, contributing to the lower log loss.

Accuracy before regularization is 81.98%

Accuracy as per Gradient boosting is Accuracy: 92.42%

Accuracy as per L2 regularization: Accuracy: 82.50%

The above numbers suggest that the model makes sense

**7) Does regularization help?**
The regularization seem to be helping a bit the accuracy of the model increases ahead from 81.98% to 82.50 after PCA regularization using L2 regularization Ridge regression

The accuracy of the model gets better Marginally

**8) Which independent variables are significant?**
This suggests that, under the standard significance level of 0.05, you would reject the null hypothesis for each variable, indicating that they are likely to be significant predictors of the response variable in your model. Therefore, all the independent variables (Lead Origin, Lead Source, TotalVisits, Total Time Spent on Website, Page Views Per Visit, Last Activity, Specialization, Tags, Lead Quality, Last Notable Activity) are considered statistically significant in this analysis.

**9 Which hyperparameters are important?**
For RandomForestClassifier:

n_estimators: The number of trees in the forest = 100.
max_depth: The maximum depth of the tree. = default
min_samples_split: The minimum number of samples required to split an internal node. *default**
min_samples_leaf: The minimum number of samples required to be at a leaf node . default
max_features: The number of features to consider when looking for the best split. default
For LogisticRegression:

penalty: Used to specify the norm used in the penalization (regularization). = l2
C: Inverse of regularization strength; smaller values specify stronger regularization. = 1.0
hyperparameters in H20 instance

The important hyperparameters for the GBM_3_AutoML_1_20240219_223125 which is the 2nd best model according to variable importance but is the best model because the best model is madeup of multiple model which in our case is StackedEnsemble_AllModels_1_AutoML_1_20240219_223125

the choice of the metalearner algorithm (in this case, Generalized Linear Model or 'glm'),

the number of folds for metalearner cross-validation (set to 5), * the selection of base models (e.g., GBM, XGBoost, DRF, GLM)

the random seed for reproducibility (set to 1245).

Adjusting these hyperparameters can impact model performance and should be considered during tuning.
