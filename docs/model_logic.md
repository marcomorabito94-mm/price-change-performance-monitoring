# Model Logic

The production model was built in SQL and exposed through dashboard tables. The original query is not included because it references internal systems and business data.

This repository documents the modelling logic at a level that is useful for portfolio review without exposing internal implementation details.

## 1. Price-Change Perimeter

The model starts from articles that changed price during the last rolling 12 months.

Excluded cases include non-relevant article ranges and records without a previous price.

## 2. Effective Post-Change Window

For each article, the model calculates the effective number of days observed after the price change:

- from price start date to price end date when the price is closed
- from price start date to the latest available closed day when the price is still active

This avoids comparing a 10-day post period with a 90-day pre period.

## 3. Symmetric Pre-Change Window

The pre-change benchmark uses the same number of days as the post-change period, immediately before the new price started.

This makes pre/post comparison operationally readable and fairer on duration.

## 4. N-1 Benchmark

The N-1 benchmark uses the same calendar window from the previous year.

This is important in retail because performance can be strongly affected by seasonality. N-1 is often more stable than the immediately previous period when categories have seasonal demand patterns.

## 5. KPI Calculation

For each article and benchmark period, the model calculates:

- quantity sold
- sales including taxes
- sales excluding taxes
- store selling price value
- discount value
- margin value
- stock coverage

## 6. Performance Classification

The dashboard classifies each price change using three dimensions:

- price direction: up or down
- quantity direction: up or down
- margin direction: up or down

This creates readable business groups such as:

- `Price up - Qty down - Margin up`
- `Price down - Qty up - Margin up`
- `Price up - Qty down - Margin down`

The most important metric remains margin value, supported by revenue, quantity and price variation.

