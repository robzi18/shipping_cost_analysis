
## The Data

All files are in the `data/` directory.

### `orders.csv` (~18,009 rows)

Each row represents one customer order.

| Column | Description |
|---|---|
| `order_id` | Unique order identifier (integer) |
| `order_date` | Timestamp of the order (YYYY-MM-DD HH:MM) |
| `customer_id` | Customer identifier (e.g., C00001) |
| `channel` | Sales channel: `web`, `mobile_app`, or `marketplace` |
| `region` | Geographic region: North, South, East, West, Central |
| `order_total` | Total value of the order in € |
| `shipping_cost` | Shipping charged to the customer: €5.95 or €0.00 |
| `num_items` | Number of line items in the order |

### `order_lines.csv` (~48,205 rows)

Each row represents one product line within an order.

| Column | Description |
|---|---|
| `line_id` | Unique line item identifier |
| `order_id` | References `orders.csv` |
| `product_id` | References `products.csv` |
| `product_name` | Name of the product |
| `category` | Product category |
| `quantity` | Number of units ordered |
| `unit_price` | Price per unit at time of sale (€) |
| `line_total` | Total for this line: `quantity × unit_price` |

### `products.csv` (150 products)

The product catalog.

| Column | Description |
|---|---|
| `product_id` | Unique product identifier |
| `product_name` | Product name |
| `category` | One of 6 categories |
| `unit_price` | Catalog price per unit (€) — note: `order_lines` has the actual transaction price |
| `unit_cost` | Cost price per unit (€) — needed for margin calculations |

The six product categories are: Electronics, Books, Beauty & Health, Clothing & Accessories, Sports & Outdoors, and Home & Kitchen (25 products each).
