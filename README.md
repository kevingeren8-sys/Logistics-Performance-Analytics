# Logistics Performance Analytics

An exploratory analysis of logistics operations: how clean the data is, how well deliveries perform, and what drives trip duration and revenue.

Individual coursework project (analytics course, BINUS University, 2026).

## Key findings

- **Delivery is almost always on time (99.99%), and the 7 late trips are all on one route, RTE00017.** That points to a focused route investigation, not a system-wide response.
- **Refrigerated and dry van loads earn almost the same average revenue** (about $3,072 vs $3,074 per load, a 50.3% / 49.7% split of trips), even though their operating costs are likely very different. Pricing for refrigerated loads is worth reviewing against actual cost.
- **Distance explains most of trip duration.** Pearson r between distance and duration is 0.988, and a simple OLS model has R² = 0.9766 with a mean absolute error of 1.65 hours. Each extra 100 miles adds roughly 1.7 hours.

## Data

Four related tables: `loads`, `trips`, `routes` and `customers`. After cleaning and joining them, the master table has 85,410 trips and 43 columns.

The CSV files are not included in this repository. [Add where the data came from and how to get it.]

## Approach

1. **Data quality checks.** Missing values, plus a logical consistency check on implied speed (distance divided by duration) to catch impossible trips: faster than 85 mph, slower than 10 mph, or zero or negative duration. Implied speed stayed within a plausible range, so no trips were dropped.
2. **Cleaning.** 5,066 missing fleet identifiers (driver, truck, trailer) were filled with "Unknown" so those trips stayed in the analysis.
3. **Integration.** Loads joined to trips, then routes, then customers, into one master table.
4. **Analysis.** Descriptive statistics, segment comparisons (load type, customer segment), Pearson correlation, and an OLS regression of duration on distance with residual checks.

## Limitations

- Only 7 of 85,410 trips were late, so the data cannot support a reliable model for predicting delays.
- There are no external factors in the data (weather, traffic, driver hours), so the duration model only captures distance.
- Revenue was compared across segments without cost data, so the pricing finding is a question to investigate, not a conclusion.

## Tools

Python, pandas, NumPy, SciPy, Matplotlib, Seaborn, Plotly. The notebook was written in Google Colab.

## Run it

1. Put `loads.csv`, `trips.csv`, `routes.csv` and `customers.csv` where the notebook loads them.
2. Open the notebook in Google Colab or Jupyter and run all cells.

## Dashboard

An interactive web version of these results: (https://kgeren-portfolio.vercel.app/#)
