# Dashboard Reports

This folder contains the final Power BI reporting assets for the **Short-Video Engagement Analysis** project.

## Files in This Folder

- `dashboards.pbix`
- `Executive Overview.jpg`
- `Delivery Context.jpg`
- `Daily Performance.jpg`
- `Segment Opportunities.jpg`
- `Strategy Priorities.jpg`

## What These Dashboards Show

The report is designed for a marketing/media strategy audience and answers five practical questions :

### 1. Executive Overview
How efficiently do impressions convert into valuable engagement?

This page summarizes the core topline metrics :
- impressions
- click rate
- meaningful watch rate
- high-value engagement rate
- overall impression-to-outcome progression
- traffic-source positioning

### 2. Delivery Context
How does delivery context change engagement quality before and after click?

This page compares :
- standard vs random traffic
- feed-tab placement quality
- context-level differences in click and engagement performance

### 3. Daily Performance
Are daily shifts driven by traffic mix or by true performance changes?

This page is especially important because it separates :
- actual daily click performance
- expected performance based on traffic-source mix
- the remaining gap after adjusting for mix

### 4. Segment Opportunities
Which audience and content segments offer stronger engagement?

This page highlights :
- stronger pre-click opportunity segments
- stronger post-click high-value segments
- top-performing video-tag groups by scale and quality

### 5. Strategy Priorities
Where are the clearest action opportunities?

This page surfaces :
- segment pathways linked to stronger high-value engagement
- creators with stronger conservative high-value potential
- which segment types dominate the opportunity mix

## Important Interpretation Notes

A few points matter when reading the report :

- The project’s Page 1 funnel should be interpreted as **impression-to-outcome progression**, not as a perfectly strict step-by-step behavioral funnel across every stage.
- Traffic source is a major structural divider in the dataset, so many comparisons are intentionally traffic-source-aware.
- The predictive model supports prioritization and ranking. It should not be treated as a causal or production-grade recommendation engine.

## Intended Use

These dashboards are meant to support :
- strategy presentations
- project reviews
- portfolio demonstrations
- business storytelling around short-video engagement behavior

They are not intended to serve as a live production BI environment.

## Project Context

The dashboards are based on curated analytical tables derived from the **KuaiRand-Pure** public dataset and built through :
- Python-based cleaning and feature engineering
- Azure Blob Storage export layers
- Power BI visualization and storytelling

For the full project background, methodology and modeling details, see the repository root `README.md`.