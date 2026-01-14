# Marketing Campaign Data Cleaning

A comprehensive data cleaning pipeline for messy marketing campaign data using Python and pandas.

## Overview

This notebook demonstrates professional data cleaning techniques applied to a real-world marketing campaign dataset containing 2,020 records with various data quality issues.

## Dataset

**File:** `marketing_campaign_data_messy.csv`

**Columns:**
- Campaign_ID, Campaign_Name
- Start_Date, End_Date
- Channel (marketing platform)
- Impressions, Clicks, Spend, Conversions
- Active (campaign status)
- Campaign_Tag

## Data Quality Issues Addressed

### 1. Header Cleaning
- Removed leading/trailing whitespace
- Standardized to lowercase with underscores
- Eliminated duplicate column names

### 2. Currency Cleaning
- Removed dollar signs and special characters from `Spend` column
- Converted to numeric type for analysis

### 3. Categorical Typos
Fixed inconsistent channel names using fuzzy matching:
- `Facebok` → `Facebook`
- `Insta_gram` → `Instagram`
- `Tik_Tok` → `TikTok`
- `Gogle` → `Google Ads`
- `E-mail` → `Email`

### 4. Boolean Standardization
Unified mixed boolean representations in `Active` column:
- `Yes/No`, `Y/N`, `1/0`, `True/False` → consistent boolean type

### 5. Date Parsing
- Converted mixed date formats to datetime
- Handled multiple date formats (YYYY-MM-DD, DD/MM/YYYY, timestamps)
- Applied `dayfirst=True` for UK date formats

### 6. Logical Integrity - Clicks vs Impressions
- Validated that clicks never exceed impressions
- Identified impossible scenarios

### 7. Logical Integrity - Time Travel
- Fixed campaigns where end_date < start_date
- Applied 30-day default duration correction

### 8. Outlier Handling
- Used IQR method with 3× multiplier
- Winsorized extreme spend values (capped at upper bound)
- Preserved data distribution while removing anomalies

### 9. Feature Extraction
- Parsed campaign names using regex
- Extracted `season` field (Summer, Winter, Launch, BlackFriday)
- Pattern: `Q#_Season_CMP-#####`

## Key Techniques

- **Regex patterns** for string parsing and extraction
- **Quantile-based outlier detection** (IQR method)
- **Boolean mapping** for mixed data types
- **Date parsing** with error handling
- **Fuzzy categorical matching** via dictionaries

## Results

Clean dataset ready for analysis with:
- Standardized column names
- Consistent data types
- Validated logical relationships
- Extracted semantic features
- Handled outliers appropriately

## Dependencies

```python
pandas
numpy
```

## Usage

```python
import pandas as pd
import numpy as np

df = pd.read_csv('marketing_campaign_data_messy.csv')
# Apply cleaning steps as shown in notebook
```

## Notes

This notebook demonstrates industry-standard data cleaning practices suitable for marketing analytics, business intelligence, and data science workflows.
