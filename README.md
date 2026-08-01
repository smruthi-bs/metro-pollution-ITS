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
- **Air quality:** CPCB CAAQM Dashboard  (Majestic, Peenya) (https://airquality.cpcb.gov.in/ccr/#/)
- **Rainfall:** India Meteorological Department (IMD), Pune (https://imdpune.gov.in/lrfindex.php)
- **Other weather variables:** NASA POWER Data Access Viewer (https://power.larc.nasa.gov/docs/services/api/temporal/daily/)
- **Vehicle registrations (BS4):** Transport Dept., Govt. of Karnataka (via OpenCity) (https://data.opencity.in/dataset/total-vehicles-registered-inbengaluru)

## Repository Structure
- DataTechies_code/ Jupyter notebooks (data extraction + ITS analysis)
- DataTechies_dataset/ Cleaned datasets used in the analysis

## Key Findings
## Key Findings
- **Carbon Monoxide (CO):** The only pollutant with a statistically significant immediate metro effect (Metro_P = 1.5875, p = 0.025) — CO levels rose right after the station opened, likely from construction and traffic disruption. The post-intervention trend change was only marginally significant (p = 0.091), so evidence for a sustained decline afterward is suggestive but not conclusive.
- **Particulate Matter (PM10):** No statistically significant immediate metro effect (Metro_P = 77.41, p = 0.25). PM10 did decline significantly over the full study period (T = -0.083, p < 0.001), but this appears to be a broader downward trend rather than something attributable specifically to the metro opening.
- **Nitrogen Dioxide (NO2):** The immediate metro effect was only marginally significant (Metro_P = 55.74, p = 0.10). Over the full study period, NO2 showed a significant *rising* trend (T = +0.051, p < 0.001), so the data don't support a clear reversal driven by the metro.
- **Nitric Oxide (NO):** No significant immediate metro effect (Metro_P = 3.79, p = 0.80).

Overall, CO is the only pollutant with reasonably strong evidence of a metro-related effect; PM10, NO, and NO2 show no statistically significant immediate impact from the metro opening once weather, vehicle growth, and (where applicable) industrial confounders are controlled for.
