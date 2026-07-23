# Shipping Cost Analysis — Did Free Shipping Increase Profit?

*Conclusion: Yes — free shipping increased profitability.*

## Business Question

A mid-sized European e-commerce company introduced **free shipping on orders above €50** starting July 2024. Before that, every order carried a flat fee of **€5.95**. The finance team raised a concern:

> Did free shipping actually improve profitability, or did the company simply give away delivery income?

This project analyses order, product, and sales data from **January to September 2024** to answer that question with a data-backed recommendation.

---

## Project Structure

```
shipping_cost_analysis_project/
│
├── data/
│   ├── raw/
│   │   ├── orders.csv          # 18,009 customer orders
│   │   ├── order_lines.csv     # ~48,205 line items
│   │   └── products.csv        # 150 products across 6 categories
│   └── processed/
│       └── cleaned_merged_all.csv   # Cleaned and merged output
│
├── notebooks/
│   └── 01_data_cleaning_SC.ipynb   # Full analysis notebook
│
├── ASSIGNMENT.md
├── DATA_SPECS.md
├── HINTS.md
└── README.md
```

---

## Data Overview

| Table | Rows | Description |
|---|---|---|
| `orders.csv` | ~18,009 | One row per customer order |
| `order_lines.csv` | ~48,205 | One row per product line within an order |
| `products.csv` | 150 | Product catalog with cost prices |

The dataset covers two periods:
- **Before** (Jan – Jun 2024): flat €5.95 shipping on all orders
- **Promotion** (Jul – Sep 2024): free shipping on orders above €50

---

## Methodology

### 1. Load & Inspect
- Loaded all three CSVs and verified row counts, column types, and memory usage
- Identified data quality issues before any transformation

### 2. Clean
| Issue | Action |
|---|---|
| 452 malformed rows in `order_lines` (9 columns instead of 8) | Dropped |
| 220 duplicate `line_id` rows in `order_lines` | Verified as exact full-row duplicates (same product, quantity, price) before dropping |
| Missing `shipping_cost` values | Filled using business rules (€5.95 before July; €0 for orders > €50 in promo) |
| Missing `unit_price` and `line_total` in order lines (927 rows) | Back-calculated from `order_total - known_line_totals` (confirmed `order_total` reflects merchandise value only, not shipping) |
| `unit_cost` stored with comma as decimal separator (`18,50`) | Replaced comma with period before casting to float |

### 3. Enrich
- Merged all three tables on `order_id` and `product_id`
- Engineered `shipping_promotion_period` label (`before` / `on_promotion`)
- Calculated `profit_margin = (unit_price - unit_cost) × quantity` per line item
- Classified orders into spending tiers using `pd.cut()`


### 4. Analyse
Key questions addressed:
- Order volume change before vs. during promotion
- Average order value and spending behaviour change
- Total revenue and profit margin comparison
- Net promotion profit (revenue − product cost − absorbed shipping)
- Regional and channel breakdown
- Category-level profit contribution

### 5. Conclude
Findings translated into a business recommendation with caveats.

---

## Key Findings

| Metric | Result |
|---|---|
| Order volume during promotion | 59.4% of the full 6-month before period's order count — reached in just 3 months |
| Revenue during promotion | 69.7% of the before period's revenue — reached in just 3 months |
| Profit margin during promotion | 69.2% of the before period's profit — reached in just 3 months |
| Shipping cost absorbed by company (orders > €50) | €36,610.35 |
| Net promotion profit (orders > €50) | €457,274.91 |

Every region posted a higher monthly profit run-rate during the promotion. The promotion generated significantly more revenue and profit per month than the before period, and the absorbed shipping cost was comfortably covered by the increase in sales volume and order values.

---

## Tools & Libraries

- **Python 3** — core language
- **pandas** — data loading, cleaning, transformation, analysis
- **NumPy** — vectorised calculations and conditional assignment
- **Matplotlib** — visualisation

---

## How to Run

1. Clone or download the project folder
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib duckdb jupyter
   ```
3. Open the notebook:
   ```bash
   jupyter notebook notebooks/01_data_cleaning_SC.ipynb
   ```
4. Run all cells from top to bottom

> The notebook is designed to be run sequentially. All cleaning steps must complete before the analysis cells.

---

## Assumptions & Caveats

- Only Jan–Sep 2024 data is available — no full-year baseline for seasonal comparison
- The before period is 6 months; the promotion period is 3 months — all comparisons account for this time difference
- The promotion period happened during the pick summer season, maybe the increase in volume of orders come from that.
- 452 malformed rows and 220 duplicate line items were dropped; if these were non-random, results may be slightly biased
- `unit_cost` values were stored with a European decimal comma — corrected to standard float format
- The net promotion profit calculation covers only qualifying orders (> €50) where shipping was waived
