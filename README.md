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
  - BS4 emission standard rollout (April 2017)
  - Vehicle registration growth
  - Industrial confounding (Peenya pollutant levels)

## Data Sources
- **Air quality:** CPCB CAAQM Dashboard  (Majestic, Peenya) (https://airquality.cpcb.gov.in/ccr/#/)
- **Rainfall:** India Meteorological Department (IMD), Pune (https://imdpune.gov.in/lrfindex.php)
- **Other weather variables:** NASA POWER Data Access Viewer ( https://power.larc.nasa.gov/docs/services/api/temporal/daily/)
- **Vehicle registrations (BS4):** Transport Dept., Govt. of Karnataka (via OpenCity) (https://data.opencity.in/dataset/total-vehicles-registered-inbengaluru)

## Repository Structure
- DataTechies_code/ Jupyter notebooks (data extraction + ITS analysis)
- DataTechies_dataset/ Cleaned datasets used in the analysis

## Key Findings
- **CO** showed the strongest evidence of a metro-related effect: an immediate post-opening increase followed by a significant long-term decline (~15% reduction from baseline by late 2019).
- **PM10** showed a large immediate spike (construction-related) with a marginally significant post-intervention decline.
- **NO2** showed a pre-intervention rising trend that reversed after the metro opened.
- **NO and PM2.5** showed no statistically significant metro-related effects.
