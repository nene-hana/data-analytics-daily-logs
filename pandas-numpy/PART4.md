# Pandas Basics 🐼: Column & Row Operations, Filtering, Sorting, and More

This  covers essential Pandas operations for data manipulation in Python. It includes selecting columns, renaming, removing, adding columns, sorting, filtering rows, applying multiple filters, and best practices.

## Selecting Columns

Select a single column as a Series:

```python
column_series = df['column_name']  # Returns a Series
```

Select multiple columns as a DataFrame:

```python
df_subset = df[['col1', 'col2']]  # Returns a DataFrame
```

## Getting Column Values as Numpy Array

```python
column_values = df['column_name'].values  # Returns NumPy array
```

## Renaming Columns

```python
df.rename(columns={'old_name': 'new_name'}, inplace=True)
```

- `inplace=True` modifies the original DataFrame.  
- Without `inplace`, it returns a new DataFrame with renamed columns.

## Removing Columns

Drop a single column:

```python
df.drop('column_name', axis=1, inplace=True)
```

Drop multiple columns:

```python
df.drop(['col1', 'col2'], axis=1, inplace=True)
```

- `axis=1` indicates column.  
- `axis=0` would indicate rows.

## Adding Columns

Add a new column using operations:

```python
df['new_column'] = df['col1'] + df['col2']
```

Add a column with a constant value:

```python
df['new_column'] = 'default_value'
```

## Sorting Values

Sort by a single column:

```python
df.sort_values(by='column_name', ascending=True, inplace=True)
```

Sort by multiple columns:

```python
df.sort_values(by=['col1', 'col2'], ascending=[True, False], inplace=True)
```

- `ascending=False` sorts descending.  
- Multiple columns can have different sort orders.

## Filtering Rows by Column Values

Filter rows with a single condition:

```python
filtered_df = df[df['column_name'] == 'value']
```

Filter rows with multiple conditions (AND):

```python
filtered_df = df[(df['col1'] > 10) & (df['col2'] == 'value')]
```

Filter rows with multiple conditions (OR):

```python
filtered_df = df[(df['col1'] > 10) | (df['col2'] == 'value')]
```

## Applying Multiple Filters

```python
filtered_df = df[(df['col1'] > 5) & (df['col2'] != 'value') & (df['col3'] < 100)]
```

- Each condition must be in parentheses.  
- Use `&` for AND, `|` for OR.

## conclusion

```python
import pandas as pd  # Always import Pandas before using
```

- Use `.copy()` to avoid modifying the original DataFrame.  
- Use `.head()`, `.tail()`, `.info()`, `.describe()` to inspect your data.  
- For large DataFrames, chain filters with parentheses for clarity and readability.  
- Always double-check column names to avoid KeyErrors.  
- Use `.values` to convert columns to NumPy arrays for faster numerical operations.  
- Use `.rename()` carefully to maintain column consistency in large projects.  
- Sorting and filtering can be combined to prepare data for analysis or visualization efficiently.
