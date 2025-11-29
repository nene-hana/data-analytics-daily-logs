**Selecting Rows & Columns in Pandas**

## 1. Selecting Multiple Columns
To select more than one column, pass a list of column names inside `[]`.

```python
reviews[['country', 'province', 'points']]
```

To reorder columns:
```python
reviews[['points', 'country']]
```

---

## 2. Selecting Rows by Number Range (Slice)
This uses **iloc** because slicing uses positions.

```python
reviews.iloc[0:10]
```

This selects rows 0 to 9.

To select the first 100 rows:
```python
reviews.iloc[:100]
```

To select the last 5 rows:
```python
reviews.iloc[-5:]
```

---

## 3. Selecting Columns by Number Range (Slice)
```python
reviews.iloc[:, 0:3]
```

Explanation:
- `:` before comma → all rows  
- `0:3` after comma → columns from index 0 to 2  

---

## 4. Selecting Rows by Label Range (loc slicing)
loc slicing **includes the end value**, unlike Python lists.

```python
reviews.loc[10:20]
```

This returns rows 10 through 20.

---

## 5. Selecting by Conditions with `isin()`
Use `isin()` for checking if a value belongs to a list.

### Example: wines from multiple countries
```python
reviews.loc[reviews.country.isin(['Italy', 'France', 'US'])]
```

### Example: remove rows with certain countries
```python
reviews.loc[~reviews.country.isin(['Spain', 'Argentina'])]
```

`~` means NOT.

---

## 6. Selecting by Range with `between()`
Check if values fall between two numbers.

Example: wines with points between 85 and 90:
```python
reviews.loc[reviews.points.between(85, 90)]
```

Inclusive by default (85 and 90 included).

---

## 7. Combining Multiple Column Filters
Example: Italian wines with 90+ points:
```python
reviews.loc[
    (reviews.country == 'Italy') &
    (reviews.points >= 90)
]
```

Example: wines from US OR Italy:
```python
reviews.loc[
    (reviews.country == 'US') |
    (reviews.country == 'Italy')
]
```

`&` = and  
`|` = or  
`~` = not  

---

## 8. Filtering Rows with Text Matching (`str.contains`)
Example: check if a description contains the word 'fruity':
```python
reviews.loc[reviews.description.str.contains('fruity', case=False)]
```

`case=False` ignores capitalization.

---

## 9. Selecting Unique Values
To see all unique countries:
```python
reviews['country'].unique()
```

To count unique values:
```python
reviews['country'].nunique()
```

---

## 10. Selecting Rows with Null / Not Null
Rows with missing values:
```python
reviews.loc[reviews.country.isnull()]
```

Rows without missing values:
```python
reviews.loc[reviews.country.notnull()]
```

---

## Summary Table

| Operation | Method |
|----------|--------|
| Select multiple columns | `df[['col1','col2']]` |
| Select rows by position | `df.iloc[start:end]` |
| Select rows by label | `df.loc[start:end]` |
| Select by value list | `df.column.isin([...])` |
| Exclude values | `~df.column.isin([...])` |
| Select by numeric range | `df.column.between(a, b)` |
| Text filtering | `df.column.str.contains()` |
| Null values | `df.column.isnull()` |
| Not-null values | `df.column.notnull()` |

---
