# Stage 3 Calculation Validation

## Scope and baseline note

The app's calculation panel evaluates the illustrative test inputs below using the same calculation functions used for station metrics and basin summaries. These fixtures are test data, not live station observations.

The AWDB response supplies a "30-year median" but does not identify its reference years. The app therefore does not use that field as the specified 1991–2020 baseline: live Percent of Median and anomaly values remain unavailable until the baseline is verified. The AWDB median is shown as source data only.

## Case 1: Trial Lake SNOTEL (illustrative)

**Inputs**

- Current SWE: 24.6 in
- Median SWE: 20.5 in
- Snow depth: 72.0 in
- Liquid-water reference density: 62.4 lb/ft³

**Calculations and expected outputs**

1. Percent of Median: $(24.6 / 20.5) \times 100 = 120.0\%$
2. SWE anomaly: $24.6 - 20.5 = +4.1$ in
3. Snow density percentage: $(24.6 / 72.0) \times 100 = 34.1667\% \approx 34.2\%$
4. Bulk snow density: $(24.6 / 72.0) \times 62.4 = 21.32 \approx 21.3$ lb/ft³
5. Status: 120.0% is in the $110\% \le P_{\mathrm{med}} < 130\%$ band: **Above Normal (Light Blue)**.

## Case 2: Existing three-station case from `spec.md`

| Station | Current SWE (in) | Median SWE (in) | Station Percent of Median |
| --- | ---: | ---: | ---: |
| A | 10 | 8 | 125% |
| B | 20 | 20 | 100% |
| C | 30 | 40 | 75% |

- Average SWE: $(10 + 20 + 30) / 3 = 20.0$ in
- Mean of station percentages: $(125 + 100 + 75) / 3 = 100.0\%$

This preserves the existing spec validation case and its expected outputs.

## Case 3: Additional three-station basin case

| Station | Current SWE (in) | Median SWE (in) | Snow depth (in) | Station Percent of Median |
| --- | ---: | ---: | ---: | ---: |
| A | 18 | 20 | 60 | 90% |
| B | 12 | 15 | 48 | 80% |
| C | 27 | 25 | 80 | 108% |

- Average SWE: $(18 + 12 + 27) / 3 = 19.0$ in
- Average median SWE: $(20 + 15 + 25) / 3 = 20.0$ in
- Mean of station percentages: $(90 + 80 + 108) / 3 = 92.6667\% \approx 92.7\%$
- Ratio of basin means: $(19.0 / 20.0) \times 100 = 95.0\%$
- Mean SWE anomaly: $((-2) + (-3) + 2) / 3 = -1.0$ in

Per the spec, the app uses the **mean of valid station percentages (92.7%)** for the basin Percent of Median output. The 95.0% ratio is displayed only as a comparison.

## Edge cases and browser check

- Zero median: Percent of Median is `N/A`; the app does not divide by zero.
- Zero or missing snow depth: both density outputs are `N/A`.
- Missing current SWE: the station is excluded from current-SWE averages and the reading count.
- Percent-of-Median threshold boundaries at 70%, 90%, 110%, and 130% are tested using unrounded values.
- Browser UI result: **24 calculation, missing-value, and threshold checks passed.**
- Live AWDB check on 2026-11-24: 141 active stations loaded; latest daily readings were 2026-11-23. 140 stations had SWE readings, 141 had snow-depth readings, and AWDB supplied a median value for 103 stations. The live average SWE displayed as 2.3 in and the highest current reading as 8.6 in at Midway Valley. Live Percent of Median remained `N/A` because the AWDB median period is unverified.
