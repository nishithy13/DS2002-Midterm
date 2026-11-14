DS2002 Midterm Project — Walmart Hurricane Helene Analytics

Team: Iceman (Ishan Alla, Sid Luthra, Nishith)

Repository Files

- DS2002-Midterm/notebooks/walmart_hurricane_analysis.ipynb — Our main ETL and analysis notebook covering Questions 1–5.
- 2026-10-30 — Midterm Progress — Lab.ipynb — Checkpoint notebook from Week 2.
- 06-midterm-walmart/data/ — The raw data files provided for the project (walmart_transactions.csv, product_catalog.csv, store_locations.csv, distribution_centers.csv) and the SQLite database (inventory_and_sales.db).
- CHARTER.md — Our team charter and breakdown of who owned which questions.

How to Run the Notebook

1. Clone the repo (git clone https://github.com/nishithy13/DS2002-Midterm.git) or open DS2002-Midterm/notebooks/walmart_hurricane_analysis.ipynb directly in Google Colab or Jupyter.
2. Put the five data files from 06-midterm-walmart/data/ in your working data folder (or your local Downloads directory), and make sure you have pandas, matplotlib, and requests installed.
3. Hit Restart & Run All to run everything from top to bottom. For Question 3, the notebook pulls live hourly data from the Open-Meteo Historical Weather API (https://open-meteo.com) in America/New_York time for the 11 stores that have valid coordinates.

Summary of Key Findings

• Cleaning & Pipeline: We started with 25,562 raw transaction rows. After dropping 30 duplicate transaction IDs and 130 rows with negative quantities, we ended up with 25,402 valid rows (and 24,521 dated rows once we set aside 881 rows missing timestamps). We also mapped 60 messy store ID variants down to 12 actual Florida stores and standardized 37 raw category names into 10 clean categories.

• Q1 (7-Day Demand Surge Across Categories): Comparing the week right before the storm (Sept 19–25) to the previous week (Sept 12–18), Breakfast saw the biggest jump in average daily units at +242.2% (going from 110.1 to 376.9 units/day). Emergency supplies followed at +137.4% (424.0 to 1,006.4 units/day), along with Electronics (+124.2%), Entertainment (+107.5%), and Alcohol (+106.4%).

• Q2 (Pop-Tarts Consolidation): Strawberry Pop-Tarts were split across four different SKUs (PT-12, SKU#459812, POPTART-STRAW, and PT_STRAWBERRY). Grouping them together gave us 5,005 deduplicated units (compared to 5,006 raw rows and just 1,332 units if we had only looked at PT-12), with sales peaking at 678 units on September 25.

• Q3 (Weather API Correlation & Lag): We pulled hourly precipitation, wind speed, and surface pressure from Open-Meteo and aggregated them to daily numbers across the 11 stores with coordinates (FL-619 in Tallahassee didn't have lat/long data). Daily store sales had a weak positive correlation with max wind speed (r = 0.218) and slight negative correlations with surface pressure (r = -0.208) and precipitation (r = -0.215). Looking at composite weather severity, the correlation shifted from r = 0.083 on the same day to r = -0.163 at a 1-day lead and r = -0.242 at a 2-day lead, showing that shoppers stocked up before the worst weather actually hit.

• Q4 (Store & Region Patterns): Every store saw a sharp jump in 7-day unit volume, ranging from +99.9% at FL-078 (Gainesville) up to +123.4% at FL-710 (Pensacola), with no statistical outliers under the 1.5-IQR rule. Regionally, the East (+118.8%), Panhandle (+118.7%), and West (+111.7%) regions saw the largest spikes.

• Q5 (Signal vs. Artifact — Board Games & SQLite Check): Sales for the three Monopoly/board-game SKUs (BG-MONO, MONOPOLY-01, and GAME-MONO) jumped +143.8%, climbing from 320 units (Sept 12–18) to 780 units (Sept 19–25). Cross-checking our cleaned POS data against the SQLite daily_sales_summary and inventory_levels tables showed that the database lumps board games together with Roku sticks and playing cards under Entertainment. Because of that, restocking should target those specific board-game SKUs instead of scaling up the whole category.

Reflection

1. Data Quality Impact
One data quality issue we encountered was 30 duplicate transaction IDs and 60 inconsistent store ID spellings (for just 12 actual stores) in the 25,562 raw Walmart sales rows. This was important because having the same transaction counted multiple times—or dropping store rows that failed to match—could distort how much customers were actually buying. We cleaned the data by removing the 30 duplicate transaction IDs and 130 negative-quantity rows, leaving 25,402 valid transactions (and 24,521 dated rows after setting aside 881 rows missing timestamps) so that each valid sale was counted once. For Pop-Tarts alone, deduplicating changed the raw total from 5,006 units to 5,005 clean units, while standardizing the 37 raw category spellings into 10 clean categories prevented sales from splitting across duplicate category labels. This showed me how even small data quality issues can impact the final analysis when businesses use that information to make inventory decisions.

2. ETL Trade-offs
One important decision we made was how to standardize SKUs, especially for Strawberry Pop-Tarts. The dataset had four different SKUs (`PT-12`, `SKU#459812`, `POPTART-STRAW`, and `PT_STRAWBERRY`) representing variations of the same product, which made it difficult to understand overall demand. We decided to use the product catalog to identify related SKUs and combine them, which totaled 5,005 deduplicated units across September (peaking at 678 units on September 25). An alternative would have been to leave each SKU separate and analyze them individually, where the single largest SKU (`PT-12`) only had 1,332 units—undercounting family demand by 3.76x. Leaving them separate could be useful for checking which specific package sizes (`4-pack` vs. `6 pack`) were selling, but it made the overall demand surge look much smaller than it actually was. By combining the SKUs, we saw the bigger picture of customer purchasing behavior while noting that Walmart still needs SKU-level checks before ordering cases.

3. Pipeline Trust
I agree with the Walmart CDO that the biggest risk is the data pipeline rather than the model itself. Throughout this project, I realized that even if our analysis and calculations were correct, the results would not be trustworthy if the data going into them was inaccurate. The most fragile part of our pipeline was connecting data from different sources, especially when matching cleaned sales transactions with the product catalog (`0` unmatched SKUs) and Open-Meteo weather data across our 12 normalized stores. We had to make sure store IDs (`fl-412`, `FL_239`, `FL239` -> `FL-412`, `FL-239`) and local `America/New_York` dates were consistent across datasets, and we caught that store `FL-619` (Tallahassee) was missing latitude and longitude coordinates, leaving 11 stores with valid weather data. We also had to handle mixed timestamp formats (including 8-digit `YYYYMMDD` dates in SQLite) and 886 missing timestamps. Building explicit print checks at each merge showed me that pipeline validation is just as important as the final charts.

4. Business vs. Data
For Question 5, the biggest challenge was determining whether the +143.8% increase in Monopoly board-game sales (rising from 320 units in the September 12–18 baseline week to 780 units in the September 19–25 pre-event week across `BG-MONO`, `MONOPOLY-01`, and `GAME-MONO`) represented real customer demand or an artifact of the data. We compared POS transaction data with the SQLite `daily_sales_summary` and `inventory_levels` tables, and found that the SQLite summary grouped all `Entertainment` products together (reaching 2,113 units on September 24 by mixing board games with Roku streaming sticks and playing cards). From a business perspective, I would be cautious about recommending a massive inventory increase based on the broad Entertainment summary alone. Ordering too many board games could leave Walmart with excess stock after the hurricane, so I would recommend a smaller, targeted buffer specifically for the three catalog-verified Monopoly SKUs alongside larger pre-event restocking for `Breakfast` (+242.2%) and `Emergency` (+137.4%) in the East, Panhandle, and West regions. With more time, I would verify whether the SQLite inventory snapshots were logged before or after daily sales.

5. Team Collaboration
Each team member (Ishan, Sid, and Nishith) contributed to the project by dividing up the pipeline, weather API integration, and Questions 1–5 as outlined in our `CHARTER.md`. This allowed us to work efficiently and help each other debug issues, especially when reconciling file paths between local `~/Downloads` folders, Google Colab, and our GitHub folders (`06-midterm-walmart/` and `DS2002-Midterm/notebooks/`). Some of us focused on writing the regex and cleaning functions, while others focused on the Open-Meteo API calls, SQLite cross-checks, and connecting the results to Walmart’s inventory decisions. If we had another week, we would lock a single repository folder structure on Day 1 with our shared `find_input()` path loader and keep one designated notebook owner at a time so we do not spend extra time fixing path mismatches or duplicate notebook commits.
