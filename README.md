# Checking_dataframe_missing_value
This script demonstrates how to handle missing values in a dataset, calculate averages, and update specific columns based on groupings. The dataset used is the Cars93_miss.csv file, which contains data about various car models, including some missing values.

## Sample Code

```python
import pandas as pd
url = 'https://raw.githubusercontent.com/selva86/datasets/master/Cars93_miss.csv'
df = pd.read_csv(url)

# Check for missing values
missing_values = df.isnull().sum()
print("Number of missing values in each column:")
print(missing_values)

max_missing = missing_values.max()
print("\nMaximum number of missing values in any column:", max_missing)

# Replace missing values with mean for numeric columns
numeric_cols = df.select_dtypes(include='number').columns
df[numeric_cols] = df[numeric_cols].fillna(df[numeric_cols].mean())

# Calculate average price by manufacturer
avg_price_by_manufacturer = df.groupby('Manufacturer')['Price'].mean()
print("\nAverage price of different manufacturers:")
print(avg_price_by_manufacturer)

# Replace missing values in 'Price' column with mean depending on manufacturer
df['price'] = df.groupby('Manufacturer')['Price'].transform(lambda x: x.fillna(x.mean()))

# Display the updated DataFrame
print("\nUpdated DataFrame:")
print(df.head())
