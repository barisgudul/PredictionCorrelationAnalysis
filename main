# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.impute import SimpleImputer
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# Load the dataset and fill missing values with column means
dataset = pd.read_csv("msleep.csv")
subset = dataset.iloc[:, 6:11].values  # Select the columns with missing values
imputer = SimpleImputer(missing_values=np.nan, strategy="mean")
imputer.fit(subset)
subset = imputer.transform(subset)
dataset.iloc[:, 6:11] = subset  # Replace the original data with imputed values

# Set the independent (X) and dependent (y) variables
X = dataset.iloc[:, 6:11].values  # Features: sleep_rem, sleep_cycle, awake, brainwt, bodywt
y = dataset.iloc[:, 5:6].values  # Target: sleep_total

# Split the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Create and train the Linear Regression model
regressor = LinearRegression()
regressor.fit(X_train, y_train)

# Make predictions on the test data
y_pred = regressor.predict(X_test)

# Create a DataFrame for the test results
test_results = pd.DataFrame(X_test, columns=dataset.columns[6:11])
test_results["actual_sleep_total"] = y_test
test_results["predicted_sleep_total"] = y_pred

# Plot a scatter plot and regression line for Actual vs Predicted Sleep Total
plt.figure(figsize=(15, 8))

# Scatter plot
sns.scatterplot(
    x=test_results["actual_sleep_total"], 
    y=test_results["predicted_sleep_total"], 
    label="Predicted vs Actual", color="blue"
)

# Regression line
sns.lineplot(
    x=test_results["actual_sleep_total"], 
    y=test_results["predicted_sleep_total"], 
    color="red", label="Regression Line", linestyle="-"
)

# Set plot title and labels
plt.title("Actual vs Predicted Sleep Total")
plt.xlabel("Actual Sleep Total")
plt.ylabel("Predicted Sleep Total")
plt.legend()

# Display the plot
plt.show()
