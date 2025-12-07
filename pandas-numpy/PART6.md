# Pandas `groupby()`

## What is `groupby`?

`groupby()` lets you take a DataFrame and split it into groups based on one or more columns.  
After splitting, you can apply operations (sum, mean, count, etc.) on each group, and then combine everything back into a single result.

Basic idea: **split → apply → combine**.

Syntax:

```python
df.groupby(by=..., as_index=True, sort=True)
```

`by` can be a single column or a list of columns.


---

## Simple grouping + aggregation

```python
import pandas as pd

data = {
    'Item': ['Cake', 'Cake', 'Bread', 'Pastry', 'Cake'],
    'Flavor': ['Chocolate', 'Vanilla', 'Whole Wheat', 'Strawberry', 'Chocolate'],
    'Price': [250, 220, 80, 120, 250]
}
df = pd.DataFrame(data)

# Sum of Price for each Item
df.groupby('Item')['Price'].sum()

# Count rows per group (counts non-null values)
df.groupby('Item').count()
```

To get multiple statistics at once:

```python
df.groupby('Item').agg(['sum', 'mean', 'count', 'min', 'max'])
```

Different functions for different columns:

```python
df.groupby('Item').agg({
    'Price': ['sum', 'mean'],
    'OtherCol': 'count'
})
```


---

## Grouping by multiple columns

```python
df.groupby(['ColumnA', 'ColumnB']).sum()
df.groupby(['ColumnA', ColumnB'])['SomeCol'].mean()
```

This groups by the combination of both column values.


---

## Iterating through groups or selecting a group

```python
grp = df.groupby('Item')

for name, group_df in grp:
    print(name)
    print(group_df)
```

Get a single group:

```python
grp.get_group('Cake')
```

If grouping by multiple columns, pass a tuple to `get_group()`.


---

## Advanced usage

### Multiple aggregations

```python
df.groupby('Item').agg({
    'Price': ['sum', 'mean', 'count', 'min', 'max']
})
```

Named aggregations (cleaner output):

```python
df.groupby('Item').agg(
    total_price=('Price', 'sum'),
    avg_price=('Price', 'mean'),
    count_price=('Price', 'count')
)
```


### Custom operations with `apply` or `transform`

Used when you want more control than built-in functions give.

Example: (sorting inside each group → cumulative results, etc.)
Use `apply()` or `transform()` depending on the shape of output you want.


---

## Combining `groupby` with sorting, merging, etc.

### Sorting inside groups

```python
df_sorted = df.sort_values(['GroupKey', 'ValueColumn'], ascending=False)
top3 = df_sorted.groupby('GroupKey').head(3)
```

Get the top N values inside each group:

```python
df.groupby('GroupKey')['ValueColumn'].nlargest(3)
```


### Merging groupby results with another DataFrame

```python
result = df1.groupby('Category')['Value'].mean()
final = pd.merge(result.reset_index(), df2, on='Category')
```


### Combining string values inside a group

```python
df.groupby('Hobby', as_index=False).agg({
    'Hobby': 'first',
    'Name': ', '.join
})
```


---

## Common mistakes & things to remember

- `.count()` counts non-null values in each column → not the number of rows.  
  Use `.size()` for pure row counts.
  
- Aggregations like `mean()` only work on numeric data.

- If results look messy, try adding `.reset_index()` to clean up the output.

---

## Quick Reference Table

| Task | Code |
|------|------|
| Sum per group | `df.groupby('col')['num'].sum()` |
| Multiple stats | `df.groupby('col').agg(['sum','mean','count'])` |
| Different stats per column | `df.groupby('col').agg({'num1':'sum','num2':'mean'})` |
| Group by two keys | `df.groupby(['col1','col2']).sum()` |
| Top N rows per group | `df.sort_values(['group','value'], ascending=False).groupby('group').head(n)` |
| Combine strings | `df.groupby('group')['name'].apply(', '.join).reset_index()` |
| Merge aggregated result | `agg = df.groupby('col').mean(); pd.merge(agg.reset_index(), other_df, on='col')` |

