# Logistic Regression
Logistic Regression is a statistical method for analyzing a dataset in which there are one or more independent variables that determine an outcome. The outcome is measured with a dichotomous variable (in which there are only two possible outcomes). It is used to predict the probability of a binary outcome based on one or more predictor variables.

# The logistic regression model can be expressed mathematically as:
`P(Y=1) = 1 / (1 + e^-(β0 + β1x1 + β2x2 + ... + βnxn))`
Where:
- P(Y=1) is the probability of the outcome being 1 (the positive class).
- x1, x2, ..., xn are the input features (the independent variables).
- β0 is the intercept (the value of the log-odds when all x's are 0).
- β1, β2, ..., βn are the coefficients (the weights assigned to each feature).
- e is the base of the natural logarithm.



# How Logistic Regression Works:
1. **Data Preparation**: The first step is to prepare the data. This includes handling missing values, encoding categorical variables, and scaling features if necessary.
2. **Model Training**: The logistic regression model is trained on the prepared data to estimate the coefficients (β0, β1, β2, ..., βn).
3. **Prediction**: Once the model is trained, it can be used to predict the probability of the outcome being 1 for new data points.
4. **Evaluation**: The performance of the model is evaluated using metrics such as accuracy, precision, recall, and F1-score.


# How to train 

