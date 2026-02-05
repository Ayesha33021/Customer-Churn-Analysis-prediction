# Customer-Churn-Analysis-prediction
In this guide we will explore the Customer Churn dataset to predict churn effectively.


Customer churn refers to situations where a customer stops utilizing a given service-provider’s services, leading to revenue loss. Analyzing this process helps businesses comprehend why customers leave their markets. High customer churn can lead to revenue and business-model-growth problems. Analyzing customer churn helps businesses take proactive measures towards retaining customers.

we start by:
# Understanding the Dataset
To gain insights into the dataset we first check for missing values and understand its structure. The dataset includes features such as:
CustomerID           0
Age                  0
Gender               0
Tenure               0
Usage Frequency      0
Support Calls        0
Payment Delay        0
Subscription Type    0
Contract Length      0
Total Spend          0
Last Interaction     0
Churn                0
dtype: int64
         CustomerID           Age        Tenure  Usage Frequency  \
count  64374.000000  64374.000000  64374.000000     64374.000000   
mean   32187.500000     41.970982     31.994827        15.080234   
std    18583.317451     13.924911     17.098234         8.816470   
min        1.000000     18.000000      1.000000         1.000000   
25%    16094.250000     30.000000     18.000000         7.000000   
50%    32187.500000     42.000000     33.000000        15.000000   
75%    48280.750000     54.000000     47.000000        23.000000   
max    64374.000000     65.000000     60.000000        30.000000   

       Support Calls  Payment Delay   Total Spend  Last Interaction  \
count   64374.000000   64374.000000  64374.000000      64374.000000   
mean        5.400690      17.133952    541.023379         15.498850   
std         3.114005       8.852211    260.874809          8.638436   
min         0.000000       0.000000    100.000000          1.000000   
25%         3.000000      10.000000    313.000000          8.000000   
50%         6.000000      19.000000    534.000000         15.000000   
75%         8.000000      25.000000    768.000000         23.000000   
max        10.000000      30.000000   1000.000000         30.000000   

              Churn  
count  64374.000000  
mean       0.473685  
std        0.499311  
min        0.000000  
25%        0.000000  
50%        0.000000  
75%        1.000000  
max        1.000000 

We check the number of churners and non-churners to understand the balance of the dataset.
# Data Preprocessing
Handling Missing and Incorrect Values Before processing we ensure that all numerical columns contain valid values. The TotalCharges column sometimes has empty spaces which need to be converted to numerical values.

# Handling Categorical Variables
Some features like State, International Plan and Voice Mail Plan are categorical and must be converted into numerical values for model training.
# LabelEncoder()
converts categorical values into numerical form. Each unique category is assigned a numeric label. The loop iterates through each categorical column and applies fit_transform() to encode categorical variables into numbers.
# Feature Selection and Splitting Data
We separate the features (X) and target variable (y) and split the dataset into training and testing sets.
X = dataset.drop(['customerID', 'Churn'], axis=1) removes the customerID (irrelevant for prediction) and Churn column (target variable). y = dataset['Churn'] defines y as the target variable, which we want to predict. train_test_split() splits data into 80% training and 20% testing for model evaluation.
# Feature Scaling:
Since features are on different scales we apply standardization to improve model performance. It prevents models from being biased toward larger numerical values and improves convergence speed in optimization algorithms like gradient descent

# StandardScaler():
Standardizes data by transforming it to have a mean of 0 and a standard deviation of 1 ensuring all features are on a similar scale. fit_transform(X_train): Fits the scaler to the training data and transforms it. transform(X_test): Transforms the test data using the same scaling parameters.

# Model Training and Prediction
For training our model we use Random Forest Classifier. It is an ensemble learning method that combines the results of multiple decision trees to make a final prediction.

# Model Evaluation
Accuracy Score To measure model performance we calculate accuracy using the accuracy_score function.
we get an accuracy of 1.00
we create a confusion matrix which showss how well the model predicts customer churn. It correctly identifies 6771 non-churners and 6094 churners. However 6 non-churners are wrongly classified as churners and 4 churners are missed.
