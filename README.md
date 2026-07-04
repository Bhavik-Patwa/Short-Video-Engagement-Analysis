# Short-Video Engagement Analysis

An end-to-end analytics project built on the **KuaiRand-Pure** public dataset to understand how short-video impressions convert into click, watch and higher-value engagement outcomes and to identify which impression-content combinations are most likely to drive business value.

## Project Purpose

Short-video delivery creates millions of impression opportunities, but not all impressions generate the same downstream value. This project evaluates the impression-to-engagement funnel and translates it into actionable strategy for a marketing and media audience.

The project focuses on four goals :

- Build a credible, cleaned analytical dataset at the **impression level**
- Quantify how impressions convert into **clicks, meaningful watch behavior and high-value engagement**
- Identify **audience, content and delivery-context segments** that outperform their baselines
- Develop an interpretable **click propensity model** to support prioritization

## Business Questions

- How efficiently do impressions convert into clicks, meaningful watches and high-value engagement?
- How much of performance variation is explained by **traffic source and feed placement**?
- Which user and content segments consistently outperform their traffic-source baseline?
- Can click probability be modeled reliably enough to support prioritization decisions?

## Dataset

**Source :** KuaiRand-Pure public dataset

**Files used :**
- Interaction logs
- User features
- Basic video features

**Excluded from the predictive base :**
- `video_dimension_statistic` aggregate fields, because they are post-outcome summaries and unsuitable for impression-level prediction

## Final Analytical Scope

**Primary prediction target :** `is_click`  
**Secondary business outcome :** `is_high_value_engagement = follow OR comment OR forward`  
**Meaningful watch definition :** `long_view`

## Tech Stack

- **Python** : data loading, cleaning, feature engineering, analysis, modeling
- **Azure Blob Storage** : raw, curated, presentation and model-output storage
- **Power BI** : dashboard development and insight delivery
- **Parquet** : curated and presentation-ready exports

## Project Structure

```text
.
├── scripts/
│   └── bootstrap.py
├── notebooks/
│   └── notebook.ipynb
├── dashboards/
│   ├── dashboards.pbix
│   ├── Executive Overview.jpg
│   ├── Delivery Context.jpg
│   ├── Daily Performance.jpg
│   ├── Segment Opportunities.jpg
│   └── Strategy Priorities.jpg
├── requirements.txt
└── .env
```

## Implementation Flow

1. Connected to Azure Blob Storage and verified all expected raw dataset files.
2. Audited file coverage, schema, row counts, join coverage, duplicates, missingness and temporal fields.
3. Built an impression-level fact table and removed exact duplicates plus unresolved duplicate event keys.
4. Added business-ready fields such as :
   - `is_meaningful_watch`
   - `is_high_value_engagement`
   - `traffic_source`
   - `video_age_days`
   - `video_orientation`
   - `playback_completion_rate`
5. Created analysis-ready exports :
   - `impression_fact.parquet`
   - `impression_analysis_base.parquet`
   - `video_tag_bridge.parquet`
   - `click_model_dataset_standard_traffic.parquet`
6. Performed funnel, conversion, daily, segment, creator and content analysis.
7. Trained an interpretable logistic regression click model for **standard traffic**.
8. Exported curated presentation tables for Power BI.

## Reproducibility

1. Create a virtual environment and install dependencies from `requirements.txt`
2. Set `AZURE_STORAGE_CONNECTION_STRING` in `.env`
3. Ensure raw KuaiRand-Pure files are available in the `raw` blob container
4. Run the notebook end-to-end in sequence
5. Refresh Power BI using the exported Parquet outputs

## Key Results

### Core Funnel
- **Impressions :** 2,597,699
- **Click Rate :** 33.29%
- **Meaningful Watch Rate :** 22.14%
- **High-Value Engagement Rate :** 0.29%

### Delivery Context
- **Standard traffic** materially outperformed **random traffic**
- Standard traffic click rate : **46.46%**
- Random traffic click rate : **17.62%**
- Standard traffic high-value engagement rate : **0.46%**
- Random traffic high-value engagement rate : **0.09%**

### Post-Click Conversion
Among clicked impressions :
- Click to meaningful watch : **66.25%**
- Click to profile enter : **4.24%**
- Click to like : **2.98%**
- Click to high-value engagement : **0.80%**

### Daily Performance
Daily rate shifts were strongly influenced by **traffic-source mix**, especially after April 22, when random traffic became dominant. This means headline daily conversion changes should not be interpreted without delivery-context adjustment.

### Segment Opportunity Signals
Traffic-source-aware segment analysis highlighted stronger-performing opportunities in :
- certain **registration-age bands**, especially mid-age registered users
- users with **higher follow-count bands**
- selected **video upload types**
- selected **orientation and creator cohorts**

### Predictive Model
A standard-traffic logistic regression model outperformed a dummy baseline :

- **Validation ROC-AUC :** 0.6566
- **Test ROC-AUC :** 0.6462
- **Validation Average Precision :** 0.5832
- **Test Average Precision :** 0.5627

The top test decile achieved an **actual click rate of 61.76%**, versus an overall standard-traffic baseline near **46.46%**.

## Business Interpretation

- Delivery quality matters as much as content quality; the same platform can generate very different engagement efficiency depending on traffic allocation.
- Daily performance reporting must control for **traffic mix**, otherwise drops and spikes can be misread.
- High-value engagement is rare, so strategy should focus on **high-scale segments with consistent lift**, not only extreme niche performers.
- The click model is useful as a **ranking tool for impression prioritization**, not as a causal engine.

**So what?**
- Prioritizing **standard-traffic impressions in the top model decile** raises click rate to **61.76%**, about **1.33x** the average standard-traffic click rate. Using the observed standard-traffic click-to-meaningful-watch conversion rate, this corresponds to roughly **110 additional meaningful watches per 1,000 impressions** versus average standard traffic.

**Immediate modeling takeaway**
- **Feed-tab placement, video upload type and user activity segment** were among the strongest observed drivers of click likelihood in the interpretable model.

## Dashboards

### Executive Overview
![Executive Overview](dashboards/Executive%20Overview.jpg)

### Segment Opportunities
![Segment Opportunities](dashboards/Segment%20Opportunities.jpg)

Additional dashboard pages in the repository :
- Delivery Context
- Daily Performance
- Strategy Priorities

## Deliverables

- Cleaned impression-level analytical dataset
- Curated Parquet tables for analysis and reporting
- Segment and creator opportunity summaries
- Standard-traffic click propensity model
- Power BI dashboard package (`dashboards.pbix`)
- Dashboard image exports for documentation and review

## Limitations

- Findings are based on a public observational dataset, not campaign-specific business data.
- Some downstream events occur without click, so the full dashboard funnel should be read as **impression-to-outcome progression**, not a fully strict sequential funnel.
- The predictive model is intentionally interpretable and practical, not optimized for maximum complexity or maximum accuracy.
- Very small-volume categories were filtered or treated cautiously in priority views.

## Conclusion

This project delivers a credible impression-to-engagement intelligence workflow for short-video content. It demonstrates that conversion quality is heavily shaped by delivery context, that traffic-mix-adjusted analysis is necessary for valid interpretation and that segment-aware prioritization can materially improve click and engagement outcomes. The result is a business-ready analytical foundation, a practical modeling layer and a dashboard suite designed for media and content strategy decisions.

## Future Scope

- Add calibrated probability monitoring and threshold-based prioritization
- Extend modeling to `high_value_engagement`
- Incorporate richer content metadata if available
- Build reusable Power BI drill-through views for creator, segment and tag diagnostics
- Evaluate uplift-oriented ranking strategies beyond click prediction