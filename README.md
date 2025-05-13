# Analyzing International Education Costs with Pandas and Matplotlib

## Objective

This project demonstrates how to:

1. Load and analyze a dataset using the pandas library in Python.
2. Create and customize simple data visualizations using matplotlib and seaborn.

---

## Dataset

- **Name:** International Education Costs
- **Format:** CSV (`International_Education_Costs.csv`)
- **Columns Used (examples):** `Exchange_Rate`, `Living_Cost_Index`

---

## Project Structure

- **Script/Notebook:**  
  Contains all code for loading, cleaning, analyzing, and visualizing the dataset.
- **This README:**  
  Explains the workflow and findings.

---

## Steps Performed

### 1. Load and Explore the Dataset

- The dataset is loaded with exception-handling to catch file errors.
- The first 5 rows are displayed to inspect the data.
- The structure of the dataset (column names, types, and missing values) is explored.

### 2. Clean the Dataset

- Duplicates are removed.
- Outliers in the `Exchange_Rate` column are filtered to include only values between 0.9 and 100.

### 3. Basic Data Analysis

- Data types and missing values are checked using `info()` and `isnull().sum()`.

### 4. Data Visualization

- **Histogram:** Shows the distribution of `Exchange_Rate`.
- **Line Chart:** Shows `Living_Cost_Index` trend over time or by index.
- **Bar Chart:** Compares average `Exchange_Rate` by `Living_Cost_Index`.
- **Scatter Plot:** Visualizes the relationship between `Exchange_Rate` and `Living_Cost_Index`.

All plots are clearly labeled with titles and axis descriptions.

---

## How to Run This Project

1. Clone this repository or download the code and dataset.
2. Make sure you have Python and required libraries installed (`pandas`, `matplotlib`, `seaborn`).
3. Place your `International_Education_Costs.csv` file in the project directory.
4. Run the Jupyter notebook or Python script.  
   In your terminal or VS Code, you can run:
   ```bash
   pip install pandas matplotlib seaborn
   python your_script_name.py
   ```
   or open the `.ipynb` file in Jupyter.

---

## Example Code Overview

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Data Loading
try:
    df = pd.read_csv('International_Education_Costs.csv')
    print("Data loaded successfully!")
except FileNotFoundError:
    print("Error: The file was not found. Please check the filename and path.")
except Exception as e:
    print(f"An error occurred: {e}")

# Exploration
print(df.head())
print(df.info())
print(df.isnull().sum())

# Cleaning
df_clean = df.drop_duplicates()
df_clean = df_clean[(df_clean['Exchange_Rate'] <= 100) & (df_clean['Exchange_Rate'] >= 0.9)]

# Visualizations
# Histogram
plt.figure(figsize=(8, 5))
sns.histplot(df_clean['Exchange_Rate'], bins=10, kde=True)
plt.title("Distribution of Exchange Rates")
plt.xlabel("Exchange Rate")
plt.ylabel("Frequency")
plt.tight_layout()
plt.show()

# Line Chart
plt.figure(figsize=(10, 5))
plt.plot(range(len(df_clean)), df_clean['Living_Cost_Index'], marker='o', label='Living Cost Index')
plt.title('Living Cost Index Over Time')
plt.xlabel('Time Period')  
plt.ylabel('Living Cost Index') 
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Bar Chart
avg_exchange_rate = df_clean.groupby('Living_Cost_Index')['Exchange_Rate'].mean().reset_index()
plt.figure(figsize=(8, 5))
sns.barplot(data=avg_exchange_rate, x='Living_Cost_Index', y='Exchange_Rate')
plt.title('Average Exchange Rate by Living Cost Index')
plt.xlabel('Living Cost Index')
plt.ylabel('Average Exchange Rate')
plt.tight_layout()
plt.show()

# Scatter Plot
plt.figure(figsize=(8, 5))
sns.scatterplot(data=df_clean, x='Exchange_Rate', y='Living_Cost_Index')
plt.title('Exchange Rate vs Living Cost Index')
plt.xlabel('Exchange Rate')
plt.ylabel('Living Cost Index')
plt.tight_layout()
plt.show()
```

---

## Findings & Observations

- **Exchange Rate Distribution:** The data shows most exchange rates cluster within a given range.
- **Cost Trends:** The living cost index trends and its relation to exchange rates are visualized.
- **Category Comparison:** The bar chart gives an at-a-glance comparison of exchange rates by cost index.
- **Correlation:** The scatter plot helps spot any patterns between exchange rate and living cost.

---

## License

This project is for educational purposes.
