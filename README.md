# DABM-Experiment-4-Multiple-Regression-Analysis-Fish-Dataset

## Aim
To perform Multiple Linear Regression on a dataset imported from a CSV file to analyze how multiple features together predict a dependent variable.

## Dataset
The dataset used for this experiment is `fish.csv` which contains real-world physical measurements of various fish species:
* **Independent Variables ($X$):**
  * `L`: Mean length derived from `Length1`, `Length2`, and `Length3`
  * `Height`: Vertical height of the fish
  * `Width`: Diagonal width of the fish
* **Dependent Variable ($Y$):**
  * `Weight`: Weight of the fish (in grams)

## Algorithm / Steps Followed
1. Import the required Python libraries (`numpy`, `pandas`, `matplotlib`, `scikit-learn`).
2. Load the fish dataset into a Pandas DataFrame using `pd.read_csv()`.
3. Display the dataset and inspect its columns.
4. Define the dependent ($Y$) and independent ($X$) variables.
5. Train the Multiple Linear Regression model using `LinearRegression()`.
6. Display the model coefficients (`model.coef_`), intercept (`model.intercept_`), and regression equation.
7. Predict target variable (`Weight`) values using `model.predict()`.
8. Evaluate model accuracy using the $R^2$ score (`r2_score()`).
9. Plot actual vs. predicted values for visual comparison.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation / Handling** | `pd.read_csv()` | Load the CSV dataset into a Pandas DataFrame |
| | `np.array()` / `pd.DataFrame()` | Create and manage numerical arrays and tabular data for regression |
| **Model Building (Scikit-learn)** | `LinearRegression()` | Initialize the Multiple Linear Regression model |
| | `model.fit()` | Train the regression model using multiple independent variables ($X$) and target ($Y$) |
| | `model.predict()` | Predict dependent variable values ($Y$) using the trained model |
| | `r2_score()` | Evaluate the accuracy of the regression model using the $R^2$ score |
| **Model Attributes** | `model.intercept_` | Retrieve the intercept (constant term) of the regression equation |
| | `model.coef_` | Retrieve the coefficients (slopes) for each independent variable |
| **Visualization (Matplotlib)** | `plt.plot()` | Plot actual and predicted weight values for comparison |
| | `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.legend()`, `plt.show()` | Configure titles, axis labels, legend, and display the plotted figure |

## Input 1
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score
from sklearn.model_selection import train_test_split

# Step 2: Calculate Mean Length
df['L'] = (df['Length1'] + df['Length2'] + df['Length3']) / 3

# Step 3: Select Independent and Dependent Variables
X = df[['L', 'Height', 'Width']]
Y = df['Weight']

# Step 4: Split Dataset
X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y, test_size=0.2, random_state=42
)

# Step 5: Train Multiple Linear Regression Model
model = LinearRegression()
model.fit(X_train, Y_train)

# Step 6: Display Coefficients and Intercept
print("\nIntercept:", model.intercept_)
print("Coefficients:", model.coef_)

# Regression Equation
print("\nRegression Equation:")
print(f"Weight = {model.intercept_:.2f} "
      f"+ ({model.coef_[0]:.2f} * L) "
      f"+ ({model.coef_[1]:.2f} * Height) "
      f"+ ({model.coef_[2]:.2f} * Width)")
```
## Output 1
```
Intercept: -411.71191786599957
Coefficients: [ 27.17519101  21.10608547 -46.84772752]

Regression Equation:
Weight = -411.71 + (27.18 * L) + (21.11 * Height) + (-46.85 * Width)
```
## Input 2
```
# Step 7: Predict Weight
Y_pred = model.predict(X_test)

print("\nActual vs Predicted:")
print(pd.DataFrame({
    'Actual Weight': Y_test.values,
    'Predicted Weight': Y_pred
}))
```
## Output 2
```
Actual vs Predicted:
    Actual Weight  Predicted Weight
0           622.3        572.715893
1            72.9         67.110028
2           117.7        186.207677
3          1893.2       1255.578210
4           358.8        393.115813
5           446.4        475.422323
6          1034.7        902.209621
7           226.0        269.341671
8            19.1        -54.659483
9           141.5        215.815797
10           76.1         87.145765
```
## Input 3
```
# Step 8: Evaluate Model
r2 = r2_score(Y_test, Y_pred)
print("\nR2 Score:", r2)
```
## Output 3
```
R2 Score: 0.8599170110482375
```

## Input 4
```
# Step 9: Visualize Actual vs Predicted Values
plt.figure(figsize=(8, 5))

plt.plot(Y_test.values, label='Actual Weight', marker='o')
plt.plot(Y_pred, label='Predicted Weight', marker='x')

plt.title('Multiple Regression - Fish Weight Prediction')
plt.xlabel('Test Samples')
plt.ylabel('Weight (grams)')
plt.legend()
plt.show()
```
## Output 4

<img width="704" height="470" alt="image" src="https://github.com/user-attachments/assets/1b93d2c9-e87f-4c22-946e-372031128cd7" />


## Result
Thus, Multiple Linear Regression was successfully implemented on the Fish dataset using Python. The model predicted fish weight based on length, height, and
