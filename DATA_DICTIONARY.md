# Data Dictionary

This document describes the raw files and the main fields created inside `Ecommerce-sales-analysis.ipynb`.

## Data grain

Each row in the two sales files represents a **product line within an order**. An `Order_ID` can therefore appear more than once when an order contains multiple products. The two sales partitions have the same schema and are concatenated before cleaning.

## Sales files

Files: `sales_data_part1.csv` and `sales_data_part2.csv`

| Raw column | Cleaned name | Type | Description |
|---|---|---|---|
| `Order_ID` | `order_id` | string | Order identifier; may repeat across product lines. |
| `Date` | `date` | date | Transaction date in `YYYY-MM-DD` format. |
| `Customer_ID` | `customer_id` | string | Customer identifier used to connect sales with customer attributes. |
| `Country_Code` | `country_code` | category | Raw country label; contains multiple representations of Jordan and Lebanon. |
| `Channel` | `channel` | category | Raw sales channel, later standardized to `online`, `offline`, or `unknown`. |
| `Sales_person` | `sales_person` | category | Sales representative associated with the transaction line. |
| `Units_Sold` | `units_sold` | integer | Number of product units on the transaction line. |
| `Unit_Price` | `unit_price` | decimal | Unit price in the source data's country-specific monetary value. |
| `Product_Code` | `product_code` | category | Product identifier. |
| `Product` | `product` | category | Product name. |
| `Promotion_Flag` | `promotion_flag` | boolean | `1` when a promotion applies and `0` otherwise. |
| `Commission_Percent` | `commission_percent` | decimal | Sales commission rate expressed as a fraction, such as `0.03`. |

## Customer file

File: `customers.csv`

| Raw column | Cleaned name | Type | Description |
|---|---|---|---|
| `customer_id` | `customer_id` | string | Customer identifier used for joins. |
| `channel` | `channel` | category | Channel associated with the customer record. |
| `city` | `city` | category | Customer city. |
| `sector` | `sector` | category | Customer segment, such as individual or institutional sectors. |

The customer file contains **1,378 rows for 1,000 unique customer IDs**. Some IDs therefore have multiple records. Any new join or customer-level analysis should check the intended relationship and deduplicate or aggregate customer records when appropriate.

## Derived sales fields

| Field | Type | Definition |
|---|---|---|
| `country` | category | Standardized country name: `jordan` or `lebanon`. |
| `unit_price_usd` | decimal | Unit price converted using the country-specific rule implemented in the notebook. |
| `total_amount` | decimal | `units_sold × unit_price_usd`; transaction-line revenue used throughout the analysis. |
| `year` | integer | Calendar year extracted from `date`. |
| `month` | integer | Calendar month number extracted from `date`. |
| `weekday_name` | category | Weekday name extracted from `date`. |

## Cleaning rules

The notebook applies the following project-specific decisions:

1. Column names and selected text values are normalized to lowercase.
2. Equivalent channel labels are mapped to `online` or `offline`; missing channels become `unknown`.
3. Country-code variants are mapped to Jordan or Lebanon.
4. Fully duplicated sales rows are removed.
5. Zero-unit sales rows are treated as errors and changed to one unit.
6. Prices are converted to a common field using the conversion logic defined in the notebook.
7. The date is parsed before year, month, and weekday features are generated.

## Important cautions

- The 2025 data ends on July 10 and does not represent a complete year.
- Revenue comparisons depend on the notebook's currency-conversion assumptions.
- Product-line counts and unique-order counts answer different questions; use `order_id.nunique()` for unique orders.
- The findings are descriptive and do not establish causal relationships.

