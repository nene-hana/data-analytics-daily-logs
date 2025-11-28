# Pandas Indexing and Conditional Selection 🎍

## 1. Attribute Access (`df.column`)
In Python, object properties can be accessed using dot '.'. Pandas allows this for columns too.

**Example:**
```python
animal.species
reviews.country
```

**Limitations:**
- Works only if the column name has no spaces  
- Cannot be used for column names that conflict with method names  

---

## 2. Indexing Operator (`df['column']`)
This is the most reliable way to select columns.Unlike attribute access, the indexing operator can handle any column name—even those with spaces, symbols, or reserved keywords. It removes ambiguity and makes your code clear and predictable. This method mirrors how you access dictionary elements in Python, which makes it intuitive for most users. Because of its flexibility and consistency, it is the preferred method for selecting columns in real projects.

**Example:**
```python
reviews['country']
```

**Why it's preferred:**
- Works for any column name (spaces, special characters)  
- Avoids naming conflicts  

---

## 3. `loc[]` – Label-Based Indexing
`loc` selects rows and columns **by label**. `loc[]` is pandas’ dedicated tool for selecting rows and columns using **labels** rather than position numbers. This makes it ideal for working with datasets that have meaningful row indexes or when you want readable and explicit selections. `loc` supports slices, boolean filtering, and combinations of row/column labels, making it extremely powerful. If you want to filter data based on values (like selecting all rows where country = 'Italy'), `loc` is the correct approach. It gives full control and clarity when you want to select data based on real-world conditions.

### Examples
Select a row by its label:
```python
reviews.loc[0]
```

Select a specific row and column:
```python
reviews.loc[0, 'country']
```

Select multiple rows and columns:
```python
reviews.loc[[0, 5, 10], ['country', 'province']]
```

**loc supports:**
- Row ranges  
- Column ranges  
- Boolean filtering  
- Label-based indexing  

---

## 4. `iloc[]` – Position-Based Indexing
`iloc` selects data **by numerical position**, similar to list indexing in Python.While `loc` uses labels, `iloc` uses **integer positions**—just like list indexing in Python. It only accepts numbers, never labels. This method is useful when you need to grab rows by their fixed position in the DataFrame rather than by a label or condition. It is predictable and fast because it purely depends on numbers. Use `iloc` when you want to select the first 10 rows, the last 5 rows, or columns by numerical order. It’s especially helpful when working with data that doesn’t have meaningful row labels.

### Examples
Select the first row:
```python
reviews.iloc[0]
```

Select by row and column positions:
```python
reviews.iloc[0, 5]
```

Select multiple:
```python
reviews.iloc[[0, 1, 10], [0, 5, 6, 7]]
```

**Important:**  
`iloc` only accepts integers.

---

## 5. Conditional Selection
Conditional selection filters rows based on conditions.

### Examples
Rows where country is Italy:
```python
reviews.loc[reviews.country == 'Italy']
```

Multiple conditions:
```python
reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
```

**Common operators:**
- `==` equal  
- `!=` not equal  
- `>` greater than  
- `<` less than  
- `>=` greater or equal  
- `<=` less or equal  

---

## so in short 💡

| Method          | Use Case                           | Works With              |
|-----------------|-------------------------------------|--------------------------|
| `df.column`     | Quick simple access                 | Simple column names      |
| `df['column']`  | Most reliable column selection      | Any column name          |
| `loc[]`         | Label-based selection + conditions  | Row & column labels      |
| `iloc[]`        | Position-based selection            | Integer indexes          |

---
