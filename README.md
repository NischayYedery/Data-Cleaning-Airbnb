# Data-Cleaning-Airbnb
Airbnb, Inc is an American company that operates an online marketplace for lodging, primarily homestays for vacation rentals, and tourism activities. Based in San Francisco, California, the platform is accessible via website and mobile app.
NYC Airbnb Open Data — Data-Cleaning README
(based on the supplied Airbnb_Open_Data.csv, 10 May 2025)

NYC Airbnb Data-Cleaning Project – Plain-English Walk-through
(Last updated 10 May 2025 – no visualisations yet)

1. Why this project exists
Airbnb’s New-York-City “Open Data” dump is rich but messy: mixed data-types, missing values, stray currency symbols, and a few price tags large enough to buy a townhouse.
The goal here was simple:

Turn one raw CSV into one tidy, analysis-ready table

Document every step so a newcomer can reproduce (or extend) the work in minutes.

2. What you’ll find in this folder
File	What it is	Status
Airbnb_Open_Data.csv	Original Kaggle snapshot (~102 k rows × 26 columns)	Untouched
Data cleaning for airbnb.ipynb	Jupyter notebook that performs every cleaning step, with inline explanations	Executable
Cleaned_data.csv	Final, polished dataset (99 k rows × 20 columns)	Ready for models/BI
requirements.txt	Minimal package list (pandas, numpy, jupyter)	Optional

No charts or dashboards are generated; the focus is solely data hygiene.

3. Bird’s-eye view of what was done
Load the raw file (Airbnb_Open_Data.csv) into a pandas DataFrame.
Standardise the schema – rename columns to lower_snake_case, drop the auto-generated index.
Fix data types – convert prices and fees from strings like “$368 ” to numeric, parse last_review into real datetimes.

Handle missing values

Critical columns (price, room type, neighbourhood) – drop rows if blank.
Informational columns (house rules, license) – keep but fill with "Unknown" and flag.
Tame outliers – any nightly price above the 99th percentile was clipped and marked with is_outlier_price = 1.
Clean categoricals – trim whitespace and lower-case neighbourhood names, merge spelling variants.
Basic sanity checks – ensure lat/long fall inside NYC, minimum_nights ≥ 1, construction_year between 1800-2025.
Save the result as Cleaned_data.csv and delete all temporary variables to free memory.

4. What we achieved

99 342 listings retained (≈ 97% of the original), all with complete core fields.
Numeric columns now behave like numbers – no stray “$” or commas.
Outliers flagged rather than silently removed, preserving transparency.

Some of the Key pandas functions & methods you’ll see in the notebook

pd.read_csv()            # ingest the raw file
DataFrame.rename()       # column-name cleanup
DataFrame.dropna()       # remove rows missing critical fields
DataFrame.replace()      # strip "$", "," and unify categories
DataFrame.astype()       # cast to int, float, bool, datetime
DataFrame.apply()        # custom lambdas (e.g., price clipping)
Series.isna()            # detect remaining nulls
DataFrame.duplicated()   # find duplicate listings




