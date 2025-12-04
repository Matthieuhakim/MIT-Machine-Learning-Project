# MIT-Machine-Learning-Project

## Modeling Dataset

After carefully aggregating sources from pizza ingredients and prices, oil prices, daily sales record, ingredient proportions and prices, we have resulted in the following datasets for modelling:

## 1. `daily_sales.csv`

**Description:**  
Feature-engineered daily pizza sales dataset where each row represents a specific day and time bucket.
All same-day pizza sales columns are treated as targets.
The features include contextual variables, previous-day pizza demand, and 3-day rolling averages for each pizza type and time bucket.

**Columns:**

| Column                       | Description                                                                                          |
| ---------------------------- | ---------------------------------------------------------------------------------------------------- |
| `date`                       | Date of the sales record (DD/MM/YYYY)                                                                |
| `time_bucket`                | Time of day category (`Lunch`, `Afternoon`, `Dinner`) encoded as a categorical feature               |
| `oil_price`                  | Daily Brent oil price (USD per barrel)                                                               |
| `is_holiday`                 | Binary flag indicating whether the day is a public holiday (1 = holiday, 0 = not)                    |
| `<pizza>_<bucket>_yesterday` | Pizza sales for each pizza type and size during each time bucket on the previous day                 |
| `<pizza>_<bucket>_avg3`      | 3-day rolling average of pizza sales for each pizza type and bucket (excluding the current day)      |
| `<pizza_type>_<size>`        | **Target variables**: actual pizza sales for each pizza type and size during the current time bucket |

---

## 2. `ingredient_prices.csv`

**Description:**  
Contains the price per kilogram for each ingredient, useful for cost modeling and profitability calculations.

**Columns:**

| Column | Description |
|--------|-------------|
| `ingredient` | Name of the ingredient |
| `price_per_kg` | Price in USD per kilogram |

---

## 3. `pizza_ingredient_matrix.csv`

**Description:**  
Specifies the ingredient composition of each pizza type. Values indicate the quantity of each ingredient (in kilograms) required per pizza.

**Columns:**

| Column | Description |
|--------|-------------|
| `pizza_type_id` | Unique identifier for the pizza type |
| `pizza_name` | Human-readable pizza name |
| `category` | Pizza category (e.g., `Chicken`, `Vegetarian`) |
| `<ingredient columns>` | Amount (kg) of each ingredient used in the pizza |

---

## 4. `pizzas.csv`

**Description:**  
Contains pricing and size information for individual pizzas.

**Columns:**

| Column | Description |
|--------|-------------|
| `pizza_id` | Unique pizza ID combining type and size |
| `pizza_type_id` | Links to the pizza type in `pizza_ingredient_matrix.csv` |
| `size` | Pizza size (S, M, L, etc.) |
| `price` | Sale price in USD |

---

## Notes

- `daily_sales.csv` is the main modeling file; other files provide auxiliary information for cost, ingredient, and price-based feature engineering.  
- All dates in `daily_sales.csv` and `oil_price` are formatted as `DD/MM/YYYY`.  
- Missing oil prices in 2015 have been filled with the mean oil price.
- The `is_holiday` flag is based on US federal holidays for 2015.
- Each pizza column in `daily_sales.csv` follows the naming convention: `<pizza_type_id>_<size>`.
