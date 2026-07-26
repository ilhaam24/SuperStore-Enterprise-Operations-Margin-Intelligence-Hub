# SuperStore-Enterprise-Operations-Margin-Intelligence-Hub
An end-to-end business intelligence solution that transforms 51,000+ rows of raw, fragmented global retail data into an interconnected, executive-ready dashboard. This project bridges the gap between high-level financial health, granular product margin leaks, and supply chain fulfillment performance.

# Data-Collection
I used kaggle to find the appropiete dataset for my data analysis. The link for the dataset is given below:
"https://www.kaggle.com/datasets/laibaanwer/superstore-sales-dataset"

# Data-Cleaning
One of the most integral part of data analysis. The main challenge I face during the cleaning of this particular dataset is the formatting issue regarding "order_date" and "ship_date" column. To rectify this issue I used python. The code used for the purpose is given below: 

# Python-code-for-fixing-date-format

import pandas as pd

file_path = "C:\Users\wwwil\Downloads\SuperStoreOrders.csv"
df = pd.read_csv(file_path)

df['order_date'] = pd.to_datetime(df['order_date'], dayfirst=True, errors='coerce')
df['ship_date'] = pd.to_datetime(df['ship_date'], dayfirst=True, errors='coerce')

missing_orders = df['order_date'].isna().sum()
missing_ships = df['ship_date'].isna().sum()
print(f"Unparsed Order Dates: {missing_orders}")
print(f"Unparsed Ship Dates: {missing_ships}")

df['order_date'] = df['order_date'].dt.strftime('%Y-%m-%d')
df['ship_date'] = df['ship_date'].dt.strftime('%Y-%m-%d')

output_path = ""C:\Users\wwwil\Downloads\SuperStore_Production_Cleaned.xlsx""
df.to_csv(output_path, index=False)

print("\nSuccess!")

# Data-Visualization
I used PowerBI for Dashboard creation. Here is the dashboard: https://github.com/ilhaam24/SuperStore-Enterprise-Operations-Margin-Intelligence-Hub/blob/main/Final_SuperStore_Data_Visualization.pbix

# Dashboard-Architecture-&-Insights

## Tab 1: Global Executive Sales & Profitability
* **Focus:** High-level commercial health and urgency strain.
* **Key Visuals:** Global Geospatial Map, Advanced Market Slicer Drawer (Tiles), Top/Bottom Country Leaderboards, and Order Priority Donut Split.
* <img width="1317" height="737" alt="SuperStoreDashboardTAB1" src="https://github.com/user-attachments/assets/86205417-f624-4f78-ab2f-fcb9035ed5c8" />

## Tab 2: Product Performance & Pricing Deep-Dive
* **Focus:** Identifying margin leakage and promotional efficiency.
* **Key Visuals:** DAX-driven 80/20 Pareto combo chart, High-Density Margin Scatter Plot, and Color-Coded Category Discount Matrix.
* <img width="1317" height="739" alt="SuperStoreDashboardTAB2" src="https://github.com/user-attachments/assets/6f962a19-8dab-4389-9285-c10b660d15f8" />

## Tab 3: Supply Chain & Logistical Optimization
* **Focus:** Operational fulfillment efficiency and SLA risk management.
* **Key Visuals:** Speedometer SLA Gauge, Avg Days-to-Ship Column Split, Carrier Cost Burden Treemap, and a Live Red-Alert Exception Grid tracking delays > 6 days.
* <img width="1308" height="739" alt="SuperStoreDashboardTAB3" src="https://github.com/user-attachments/assets/98bf436d-be11-40a9-9f82-417178de9710" />

---

## 📈 Core Business Questions Answered
# 1. Margin Leaks: The Discount Threshold
The Answer: 20% is the critical breaking point.
The Insight:
Discounts in the Low Discount (1–20%) tier maintain healthy, positive margins while driving sales volume.
Once discounts cross into the Medium (21–50%) and High (>50%) tiers, unit margins collapse so severely that even massive increases in order volume cannot cover the financial loss.
Category Impact: Furniture and Technology suffer the worst—high-discount sales in these categories yield negative net profits (e.g., selling tables or copiers at 50% off creates losses exceeding $100+ per unit).

# 2. Logistical Risks: Systemic 6-Day SLA Violations
The Answer: Southeast Asia, Central Africa, and select LATAM (Latin America) territories.
The Insight:
While markets like North America and Western Europe maintain efficient average delivery times of 4.1 to 4.5 days, regions like Southeast Asia and Central Africa average 6.2 to 6.8 days to ship.
These specific regions account for over 35% of all late shipment alert rows in the entire dataset, signaling systemic regional carrier delays or customs bottlenecks rather than isolated fulfillment mistakes.

# 3. Revenue Drivers: The Core 20% (Pareto Cutoff)
The Answer: 4 out of 17 Sub-Categories (~23% of the product catalog): Phones, Copiers, Chairs, and Bookcases.
The Insight:
Out of 17 total sub-categories, just these 4 top-performing product lines drive 80% of global revenue.
Business Action: Inventory management teams must prioritize stock protection and supply chain resilience for these 4 sub-categories. A stockout in Phones or Chairs damages global cash flow far more severely than a stockout in long-tail items like Envelopes, Fasteners, or Labels.
