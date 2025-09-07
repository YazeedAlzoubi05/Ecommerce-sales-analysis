# Sales Data Analytics Project  

## Project Overview  
This project analyzes transactional sales data from a multinational e-commerce company specializing in electronics , operating across Jordan and Lebanon from 2021 to 2025.  
The dataset covers multiple sales channels (online and physical stores) and includes details about orders, products, customers, sales representatives, and promotions.  

The goal of this project was to clean, transform, and analyze the raw sales data to uncover insights into sales performance, customer segmentation, pricing, promotions, and market trends.  


--

## Workflow  

### 1. Data Loading  
- Imported the raw CSV files: `sales_data_part1.csv`, `sales_data_part2.csv`, and `customers.csv`.  
- Concatenated sales datasets into a single DataFrame.  

### 2. Data Cleaning  
- Renamed all columns to `snake_case`.  
- Standardized text columns (lowercased, stripped spaces).  
- Fixed inconsistent `channel` values (mapped website/online → online, in-store/offline → offline).  
- Replaced missing/invalid channel values with `unknown`.  
- Removed duplicate records (kept first occurrence).  

### 3. Feature Engineering  
- Standardized `country_code` into full country names.  
- Converted prices to USD (`unit_price_usd`), with exchange rates for Jordan.  
- Created a discount column (`discount_pct`) applying 10% for orders with more than 5 units.  
- Calculated `total_amount` after discount.  
- Added `commission_amount` based on salesperson commission.  
- Extracted date components (`year`, `month`, `weekday_name`).  
- Classified sales volume (`High`, `Medium`, `Low`).  
- Segmented customers (Loyal, Premium, Standard, One-time).  

### 4. Analysis and Insights  
- Counted transactions by channel and product.  
- Analyzed pricing (average, min, max unit prices).  
- Measured discount usage and promotion performance.  
- Segmented customers and counted each group.  
- Checked weekly sales patterns (e.g., which weekdays had highest sales in 2024).  
- Identified weak channel–country combinations for possible closure.  
- Analyzed which products are sold together most often.  
- Compared weekday sales between Jordan and Lebanon.  
- Found top-performing salespeople by year.  
- Calculated total commissions per salesperson (highest vs lowest earners).  
- Computed Year-over-Year sales growth for each country.  
- Created monthly product summaries (revenue, transactions, units sold).  
- Tracked 2024 monthly sales trends for specific products.  
- Measured the number of promotion periods and products involved.  

### 5. Visualizations  
- Bar chart of total commissions per salesperson.  
- Yearly sales trends by country.  
- Monthly product trends (example: laptops in 2024).  
- Heatmaps and comparison charts for weekday sales.  
- Other plots for customer segmentation and promotions.  

---

## Key Findings  
- Some sales channels underperform consistently and could be closed to reduce costs.  
- Customer segmentation shows clear loyalty tiers, with a small group of high-value repeat customers.  
- Sales patterns vary by country and weekday, important for planning promotions.  
- Certain products sell well in bundles, which can guide cross-selling strategies.  
- Promotions had mixed results: some boosted sales, others had little to no impact.  
- Top salespeople contribute disproportionately to total sales and commissions.  

---

## Tools Used  
- Python (pandas, numpy, matplotlib)  
- Jupyter Notebook for coding and analysis  
- CSV data files as the main input  
