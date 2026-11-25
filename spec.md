# Problem 6: Utah Snowpack Map

## 1. Purpose

- **Overview:** Map the SNOTEL snow-monitoring sites in Utah and show how this year's snowpack compares to normal.
- **Audience:** Water resource engineers, hydrologists, municipal water planners, and backcountry recreationists evaluating Utah's spring runoff potential and drought/flood status.

## 2. Inputs

- **Basin / Watershed Filter:** Dropdown selector with All Utah Basins and every basin represented by included Utah SNOTEL stations. Use AWDB station basin metadata where available and a curated mapping for remaining stations. Default: All Utah Basins. Include only stations located within Utah.
- **Target Date:** Date picker limited to dates with available AWDB data. Default: the latest available date. The selected date determines the water year (October 1–September 30) for the time-series window.
- **Minimum Elevation Filter:** Slider or numeric box in feet. Range: 6,000–11,500 ft; step: 250 ft; default: 6,000 ft.
- **Station Selection:** Select a SNOTEL marker on the map or choose a station from a searchable dropdown/list. Default: statewide summary with no station selected.
- **Display Metric Toggle:** Radio buttons to color-code map markers by Current SWE (in) or Percent of 1991–2020 Median (%). Default: Percent of Median.
- **Data Source and Runtime:** Retrieve station metadata and data from the NRCS AWDB REST API directly in the browser. The app requires internet access; load Leaflet and Chart.js from a CDN. Verify AWDB browser access (CORS) before implementation. If requests fail, show a clear error with a retry option; do not present missing values as zero or as a successful load.
- **Filter Scope:** Apply basin, target-date, and elevation filters to the map, KPIs, station table, and station selection. If filters exclude the selected station, clear the selection and return to the summary state.

## 3. Calculations

- **Snow Water Equivalent ($SWE$, in):** Depth of liquid water contained in the snowpack, retrieved from NRCS SNOTEL ($WTEQ$ sensor) in inches (in).

- **Historical Baseline:** Use the fixed 1991–2020 period and compare each selected date with the median for the same day of water year. Use the same aligned series in the chart and calculate medians from available historical observations only. Use the AWDB median field only if its period and alignment match; otherwise, source or calculate 1991–2020 medians rather than substituting an unspecified 30-year median.

- **Percent of Normal / Median ($P_{\mathrm{med}}$, %):**

  $$
  P_{\mathrm{med}} =
  \left(\frac{SWE_{\mathrm{current}}}{SWE_{\mathrm{median}}}\right)\times 100
  $$

  *(Handle edge cases where $SWE_{\mathrm{median}} = 0$ in early/late season by displaying `N/A` instead of dividing by zero.)*

- **SWE Anomaly ($\Delta SWE$, in):**

  $$
  \Delta SWE = SWE_{\mathrm{current}} - SWE_{\mathrm{median}}
  $$

- **Estimated Snow Density ($\rho_{\mathrm{snow}}$, % or lb/ft$^3$):** When snow depth ($D_{\mathrm{snow}}$, in) is available ($D_{\mathrm{snow}} > 0$):

  $$
  \text{Density (\%)} =
  \left(\frac{SWE_{\mathrm{current}}}{D_{\mathrm{snow}}}\right)\times 100,
  \qquad
  \rho_{\mathrm{snow}} =
  \left(\frac{SWE_{\mathrm{current}}}{D_{\mathrm{snow}}}\right)\times 62.4\ \mathrm{lb/ft^3}
  $$

  Display `N/A` when snow depth is missing or less than or equal to zero.

- **Basin Average SWE & Percent of Median:** Compute the arithmetic mean of current SWE over stations with a non-null current SWE value, and the arithmetic mean of $P_{\mathrm{med}}$ over stations with a valid $P_{\mathrm{med}}$, within the selected basin and elevation filter.

- **Station Inclusion for Counts and Averages:** Keep active Utah SNOTEL stations visible in the map and table even when they have no current SWE reading; show a neutral marker and `N/A`. Count only stations with a non-null current SWE value for the selected date. Calculate each average using only stations with valid values for that metric. A missing or zero median makes $P_{\mathrm{med}}$ `N/A` and excludes that station from the Percent of Median average, but not from the current-SWE average or station count.

- **Marker Status Thresholds (Color Rules):**
  - Classify using the unrounded $P_{\mathrm{med}}$ value.
  - $P_{\mathrm{med}} < 70\%$: Red (Well Below Normal)
  - $70\% \le P_{\mathrm{med}} < 90\%$: Orange (Below Normal)
  - $90\% \le P_{\mathrm{med}} < 110\%$: Green (Near Normal)
  - $110\% \le P_{\mathrm{med}} < 130\%$: Light Blue (Above Normal)
  - $P_{\mathrm{med}} \ge 130\%$: Dark Blue / Purple (Well Above Normal)

