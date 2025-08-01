# 🧠 Rethinking Product Data Integrity at FoodYum

## Context

This project began with a simple goal: ensure FoodYum’s product dataset was complete and consistent. But beneath that surface task was a deeper opportunity — to assess how data cleaning decisions affect analytical outcomes, and how we, as analysts, shape business understanding through technical judgment.

---

## 🔍 Key Observations and Thought Process

### 1. Not All Nulls Are Created Equal

When the system bug left some `year_added` values missing, it raised a bigger question:  
> *What do we lose when temporal context is stripped from price data?*

By assuming 2022 for missing `year_added`, we restore analytical continuity — but also introduce a risk of masking older products. The tradeoff between imputation and transparency is one I consciously made to prioritize completeness for pricing analysis.

### 2. Median Over Mean: A Conscious Bias

For `price` and `weight`, I chose **median** imputation via `PERCENTILE_DISC`. This was not just technical correctness — it was about fairness:
- Food prices are often skewed by premium items.
- Medians resist outliers, giving a more representative "typical" value.

This is especially critical when FoodYum aims to serve a broad range of customers.

### 3. Clean ≠ Standardized: Why REGEXP Matters

Not all weights are entered cleanly — some may read “500g” or “1.2kg”. Using `REGEXP_REPLACE` allowed me to:
- Strip unwanted characters
- Standardize weights to numeric
- Preserve units for meaningful comparisons

This was a small act of technical empathy: building SQL that assumes human messiness.

### 4. Defensive Querying for Brand Integrity

Some brands were entered with dashes ("-") or left blank. The logic:
```sql
NULLIF(REPLACE(brand, '-', ''), '')


---

Let me know if you'd like this version tailored for a portfolio submission, job application, or school project — or if you want a short reflective paragraph instead of a full README.
