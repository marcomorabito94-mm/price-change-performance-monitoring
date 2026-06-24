# Price Change Performance Monitoring in Retail

> Real business case study rebuilt with synthetic data.  
> The original project was developed on internal retail data; this repository contains fake, synthetic records with the same analytical structure. Dashboard screenshots are included only as demonstration examples, using random filters and periods, and do not disclose real business results.

**Domain:** Retail pricing / commercial performance  
**Methods:** Price-change monitoring, pre/post analysis, N-1 seasonal benchmark, margin impact classification  
**Stack:** SQL data modelling · Dashboarding · Retail KPI design

---

## Business Problem

In retail, price changes are frequent and can affect revenue, quantity sold and margin in different directions.

A price increase is not automatically good if it destroys volume or margin value. A price decrease is not automatically bad if it unlocks enough quantity and protects total margin. The business need was to create a monitoring model that lets Performance Leaders, Product Leaders and Pricing teams quickly understand which price changes are working, which are risky and where corrective action may be needed.

The dashboard built on top of the model allows users to:

- monitor all price changes in the last rolling 12 months
- compare performance after the change vs the period immediately before the change
- compare performance after the change vs the same period in the previous year
- classify each reference by price direction, quantity movement and margin movement
- identify where margin value is gained or lost
- drill from executive summary tables to article-level price-change details

## Why Two Benchmarks

The model uses two complementary readings.

**Pre/post price-change benchmark**

This compares the post-change period with an equivalent period immediately before the change. It is useful to read the short-term effect of the price move, especially for fast operational monitoring.

However, it can be noisy. If the pre-change period is not seasonally comparable, the model may overstate or understate the real impact.

**N-1 benchmark**

This compares the post-change period with the same period in the previous year. In retail this is often more robust because seasonality, campaigns, weather patterns and category cycles can strongly affect demand.

For that reason, the dashboard includes both views: pre/post for immediate control and N-1 for a more seasonally stable interpretation.

## Analytical Approach

The original SQL model was not published because it was built on internal data sources. The logic is reproduced here at a business and data-model level:

- build the perimeter of articles with a valid price change in the last rolling 12 months
- calculate the effective number of days observed after the price change
- create a pre-change comparison window with the same duration as the post-change window
- calculate quantity, sales, sales excluding taxes and margin value before and after the change
- calculate the same KPIs on the equivalent N-1 period
- add stock coverage indicators to contextualize performance
- expose the output table to dashboard views and business filters

## Dashboard Examples

### Summary of Price Changes

![Summary](assets/dashboard_summary.png)

This view separates the changed-price perimeter from the total business perimeter and shows the incidence of price changes on revenue, quantity and margin.

### Performance vs Previous Period

![Performance vs previous period](assets/dashboard_pre_post_performance.png)

This view classifies price changes by the direction of price, quantity and margin after the change. The core KPI is **margin value delta**, supported by revenue and quantity progression.


### Performance vs N-1

![Performance vs N-1](assets/dashboard_n1_performance.png)

This view uses the same period from the previous year as benchmark, which is especially useful when retail seasonality makes the immediate previous period less reliable.

## Key Metrics

- **Variation PV:** price variation vs previous selling price
- **Delta Margin:** margin value generated after the change minus margin value before the change
- **Progression CA:** revenue progression vs benchmark period
- **Progression Qty:** quantity progression vs benchmark period
- **Progression Mrg:** margin value progression vs benchmark period
- **N-1 metrics:** same performance metrics calculated against the equivalent period in the previous year
- **Stock coverage:** days of stock coverage used to contextualize performance signals

## Example Insights Enabled

The model helps distinguish cases that look similar at first glance but require different actions:

- **Price up, quantity down, margin up:** acceptable when the margin gain offsets the volume loss
- **Price up, quantity down, margin down:** high-risk changes where price elasticity may be too strong
- **Price down, quantity up, margin up:** potentially successful tactical move
- **Price down, quantity up, margin down:** volume recovery is not enough to protect value
- **Pre/post positive but N-1 weak:** possible seasonal distortion in the immediate benchmark
- **N-1 positive but pre/post weak:** possible short-term noise or transition effect after the change

## Repo Structure

```text
├── assets/
│   ├── dashboard_n1_performance.png
│   ├── dashboard_pre_post_performance.png
│   └── dashboard_summary.png
├── data/
│   └── synthetic_price_change_model.csv
├── docs/
│   ├── field_dictionary.md
│   ├── model_logic.md
│   └── synthetic_data_qa.json
└── README.md
```

## Data

The dataset in `data/synthetic_price_change_model.csv` is synthetic and contains 6,500 article-level price-change records.
No real article IDs, prices, quantities, sales, margins or internal source data are included.


