# 🚀 BigMart Sales Analysis with PySpark on Databricks

This project showcases how to perform scalable data analysis using **PySpark** within **Databricks**, applying transformations, filtering, and saving processed results — all using cloud-native tools.

---

## 📌 Project Summary

This notebook performs end-to-end data operations on a retail sales dataset — including **data cleaning**, **transformation**, **filtering**, and **writing outputs** in different formats. The goal is to gain insights into sales performance and prepare data for downstream modeling or reporting.

---

## 📊 Dataset Overview

- **Source**: BigMart simulated retail sales data
- **Rows**: 8,000+
- **Key Columns**:
  - `Item_Identifier`, `Item_Weight`, `Item_MRP`, `Item_Type`
  - `Outlet_Type`, `Outlet_Establishment_Year`, `Item_Outlet_Sales`
  - Categorical: `Outlet_Size`, `Outlet_Location_Type`, `Item_Fat_Content`

---

## 🔄 Transformations Performed

| Transformation Task                       | Description |
|-------------------------------------------|-------------|
| 🚫 Dropped nulls or incomplete values     | Removed rows with missing `Item_Weight` or key fields |
| 🧬 Type Casting                           | Casted columns like `Item_Weight` to `DoubleType` |
| 📌 Conditional Filtering                  | Selected specific item types like `'Soft Drinks'` with conditions |
| ➕ Duplicates Added for Testing           | Created manual duplicate records to test deduplication logic |
| 🔁 Union of DataFrames                    | Appended new records using `.union()` |
| 🧹 Cleaned up inconsistent columns        | Normalized `Item_Fat_Content` categories |
| 📁 Saved output in Parquet + CSV formats | Used `.write()` with `mode('overwrite')` and `append` |

---

## 🛠️ Major PySpark Functions & Methods Used

| Function / Method             | Purpose |
|------------------------------|---------|
| `spark.read.format()`        | Load CSV/Parquet files |
| `df.printSchema()`           | Inspect DataFrame schema |
| `df.select()` / `df.filter()`| Filter and select columns |
| `col()`                      | Access column objects for expressions |
| `.cast('double')`            | Convert string to numeric types |
| `.union()`                   | Combine two DataFrames |
| `.withColumn()`              | Create or update a column |
| `.dropna()`                  | Drop rows with null values |
| `.write.format().save()`     | Export data to file system |
| `display()`                  | Show results visually in Databricks |

---

## 🧪 Sample Code Snippets

### ➤ Filter with Casting
```python
from pyspark.sql.functions import col

df.filter(
    (col('Item_Type') == 'Soft Drinks') &
    (col('Item_Weight').cast('double') < 10)
).display()
