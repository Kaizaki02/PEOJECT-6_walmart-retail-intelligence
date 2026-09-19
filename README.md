## Model Results

### Final Baseline vs Tuned Comparison

| Model                        | RMSE          | R²       |
|-------------------------------|--------------:|---------:|
| Random Forest (baseline)      | 113,537.68    | 0.9600   |
| Random Forest (tuned)         | 113,598.52    | 0.9599   |
| Gradient Boosting (baseline)  | 163,769.39    | 0.9167   |
| Gradient Boosting (tuned)     | 92,146.03     | 0.9736   |

**Best model: Tuned Gradient Boosting** — lowest RMSE and highest R² across all models. Tuning gave Gradient Boosting a large boost (RMSE dropped ~44%, R² rose from 0.917 to 0.974). Random Forest was already near-optimal at baseline, so tuning made virtually no difference (RMSE actually rose marginally, within noise).

## Key Findings

1. **Holiday effect is real:** Holiday weeks show a statistically significant difference in average weekly sales compared to non-holiday weeks (t-test), confirming that seasonal/promotional events materially move revenue.
2. **Store identity dominates:** ANOVA and feature-importance results show store identity is the strongest driver of sales variation — structural differences between stores (location, size, demographics) matter more than short-term macro-economic fluctuations.
3. **Macro indicators are individually weak but useful in combination:** CPI, Unemployment, Fuel_Price, and Temperature show weak linear correlation with Weekly_Sales on their own, but tree-based ensembles capture non-linear interactions between them and outperform Linear Regression.
4. **Tuning helps selectively:** Hyperparameter tuning (RandomizedSearchCV for Random Forest, GridSearchCV for Gradient Boosting) improved Gradient Boosting substantially; Random Forest baseline was already strong, validated via 5-fold cross-validation.

## Recommendations

1. **Inventory & Staffing** — Increase stock and staffing ahead of known holiday weeks, especially for historically high-performing stores.
2. **Store-level Strategy** — Since store identity strongly affects sales, develop store-specific (rather than one-size-fits-all) forecasting and promotional strategies.
3. **Macro-monitoring** — Track CPI and unemployment trends regionally; their effect, while individually weak, compounds with other factors in ensemble model predictions.
4. **Model Deployment** — Deploy the tuned Gradient Boosting model for weekly sales forecasting, retraining periodically (e.g. monthly) as new sales data accumulates.
5. **Further Work** — Incorporate additional external data (regional events, local competitor activity, promotional calendars) to further improve model accuracy.