
## The Question

The core business question:

**Did the introduction of free shipping (for orders above €50, starting July 2024) improve overall profitability — or did the company simply lose shipping revenue without enough upside to compensate?**

To answer this well, you'll probably need to explore:

- How did order volume change before vs. after?
- How did average order value change?
- What is the margin on products sold — and did the product mix shift?
- How much shipping revenue was lost?
- Did the additional volume make up for the lost shipping income?
- Are there differences across categories, channels, or regions?

---

## Technical Requirements

1. **Python + pandas** — Use Python with pandas to load, inspect, clean, and transform the data.
2. **SQL** — Use SQL (via SQLite or DuckDB) for your analytical queries. Load your cleaned data into a database and write queries to answer the business questions.
3. **Structured workflow** — Your work should follow a logical progression: load → inspect → clean → transform → analyze → conclude.

You can work in Jupyter notebooks, Python scripts, or a combination — whatever lets you show your process clearly.

---

## Suggested Approach

This is a suggestion, not a rigid recipe. Adapt as you see fit.

1. **Load and inspect** — Start by loading all three files and verifying that the data looks right. Check that all columns have the expected data types, the row counts make sense, and there are no obvious anomalies. Don't rush past this step.

2. **Clean** — Handle any data quality issues you find. Document what you found and what you did about it. Every decision you make here affects your analysis downstream.

3. **Enrich** — Join the datasets as needed. Calculate derived metrics like product margin, order profit, period labels (pre/post free shipping).

4. **Analyze** — Write SQL queries to compare the pre- and post-free-shipping periods. Look at the data from multiple angles: overall, by category, by channel, by region.

5. **Conclude** — Translate your numbers into a business recommendation. What should the company do? Keep free shipping? Modify the threshold? Roll it back?

---

## Deliverables

Prepare a **short presentation** (slides, a notebook, or a written report — your choice) that covers:

1. **Data quality findings** — What issues did you discover in the data? How did you handle them, and why?
2. **Methodology** — How did you approach the analysis? What SQL queries or transformations were key?
3. **Results** — What do the numbers say? Include relevant tables or charts.
4. **Business recommendation** — Answer the question: should the company continue with free shipping? Support your recommendation with data.
5. **Caveats and assumptions** — What limitations does your analysis have? What would you want to investigate further with more data or time?

The focus should be on your **reasoning and recommendations**, not just on producing code or charts. We want to see that you understand the data and can think critically about what it means for the business.

---

## Timeline

You have **two weeks** to complete this assignment. Given that you're also attending classes, plan your time accordingly. A rough breakdown:

| Phase | Suggested time |
|---|---|
| Data loading, inspection, cleaning | 3–4 days |
| Data enrichment and SQL setup | 2–3 days |
| Analysis and querying | 3–4 days |
| Presentation / write-up | 2–3 days |

Don't spend all your time on cleaning and none on analysis — and don't skip cleaning to jump straight to analysis. Both matter.
