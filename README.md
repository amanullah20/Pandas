<picture align="center">
  <source media="(prefers-color-scheme: dark)" srcset="https://pandas.pydata.org/static/img/pandas_white.svg">
  <img alt="Pandas Logo" src="https://pandas.pydata.org/static/img/pandas.svg">
</picture>


<h1 align='center'> Overview of Pandas</h1>

<h3 align='adjusted'>Pandas is a powerful, open-source data analysis and manipulation library built on top of NumPy. It is
widely used in data science, machine learning, and statistical analysis due to its ability to handle,
clean, and analyze data efficiently. Pandas provides high-level data structures and methods that make
working with structured data easy and intuitive.</h3>

### The two primary data structures provided by Pandas are : 
- 01 ` Series ` – a one-dimensional labeled array (like a column in a table).
- 02 `DataFrame` – a two-dimensional labeled data structure (like a table or a spreadsheet).

### Key Features of Pandas
#### 1. Data Structures
- `Series:` A one-dimensional labeled array. It can hold data of any type (integers, strings, floats,
etc.), and is similar to a list or an array, but with labels (indices).
-  `DataFrame:` A two-dimensional table, similar to a spreadsheet or SQL table, where data is
organized into rows and columns. It is the most commonly used structure in Pandas.

### 2. Handling Missing Data:
- Pandas provides robust support for handling missing data (represented as NaN in floatingpoint columns). You can easily detect, fill, or drop missing values in your dataset.
### 3. Data Alignment:
- Pandas aligns data based on labels, ensuring that operations between datasets (such as
addition or subtraction) are done in an aligned way. This simplifies many complex data
manipulation tasks.
### 4. Efficient Data Manipulation:
- Pandas provides built-in methods for reshaping, aggregating, merging, and grouping data. It
supports operations such as sorting, filtering, and applying functions to data.
### 5. Integration with Other Libraries:
- Pandas integrates well with NumPy, Matplotlib (for visualization), and SciPy (for scientific
computations). It also supports reading from and writing to many different file formats (CSV,
Excel, SQL, JSON, etc.).

<h1 align='center'>Core Data Structure</h1>

### 1. Series
A Series is essentially a column in a DataFrame. It is a one-dimensional array that can hold data of any
type, and each element is labeled with an index.
### Creating a Series:
 ```bash
import pandas as pd
s = pd.Series([1, 2, 3, 4])
print(s)

```

### Output
```bash
0 1
1 2
2 3
3 4
dtype: int64
```

You can also provide custom labels (index):
```bash
s = pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])
print(s)
```

### Output
```bash
a 1
b 2
c 3
d 4
dtype: int64

```

### 2. DataFrame
A DataFrame is a two-dimensional table with rows and columns. Each column is a Series, and the
rows are indexed by labels. A DataFrame can store different data types (e.g., integers, floats, strings) in
different columns.
#### Creating a DataFrame:
```bash
import pandas as pd
# Dictionary to create a DataFrame
data = {
'Name': ['Alice', 'Bob', 'Charlie'],
'Age': [24, 27, 22],
'Salary': [50000, 60000, 45000]
}
df = pd.DataFrame(data)
print(df)
```

### Output:
```bash
Name Age Salary
0 Alice 24 50000
1 Bob 27 60000
2 Charlie 22 45000
```
You can also read from various file formats (CSV, Excel, JSON, SQL, etc.):
```bash
# Reading from a CSV file
df = pd.read_csv('data.csv')
# Reading from an Excel file
df = pd.read_excel('data.xlsx')
```
### Key Operations on DataFrames
#### 1. Accessing Data
- By Column:
```bash
df['Name']
```
- By Row (using .loc and .iloc ):
```bash
df.loc[0] # Row with index 0 (label-based)
df.iloc[0] # Row at position 0 (integer-based)
```
- Accessing Subsets:
```bash
df[['Name', 'Age']] # Select specific columns
df.iloc[0:2, 1:3] # Select rows and columns by position
```

### 2. Filtering Data
#### Filtering rows based on conditions:
```bash
df[df['Age'] > 25] # Select rows where Age > 25
```
### 3. Sorting Data
#### Sort by column values:
```bash
df.sort_values(by='Age') # Sort by Age column
```
### 4. Grouping and Aggregating
#### Grouping data and performing aggregate operations like sum, mean, etc.
```bash
df.groupby('Name').agg({'Salary': 'mean'})
``` 
### 5. Handling Missing Data
#### Detect missing values:
```bash
df.isnull() # Returns a DataFrame of boolean values indicating missing data
```
### Fill missing values:
```bash
df.fillna(0) # Fill missing values with 0
```
### Drop missing values:
```bash
df.dropna() # Drop rows with missing values
```

### 6. Merging DataFrames
#### You can merge multiple DataFrames together based on common columns (similar to SQL joins):
```bash
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['A', 'B', 'C']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Age': [22, 23, 24]})
merged_df = pd.merge(df1, df2, on='ID', how='inner')
```
### 7. Reshaping Data
#### Pandas provides methods like .pivot() , .melt() , and .stack() for reshaping data.
```bash
df_pivot = df.pivot(index='Name', columns='Age', values='Salary')
```

### Advanced Topics
#### 1. Time Series
Pandas has powerful support for time series data, making it easy to handle time-based indices,
resample data, and perform rolling operations.
```bash
# Create a time series index
dates = pd.date_range('20210101', periods=6)
df_time_series = pd.DataFrame({'data': [1, 2, 3, 4, 5, 6]}, index=dates)
# Resample data (e.g., daily to monthly)
df_resampled = df_time_series.resample('M').sum()
```

### 2. Window Functions
#### Pandas allows applying rolling windows to perform statistical operations over a fixed window.
```bash
df['rolling_mean'] = df['Salary'].rolling(window=2).mean()
```
### 3. Multi-Index DataFrames
#### Pandas also supports multi-level indexing (hierarchical indexing), which allows for more complex data
structures.
```bash
arrays = [['A', 'A', 'B', 'B'], [1, 2, 1, 2]]
df_multi = pd.DataFrame({'Value': [10, 20, 30, 40]}, index=arrays)
```
### File I/O in Pandas
Pandas provides methods to read from and write to various file formats, making it an excellent for data wrangling tasks:
- CSV:
```bash
df.to_csv('file.csv') # Write to CSV
df = pd.read_csv('file.csv') # Read from CSV
``` 
- Excel:
```bash
df.to_excel('file.xlsx') # Write to Excel
df = pd.read_excel('file.xlsx') # Read from Excel
```
- SQL:
```bash
# Using SQLAlchemy to connect to a database
from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:')
df.to_sql('table_name', con=engine)
df_sql = pd.read_sql('SELECT * FROM table_name', con=engine)
```
JSON:
```bahs
df.to_json('file.json') # Write to JSON
df = pd.read_json('file.json') # Read from JSON
```

<h1 align=center >Summary</h1>
Pandas is one of the most widely-used libraries in data science and analytics due to its versatility and
rich feature set. With Pandas, you can:
- Efficiently manipulate and analyze data (e.g., filtering, grouping, merging, reshaping).
- Handle missing data seamlessly.
- Work with time series data.
- Perform statistical and rolling operations.
- Easily load and save data from multiple file formats (CSV, Excel, SQL, JSON, etc.).

##### For full documentation, examples, and advanced usage, you can always refer to the official Pandas documentation:
[Pandas Documents](https://pandas.pydata.org/pandas-docs/stable/)
