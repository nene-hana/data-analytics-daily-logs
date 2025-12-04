# Summary Functions and Maps 
This is based on Kaggle Pandas course

---

# 📘 1. What Are Summary Functions?

Summary functions help you understand your dataset quickly.  
They **summarize** data: averages, minimum, maximum, etc.

### Common Summary Methods in Pandas

| Function | Description | Example |
|---------|-------------|---------|
| `df.mean()` | Average of values | `reviews.points.mean()` |
| `df.median()` | Middle value | `reviews.price.median()` |
| `df.min() / df.max()` | Minimum / Maximum | `reviews.points.max()` |
| `df.unique()` | Unique values in a Series | `reviews.country.unique()` |
| `df.nunique()` | Count of unique values | `reviews.taster_name.nunique()` |
| `df.describe()` | Summary statistics | `reviews.points.describe()` |
| `value_counts()` | Frequency of values | `reviews.country.value_counts()` |

---

# 📘 2. Summary on Categorical Data

Categorical columns often need special exploration.

### Unique Values
```python
reviews.country.unique()
```

### Frequency of Each Category
```python
reviews.country.value_counts()
```

### Describing Categorical Columns
```python
reviews.taster_name.describe()
```

This returns:
- count  
- number of unique values  
- most frequent value ("top")  
- frequency of that value ("freq")  

---

# 📘 3. Maps and Lambda Functions

Mapping means **transforming each value** with a function.

Used on **Series only**.

### Example: Subtracting the mean from each value
```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```

### Example: Checking if description contains a word
```python
reviews.description.map(lambda d: "fruity" in d.lower())
```

---

# 📘 4. Vectorized Operations (Preferred)

Pandas supports fast, vectorized operations.

Instead of:

```python
reviews.points.map(lambda p: p - reviews.points.mean())
```

Use:

```python
reviews.points - reviews.points.mean()
```

Vectorization is:
- faster  
- cleaner  
- more “pandas-style”  

---

# 📘 5. The `apply()` Function (Row or Column Wise)

`apply()` works on **DataFrames**.

Useful when the logic uses **multiple columns**.

### Example: Assigning star ratings
```python
def stars(row):
    if row.country == "Canada":
        return 3
    elif row.points >= 95:
        return 3
    elif row.points >= 85:
        return 2
    else:
        return 1

reviews.apply(stars, axis='columns')
```

Important:
- `axis='columns'` = apply the function on each **row**
- Avoid modifying rows in-place inside `apply()`
- Always **return** something

---

# 📘 6. When to Use What?

| Goal | Use |
|------|-----|
| Find averages, min, max | Summary functions |
| Count categories | `value_counts()` |
| Transform one column value-by-value | `map()` |
| Transform using multiple columns | `apply()` |
| Fast numeric operations | Vectorized operations |

---

# 📘 7. Practical Examples (Wine Reviews Dataset)

Assume:
```python
import pandas as pd
reviews = pd.read_csv("../input/wine-reviews/winemag-data_first150k.csv", index_col=0)
```

### Average price
```python
reviews.price.mean()
```

### Median points
```python
reviews.points.median()
```

### Countries with the most reviews
```python
reviews.country.value_counts()
```

### Create a “centered price” column
```python
reviews['price_centered'] = reviews.price - reviews.price.mean()
```

### Count how many descriptions contain "tropical"
```python
tropical = reviews.description.map(lambda d: "tropical" in d.lower())
tropical.sum()
```

---

# 📘 8. Best Practices

- Prefer **built-in summary functions** for speed.
- Prefer **vectorized operations** over `map()` or `apply()`.
- Use `map()` for single-column transformations.
- Use `apply()` only when row-level logic is required.
- Avoid modifying rows directly inside an `apply()` function—always return new values.

---

# ✔️ Final Takeaway

**Summary functions help you understand your data.  
Mapping and applying help you transform it.  
Vectorized operations are the fastest way to work with numeric columns.**

This lesson is about quickly analyzing and transforming data using pandas' most powerful tools.