- **Current SWE Color Scale:** When Current SWE is selected, use a sequential color scale based on the minimum and maximum SWE values of the currently visible stations. Update the legend to show that range.

## 4. Outputs

- **Interactive Map (Leaflet):** Utah map showing color-coded circular station markers and a color-scale legend. Clicking a marker opens a popup with station name, current $SWE$, Percent of Median/status, elevation, and basin; selecting the popup opens that station's detail panel.

- **Summary KPI Cards:** Statewide or selected-basin average $SWE$ (in), average Percent of Median (%), active station count ($n$), and the highest current SWE reading (in) among stations remaining after the active filters, with station name.

- **Station Detail Panel & Time-Series Plot (Chart.js):** Displays selected station name, ID, basin, elevation (ft), current $SWE$ (in), snow depth (in), snow density (%), $\Delta SWE$ (in), and a water-year hydrograph comparing the current year's $SWE$ curve against the 1991–2020 median curve. Show gaps for missing observations; do not interpolate them or replace them with zero. When no station is selected, keep KPI cards visible, show a “Select a station” prompt, and hide the station-specific chart.

- **Sortable Station Data Table:** Columns for Station Name, Basin, Elevation (ft), Current $SWE$ (in), Median $SWE$ (in), % of Median, and Status. Status uses the same Percent-of-Median categories as map markers; show `N/A` when the median comparison is unavailable. Default sort: Percent of Median ascending, with `N/A` values last.

## 5. Look and Feel

- **Desktop Layout:** Clean two-column dashboard with a top header bar containing the title and global filters (Basin, Date, Elevation, Metric Toggle); the left 60% shows the interactive map with a floating legend; the right 40% stacks KPI summary cards above the selected station's SWE time-series chart, with the sortable station table below.
- **Initial View on Load:** Center on Utah (latitude 39.3, longitude −111.7, zoom 7) and show all active Utah SNOTEL sites colored by Percent of 1991–2020 Median for the most recent available date, with statewide summary metrics populated and no station selected.
- **Mobile / Phone Behavior:** Below 768 px wide, use a single-column order of filters, map, KPI cards, selected-station details/chart, and table. Collapse the filter bar into a stacked group, resize the map to 50vh with touch-friendly markers, and allow horizontal table scrolling without breaking page width.

## 6. Validation

- **Hand-Worked Illustrative Test Case (Trial Lake SNOTEL — Site 828; values are illustrative, not a verified observation):**
  - **Inputs:**
    - $SWE_{\mathrm{current}} = 24.6\ \mathrm{in}$
    - $SWE_{\mathrm{median}} = 20.5\ \mathrm{in}$
    - $D_{\mathrm{snow}} = 72.0\ \mathrm{in}$
  - **Expected Outputs:**
    - $P_{\mathrm{med}} = \frac{24.6}{20.5} \times 100 = 120.0\%$
    - $\Delta SWE = 24.6 - 20.5 = +4.1\ \mathrm{in}$
    - Density (%) $= \frac{24.6}{72.0} \times 100 = 34.2\%$ ($\rho_{\mathrm{snow}} = 21.3\ \mathrm{lb/ft^3}$)
    - **Marker Color Category:** Light Blue (Above Normal, since $110\% \le 120.0\% < 130\%$)

- **Synthetic Three-Station Basin-Average Test:** Treat all stations as active, non-null, and in the same selected basin, elevation filter, and date.
  - **Inputs and Per-Station Percent of Median:**
    - Station A: $SWE_{\mathrm{current}} = 10\ \mathrm{in}$, $SWE_{\mathrm{median}} = 8\ \mathrm{in}$, $P_{\mathrm{med}} = 125\%$
    - Station B: $SWE_{\mathrm{current}} = 20\ \mathrm{in}$, $SWE_{\mathrm{median}} = 20\ \mathrm{in}$, $P_{\mathrm{med}} = 100\%$
    - Station C: $SWE_{\mathrm{current}} = 30\ \mathrm{in}$, $SWE_{\mathrm{median}} = 40\ \mathrm{in}$, $P_{\mathrm{med}} = 75\%$
  - **Expected Basin Averages:**
    - Average SWE: $(10 + 20 + 30) / 3 = 20\ \mathrm{in}$
    - Average Percent of Median: $(125 + 100 + 75) / 3 = 100\%$

## 7. Out of Scope

- Streamflow runoff volume forecasting or reservoir routing models (e.g., acre-feet inflow predictions).
- Avalanche danger ratings or slope-aspect stability modeling.
- User accounts, custom data uploads, or backend server databases; everything runs client-side in a single `index.html` file.
- SNOTEL stations located outside Utah, including those in multi-state border basins such as Bear River.
