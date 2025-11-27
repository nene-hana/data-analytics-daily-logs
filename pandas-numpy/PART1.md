# Introduction to Pandas 🐼

Pandas is one of the most important Python libraries used in **data analytics**, **data cleaning**, and **data manipulation**.

To use pandas in Python, we must first import it:

```python
import pandas as pd
```

`pd` is just a short name  that makes it easier to type and call pandas functions.

---

## What is a DataFrame?

A **DataFrame** is the most commonly used object in pandas.  
It is similar to a **table** with:

- Rows  
- Columns  
- Labels  
- Data values  

You can imagine it like an Excel sheet inside Python.

![future accountant](https://github.com/user-attachments/assets/ae247c78-3fab-4262-af20-257a3fc8b3e5)


---

# Creating a DataFrame

There are multiple ways to create a DataFrame.  
Below are the two most common beginner-friendly methods.

---

## Method 1: Create a DataFrame from a Python dictionary

```python
df = pd.DataFrame({
    'AGE': [5, 7, 1],
    'YEAR': [2004, 2002, 2003]
})
```

### Explanation:
- `{}` is a Python dictionary.
- Each **key** becomes a **column name** (`AGE`, `YEAR`).
- Each **value list** becomes column data.

This creates a table like:

<img width="272" height="184" alt="image" src="https://github.com/user-attachments/assets/48b04302-48c3-4bdd-b54e-0b1d544eff0c" />

---

## Method 2: Create a DataFrame from a CSV file

```python
df = pd.read_csv('animal.csv')
```

### What is a CSV?

A **CSV** (Comma Separated Values) is a simple text file where:

- Each row is on a new line  
- Each value is separated by a **comma**

Example CSV:

```
Name,year,Type
JellyFish,5,Wild
Fox,3,Wild
Hamster,12,Pet
```

---

# Basic DataFrame Functions

These are essential beginner functions.

---

## 1. `df.shape`

```python
df.shape
```

Returns the size of the DataFrame:

```
(rows, columns)
```

Example:
```
(100, 5)
```
Meaning 100 rows and 5 columns.

---

## 2. `df.head()`

```python
df.head()
```

Shows the **first 5 rows** of the DataFrame.

To view more or fewer rows:

```python
df.head(10)   # first 10 rows
df.head(3)    # first 3 rows
```

---

# Summary

- `import pandas as pd` → import pandas  
- DataFrame = table-like structure  
- Create DataFrames using dictionary or CSV  
- `df.shape` → shows rows & columns  
- `df.head()` → previews first few rows  

These basics are needed before starting data cleaning or analysis. I keep my notes here, code files and notebooks are maintained in a separate repository [data-analytics-journey
](https://github.com/nene-hana/data-analytics-journey)


