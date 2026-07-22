# SuperStore-Enterprise-Operations-Margin-Intelligence-Hub
An end-to-end business intelligence solution that transforms 51,000+ rows of raw, fragmented global retail data into an interconnected, executive-ready dashboard. This project bridges the gap between high-level financial health, granular product margin leaks, and supply chain fulfillment performance.

# Data-Collection
I used kaggle to find the appropiete dataset for my data analysis. The link for the dataset is given below:
"https://www.kaggle.com/datasets/laibaanwer/superstore-sales-dataset"

# Data-Cleaning
One of the most integral part of data analysis. The main challenge I face during the cleaning of this particular dataset is the formatting issue regarding "order_date" and "ship_date" column. To rectify this issue I used python. The code used for the purpose is given below: 

# Python-code-for-fixing-data-format

import pandas as pd

# 1. Load the ORIGINAL raw dataset
file_path = "SuperStoreOrders.csv"
df = pd.read_csv(file_path)

print("--- Re-Parsing Dates Correctly ---")

# 2. Use dayfirst=True to force Pandas to read DD/MM/YYYY correctly
# This tells Pandas that if it sees "02/05/2011", it is May 2nd, NOT February 5th
df['order_date'] = pd.to_datetime(df['order_date'], dayfirst=True, errors='coerce')
df['ship_date'] = pd.to_datetime(df['ship_date'], dayfirst=True, errors='coerce')

# 3. Quick validation check to ensure no dates were corrupted into NaT
missing_orders = df['order_date'].isna().sum()
missing_ships = df['ship_date'].isna().sum()
print(f"Unparsed Order Dates: {missing_orders}")
print(f"Unparsed Ship Dates: {missing_ships}")

# 4. Export into the clean YYYY-MM-DD standard format for Power BI
df['order_date'] = df['order_date'].dt.strftime('%Y-%m-%d')
df['ship_date'] = df['ship_date'].dt.strftime('%Y-%m-%d')

# 5. Save and overwrite the Step 1 file
output_path = ""C:\Users\wwwil\Downloads\SuperStore_Production_Cleaned.xlsx""
df.to_csv(output_path, index=False)

print("\nSuccess!")

# END-of-the-code

I also added a column "days_to_ship", which will be used for data visualization later. 

#Data-Visualization
I used PowerBI for Dashboard creation.

#Dashboard-Architecture-&-Insights

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
**1. Margin Leaks:** At what exact discount threshold does promotional volume fail to compensate for price cuts?
= Margin Leaks: **The Discount Threshold
20% is the critical breaking point.

The Insight: Discounts in the Low Discount (1–20%) tier maintain healthy, positive margins while driving sales volume.
Once discounts cross into the Medium (21–50%) and High (>50%) tiers, unit margins collapse so severely that even massive increases in order volume cannot cover the financial loss.
Category Impact: Furniture and Technology suffer the worst—high-discount sales in these categories yield negative net profits (e.g., selling tables or copiers at 50% off creates losses exceeding $100+ per unit).

2. **Logistical Risks:** Which global regions face systemic bottlenecks where delivery windows violate our standard 6-day SLA?
= Southeast Asia, Central Africa, and select LATAM (Latin America) territories.
The Insight:
While markets like North America and Western Europe maintain efficient average delivery times of 4.1 to 4.5 days, regions like Southeast Asia and Central Africa average 6.2 to 6.8 days to ship.

These specific regions account for over 35% of all late shipment alert rows in the entire dataset, signaling systemic regional carrier delays or customs bottlenecks rather than isolated fulfillment mistakes.
3. **Revenue Drivers:** Which 20% of our product portfolio requires strict inventory protection to secure 80% of global cash flow?
