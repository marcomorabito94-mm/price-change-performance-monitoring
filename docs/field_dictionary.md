# Field Dictionary

All rows represent one synthetic article-level price change.

| Field | Meaning |
|---|---|
| `key` | Synthetic unique key: article ID plus price-change start date |
| `article_id` | Synthetic article identifier |
| `data_inizio_validita` | Start date of the new price |
| `data_fine_validita` | End date of the price validity, blank when still active |
| `price_before` | Selling price before the change |
| `price_in_period` | Selling price after the change |
| `delta_price` | Absolute difference between new price and previous price |
| `qty_pre` | Quantity sold in the pre-change comparison window |
| `qty_in_period` | Quantity sold after the price change |
| `sales_ht_pre` | Pre-change sales excluding taxes |
| `sales_pre` | Pre-change sales including taxes |
| `sales_ht_in_period` | Post-change sales excluding taxes |
| `sales_in_period` | Post-change sales including taxes |
| `cifra_ssp_pre` | Pre-change revenue valued at store selling price before discounts |
| `cifra_ssp_in_period` | Post-change revenue valued at store selling price before discounts |
| `sconto_a_valore_in_period` | Discount value in the post-change period |
| `margine_pp_valore_pre` | Margin value in the pre-change comparison window |
| `margine_pp_valore_in_period` | Margin value after the price change |
| `giorni_nel_periodo` | Number of observed post-change days |
| `delta_margine_pp_valore` | Margin value after the change minus margin value before the change |
| `qty_n_1` | Quantity sold in the equivalent N-1 period |
| `vendite_n_1` | Sales including taxes in the equivalent N-1 period |
| `vendite_ht_n_1` | Sales excluding taxes in the equivalent N-1 period |
| `margine_valore_n_1` | Margin value in the equivalent N-1 period |
| `gg_copertura` | Current stock coverage in days |
| `gg_copertura_n_1` | Stock coverage in days in the equivalent N-1 period |

## Notes

- `SSP` means store selling price, used here as a reference selling-price value before discounts.
- `HT` means excluding taxes.
- Margin value is the core KPI because it captures whether the price change creates or destroys economic value, not only whether revenue or quantity moved.

