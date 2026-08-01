# Causal Impact of Green Transport Policies on Urban Pollution Levels

## Problem Statement
Evaluating the causal impact of Bangalore Metro expansion on urban air pollution using Interrupted Time-Series (ITS) analysis.

**Core question:** Did the opening of the Majestic Metro station on June 18, 2017, lead to a significant reduction in air pollution levels (PM10, PM2.5, NO, NO2, CO) in the surrounding area?

## Approach
- **Treatment site:** Majestic (near the metro interchange station)
- **Control site:** Peenya (industrial area, proxy for regional/industrial trends)
- **Method:** Segmented regression / Interrupted Time-Series analysis with robust (HC1)
  standard errors, controlling for:
  - Meteorological variables (temperature, humidity, wind speed, precipitation, pressure)
  - BS4 emission standard rollout (April 2017) effects by tracking vehicle registration growth (new vehicles registered post-2017 comply with BS4 norms)
  - Industrial confounding (Peenya pollutant levels)

## Data Sources
- **Air quality:** CPCB CAAQM Dashboard (Majestic, Peenya) (https://airquality.cpcb.gov.in/ccr/#/)
- **Rainfall:** India Meteorological Department (IMD), Pune (https://imdpune.gov.in/lrfindex.php)
- **Other weather variables:** NASA POWER Data Access Viewer (https://power.larc.nasa.gov/docs/services/api/temporal/daily/)
- **Vehicle registrations (BS4):** Transport Dept., Govt. of Karnataka (via OpenCity) (https://data.opencity.in/dataset/total-vehicles-registered-inbengaluru)

## Repository Structure

```text
metro-pollution-ITS/
├── DataTechies_code/
│   ├── analysis.ipynb
│   └── weather_extract.ipynb
├── DataTechies_dataset/
│   ├── bs4_registration.csv
│   ├── its_merged_data_final.csv
│   ├── majestic_pollutants_cleaned_2016_2019.csv
│   ├── majestic_weather_final.csv
│   └── new_peenya_pollutants_cleaned_2016_2019.csv
├── model_summaries/
│   ├── Majestic_CO_its_robust_summary.txt
│   ├── Majestic_NO2_its_robust_summary.txt
│   ├── Majestic_NO_its_robust_summary.txt
│   └── Majestic_PM10_its_robust_summary.txt
├── plots/
│   ├── Majestic_CO_its_plot.png
│   ├── Majestic_NO2_its_plot.png
│   ├── Majestic_NO_its_plot.png
│   └── Majestic_PM10_its_plot.png
└── README.md
```

Note: this repo includes the weather extraction step and the final analysis notebook. Air-quality data cleaning (CPCB) and BS4 registration processing were done outside this repo; the cleaned outputs are included directly in `DataTechies_dataset/`.

## Model Terms
- **T** — underlying time trend (change per day, independent of any intervention)
- **Metro_P** — immediate step-change in pollution level right after the metro opened
- **Metro_TP** — change in the pollution *trend* (slope) after the metro opened, relative to the pre-metro trend
- **BS4_P / BS4_TP** — equivalent step-change and trend-change terms for the BS4 emission standard rollout

## Key Findings
- **Carbon Monoxide (CO):** CO was the only pollutant that showed a real, statistically significant jump right after the metro opened (p = 0.025), likely from construction and traffic disruption around the station. There's a hint of a decline afterward, but it's only marginally significant (p = 0.091), so we can't say for sure it was a lasting drop.
- **Particulate Matter (PM10):** No real immediate effect from the metro opening here (p = 0.25). PM10 did fall significantly over the full study period, but that looks like a general downward trend across the years rather than something the metro specifically caused.
- **Nitrogen Dioxide (NO2):** The immediate effect was borderline at best (p = 0.10), and NO2 actually trended upward over the full study period, likely reflecting steady traffic growth outweighing any metro-driven reduction.
- **Nitric Oxide (NO):** No significant effect from the metro opening at all (p = 0.80).

Overall, CO is the only pollutant with reasonably strong evidence of a metro-related effect; PM10, NO, and NO2 show no statistically significant immediate impact from the metro opening once weather, vehicle growth, and (where applicable) industrial confounders are controlled for.

## Why Some Effects Aren't Significant

The positive point estimates for PM10 and NO2 (despite non-significant p-values) are
likely explained by a few factors:

- **BS4 and Metro dates are close together** (April 2017 vs. June 2017, ~2.5 months apart), which makes it hard for the model to separate one policy's effect from the other. This is consistent with the high condition number (2.03e+05) flagged in the regression output, indicating multicollinearity.
- **Construction/disruption effects around the opening date** may have temporarily increased traffic-related pollutants (CO, NO2) rather than decreased them, since feeder infrastructure and connecting roads were still being finished.
- **Modest R² (0.16–0.26)** means a lot of daily variance is driven by factors outside the model (weather, festivals, seasonal effects), which can swamp a real but small metro effect.

In short: the estimates are directionally positive but statistically not significantly different from zero for most pollutants, which probably reflects overlapping timing of policies and the presence of noisy daily data rather than a true causal decline in air quality.

## Team
Smruthi B S, Surya Satvik, Syeda Sheema Suman, Tanmaya Karanth
