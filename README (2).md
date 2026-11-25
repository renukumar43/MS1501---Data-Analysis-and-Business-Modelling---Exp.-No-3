# Experiment 3: Regression Techniques in Business Data(Simple Linear Regression)

##  Aim
To implement Simple Linear Regression in Python to study and predict the relationship between two business-related variables.

## Dataset
A sample business dataset representing the relationship between **Advertising Expenditure** (in Lakhs) and **Sales Revenue** (in Crores). The goal is to analyze how changes in advertising investment affect sales performance.

| Index | Advertising (Lakhs) | Sales (Crores) |
| :---: | :---: | :---: |
| 0 | 18 | 12 |
| 1 | 22 | 18 |
| 2 | 25 | 20 |
| 3 | 30 | 24 |
| 4 | 35 | 28 |
| 5 | 40 | 35 |
| 6 | 45 | 38 |
| 7 | 50 | 40 |
| 8 | 55 | 42 |
| 9 | 60 | 45 |

## Algorithm / Steps Followed
1. Import required Python libraries (`numpy`, `pandas`, `matplotlib`, `scikit-learn`).
2. Create and load the dataset into a Pandas DataFrame.
3. Display the dataset.
4. Select independent ($X$) and dependent ($Y$) variables and reshape $X$ into a 2D array.
5. Build a `LinearRegression` model using `sklearn.linear_model`.
6. Fit the model and calculate the intercept ($a$) and slope ($b$).
7. Predict $Y$ values for given $X$ values and evaluate performance using the $R^2$ score.
8. Plot the actual data points alongside the fitted regression line and predict sales for a new advertising budget.

##  Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation / Handling** | `np.array()` | Create numerical arrays for regression input data |
| | `pd.DataFrame()` | Create or manage tabular data for regression |
| **Model Building (Scikit-learn)** | `LinearRegression()` | Initialize the Simple Linear Regression model |
| | `model.fit()` | Train the linear regression model using $X$ and $Y$ values |
| | `model.predict()` | Predict $Y$ values for given $X$ inputs using the fitted model |
| | `model.score()` | Calculate model performance ($R^2$ score) |
| **Visualization (Matplotlib)** | `plt.scatter()` | Plot scatter points (actual data points) |
| | `plt.plot()` | Plot regression line (predicted relationship) |
| | `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.show()` | Configure and display the regression plot |

##  Program & Output

# 1. Import required Python libraries
import numpy as np  
import pandas as pd  
import matplotlib.pyplot as plt  
from sklearn.linear_model import LinearRegression  

print("Libraries imported successfully.")  

# 2. Create the business dataset
advertising = np.array([18, 22, 25, 30, 35, 40, 45, 50, 55, 60])  
sales = np.array([12, 18, 20, 24, 28, 35, 38, 40, 42, 45])  

df = pd.DataFrame({
    "Advertising (Lakhs)": advertising,
    "Sales (Crores)": sales  
})

print("Dataset created successfully.")  
display(df)  

# 3. Select independent (X) and dependent (Y) variables
X = df[["Advertising (Lakhs)"]]  # Independent variable (2D)
Y = df["Sales (Crores)"]         # Dependent variable

print("Independent variable (X):")
display(X)

print("Dependent variable (Y):")  
display(Y)  

# 4. Build and train the Simple Linear Regression model  
model = LinearRegression()  
model.fit(X, Y)  

print("Linear Regression model trained successfully.")  

# 5. Calculate intercept (a) and slope (b)
a = model.intercept_
b = model.coef_[0]

print("Intercept (a):", round(a, 4))  
print("Slope (b):", round(b, 4))  
print(f"Regression equation: Sales = {a:.4f} + ({b:.4f} × Advertising)")  

# 6. Predict sales values and evaluate the model
predicted_sales = model.predict(X)  
r2_score = model.score(X, Y)  

results = df.copy()
results["Predicted Sales (Crores)"] = predicted_sales

print("Actual and predicted sales:")  
display(results.round(2))  

print("R2 Score:", round(r2_score, 4))  

# 7. Plot actual data points and fitted regression line
plt.figure(figsize=(8, 5))  
plt.scatter(X["Advertising (Lakhs)"], Y, label="Actual Sales")  
plt.plot(X["Advertising (Lakhs)"], predicted_sales, label="Regression Line")  
plt.title("Simple Linear Regression: Advertising vs Sales")  
plt.xlabel("Advertising Expenditure (Lakhs)")  
plt.ylabel("Sales Revenue (Crores)")  
plt.legend()  
plt.grid(True)  
plt.show()  

# 8. Predict sales for a new advertising budget  
new_advertising = pd.DataFrame({"Advertising (Lakhs)": [65]})  
new_sales_prediction = model.predict(new_advertising)    

print("New advertising budget (Lakhs):", new_advertising.iloc[0, 0])  
print("Predicted sales revenue (Crores):", round(new_sales_prediction[0], 2))




##  Result
