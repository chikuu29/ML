# Linear Regression
Linear regression is a fundamental machine learning algorithm used for predicting a continuous target variable based on one or more input features. The goal of linear regression is to find the best-fitting line (or hyperplane in higher dimensions) that minimizes the difference between the predicted values and the actual values in the training data.
The linear regression model can be expressed mathematically as:

`y = β0 + β1x1 + β2x2 + ... + βnxn + ε`
Where:
- y is the target variable (the value we want to predict).
- x1, x2, ..., xn are the input features (the independent variables).   
- β0 is the intercept (the value of y when all x's are 0).
- β1, β2, ..., βn are the coefficients (the weights assigned to each feature).
- ε is the error term (the difference between the predicted and actual values).


# Formula
 y= mx + c
Where:
- y is the dependent variable (the value we want to predict).
- x is the independent variable (the input feature).
- m is the slope of the line (the coefficient that represents the relationship between x and y).
- c is the y-intercept (the value of y when x is 0).
The goal of linear regression is to find the values of m and c that minimize the difference between the predicted values (y) and the actual values in the training data. This is typically done using a method called "least squares," which minimizes the sum of the squared differences between the predicted and actual values.




# Math Behind Linear Regression :
The math behind linear regression involves finding the best-fitting line that minimizes the sum of squared errors (SSE) between the predicted values and the actual values in the training data. The coefficients (m and c) are calculated using the following formulas:

m = (N * Σ(xy) - Σx * Σy) / (N * Σ(x^2) - (Σx)^2)

c = (Σy - m * Σx) / N

Where:
- N is the number of data points.
- Σ(xy) is the sum of the product of x and y for all data points.
- Σx is the sum of all x values.    
- Σy is the sum of all y values.
- Σ(x^2) is the sum of the squares of all x values.

Once we have the coefficients m and c, we can use the linear regression model to make predictions for new input values of x by plugging them into the formula y = mx + c. The predicted value of y will be the output of the model for the given input x.

# Example
Let's say we have a dataset of house prices based on the size of the house (in square feet). We want to use linear regression to predict the price of a house based on its size.

| Size (sq ft) | Price ($) |
|--------------|-----------|
| 1000         | 200,000   |
| 1500         | 300,000   |
| 2000         | 400,000   |
To find the coefficients m and c, we can calculate the necessary sums:

- N = 3 (number of data points)
- Σx = 4500 here (1000 + 1500 + 2000)
- Σy = 900,000 here (200,000 + 300,000 + 400,000)
- Σ(xy) = 2,250,000,000 here (1000 * 200,000 + 1500 * 300,000 + 2000 * 400,000)
- Σ(x^2) = 15,500,000 here (1000^2 + 1500^2 + 2000^2)

Now we can plug these values into the formulas to calculate m and c:

m = (3 * 2,250,000,000 - 4500 * 900,000) / (3 * 15,500,000 - (4500)^2) = 200

c = (900,000 - 200 * 4500) / 3 = 0

Now we have the coefficients m = 200 and c = 0. The linear regression model can be expressed as:
y = 200x

Now we can use this model to make predictions. For example, if we want to predict the price of a house that is 2500 square feet, we can plug x = 2500 into the formula:
y = 200 * 2500 + 0 = 500,000

This means that the predicted price of a house that is 2500 square feet is $500,000 according to our linear regression model.
Here is a simple implementation of linear regression in Python using NumPy:
```python
import numpy as np
# Sample data
X = np.array([1000, 1500, 2000])  # Size (sq ft)
y = np.array([200000, 300000, 400000])  # Price
# Calculate coefficients
N = len(X)
sum_x = np.sum(X)
sum_y = np.sum(y)
sum_xy = np.sum(X * y)
sum_x_squared = np.sum(X ** 2)
m = (N * sum_xy - sum_x * sum_y) / (N * sum_x_squared - sum_x ** 2)
c = (sum_y - m * sum_x) / N
# Make a prediction
def predict(x):
    return m * x + c
# Predict the price of a house that is 2500 square feet
predicted_price = predict(2500)
print(f"Predicted price for a house that is 2500 sq ft: ${predicted_price:.2f}")
```


# Evaluation
To evaluate the performance of a linear regression model, we can use various metrics such as R-squared (R2 Score), Mean Absolute Error (MAE), Mean Squared Error (MSE), and Root Mean Squared Error (RMSE). These metrics help us understand how well the model is fitting the data and how accurate its predictions are.
- R-squared (R2 Score): This metric indicates the proportion of the variance in the dependent variable that is predictable from the independent variable(s). It ranges from 0 to 1, where a value closer to 1 indicates a better fit.
- Mean Absolute Error (MAE): This metric measures the average absolute difference between the predicted values and the actual values. A lower MAE indicates better model performance.
- Mean Squared Error (MSE): This metric measures the average of the squares of the differences between the predicted values and the actual values. A lower MSE indicates better model performance.
- Root Mean Squared Error (RMSE): This metric is the square root of the MSE and provides a measure of the average magnitude of the errors in the same units as the target variable. A lower RMSE indicates better model performance.
In Python, we can calculate these metrics using the `sklearn.metrics` module. Here's an example of how to evaluate a linear regression model using R2 Score:
```python
from sklearn.metrics import r2_score
# Assuming y_true are the actual values and y_pred are the predicted values
y_true = np.array([200000, 300000, 400000])  # Actual prices
y_pred = np.array([210000, 290000, 410000])  #
r2 = r2_score(y_true, y_pred)
print(f"R2 Score: {r2:.4f}")
```