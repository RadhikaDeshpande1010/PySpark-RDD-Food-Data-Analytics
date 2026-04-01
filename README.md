# 🥕 PySpark RDD — Food Data Analytics

Hands-on PySpark RDD project applying core transformation operations — `map`, `filter`, and `distinct` — on a structured CSV food dataset. Covers 20 analytical exercises across string manipulation, key-value pair creation, calorie arithmetic, and category/colour-based filtering.

---

## Repository Structure

```
pyspark-rdd-food-data-analytics/
│
├── pyspark_rdd_food_data_analytics.ipynb   # Main notebook (20 RDD exercises)
├── food_data.csv                           # Source dataset (20 food items)
└── README.md
```

---

## Dataset Schema

| Column     | Type   | Description                          |
|------------|--------|--------------------------------------|
| FoodName   | String | Name of the food item                |
| Category   | String | Food group (Fruit, Dairy, Snack, …)  |
| Color      | String | Primary colour of the food item      |
| Calories   | Int    | Calorie count per serving            |

**Sample rows:**
```
Apple,Fruit,Red,95
Banana,Fruit,Yellow,105
Carrot,Vegetable,Orange,45
Chocolate,Snack,Brown,210
```

---

## Analysis Covered

| # | Operation | Description |
|---|-----------|-------------|
| 1 | `map` | Extract food names from each row |
| 2 | `map` | Convert food names to lowercase |
| 3 | `map` | Convert food names to uppercase |
| 4 | `map` | Extract and cast calorie values to integer |
| 5 | `map` | Create `(FoodName, Calories)` key-value pairs |
| 6 | `map` | Append `_FOOD` suffix to every food name |
| 7 | `map` + `distinct` | Create distinct `(Category, 1)` key-value pairs |
| 8 | `map` | Multiply each calorie value by 2 |
| 9 | `map` | Create `(Color, Calories)` key-value pairs |
| 10 | `map` | Add 10 calories to each food item |
| 11 | `filter` | Food items where calories > 100 |
| 12 | `filter` | Food items from the `Fruit` category |
| 13 | `filter` | Food items where color is `Green` |
| 14 | `filter` | Food names starting with the letter `B` |
| 15 | `filter` | Food items where calories < 80 |
| 16 | `filter` | Food items from the `Dairy` category |
| 17 | `filter` | Food items where color is `White` |
| 18 | `filter` | Food items where calories are between 90 and 120 |
| 19 | `filter` | Food items from the `Snack` category |
| 20 | `filter` | Food items where name length > 6 characters |

---

## Getting Started

### Prerequisites

- Python 3.8+
- Java 8 or Java 11 (required by PySpark)
- PySpark

### Installation

```bash
pip install pyspark
```

### Run on Google Colab

1. Open the notebook in [Google Colab](https://colab.research.google.com/)
2. Upload `food_data.csv` to `/content/sample_data/`
3. Run all cells in order

---

## Key Concepts Demonstrated

**Chained map transformations**
```python
food_names = food_rdd.map(lambda x: x.split(",")).map(lambda x: x[0])
food_names_uppercase = food_names.map(lambda x: x.upper())
```

**Key-value pair creation**
```python
food_name_calories = food_rdd.map(lambda x: x.split(",")).map(lambda x: (x[0], int(x[3])))
```

**Multi-step filter chains (parenthesised style)**
```python
high_calorie_foods = (
    food_rdd
    .map(lambda x: x.split(","))
    .map(lambda x: (x[0], x[3]))
    .filter(lambda x: int(x[1]) > 100)
)
```

**Range filtering**
```python
mid_calorie_foods = (
    food_rdd
    .map(lambda x: x.split(","))
    .map(lambda x: (x[0], x[3]))
    .filter(lambda x: 90 < int(x[1]) < 120)
)
```

**Distinct categories**
```python
distinct_categories = food_rdd.map(lambda x: x.split(",")).map(lambda x: (x[1], 1)).distinct()
```

---

## Technologies Used

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

---

*Built by **Radhika Deshpande** · PySpark RDD transformations on food analytics data*
