# Problem 6: Utah Snowpack Map

## 1. Purpose

- **Overview:** Map the SNOTEL snow-monitoring sites in Utah and show how this year's snowpack compares to normal.
- **Audience:** Water resource engineers, hydrologists, municipal water planners, and backcountry recreationists evaluating Utah's spring runoff potential and drought/flood status.

## 2. Inputs

- **Basin / Watershed Filter:** Dropdown selector. Options include All Utah Basins, Bear, Weber, Provo–Utah Lake–Jordan, Duchesne, Price–San Rafael, Sevier, and Virgin. Default: All Utah Basins. Include only stations located within Utah.
- **Target Date:** Date picker limited to dates with available AWDB data. Default: the latest available date. The selected date determines the water year (October 1–September 30) for the time-series window.
- **Minimum Elevation Filter:** Slider or numeric box in feet. Range: 6,000–11,500 ft; step: 250 ft; default: 6,000 ft.
- **Station Selection:** Select a SNOTEL marker on the map or choose a station from a searchable dropdown/list. Default: statewide summary with no station selected.
- **Display Metric Toggle:** Radio buttons to color-code map markers by Current SWE (in) or Percent of 1991–2020 Median (%). Default: Percent of Median.

## 3. Calculations

- **Snow Water Equivalent ($SWE$, in):** Depth of liquid water contained in the snowpack, retrieved from NRCS SNOTEL ($WTEQ$ sensor) in inches (in).

- **Historical Baseline:** Use the fixed 1991–2020 period for median comparisons. Use the AWDB median field only if its baseline matches; otherwise, source or calculate 1991–2020 medians rather than substituting an unspecified 30-year median.

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

- **Basin Average SWE & Percent of Median:** Compute the arithmetic mean of current SWE over stations with a non-null current SWE value, and the arithmetic mean of $P_{\mathrm{med}}$ over stations with a valid $P_{\mathrm{med}}$, within the selected basin and elevation filter.

- **Station Inclusion for Counts and Averages:** Count stations with a non-null current SWE value for the selected date. Calculate each average using only stations with valid values for that metric. A missing or zero median makes $P_{\mathrm{med}}$ `N/A` and excludes that station from the Percent of Median average, but not from the current-SWE average or station count.

- **Marker Status Thresholds (Color Rules):**
  - Classify using the unrounded $P_{\mathrm{med}}$ value.
  - $P_{\mathrm{med}} < 70\%$: Red (Well Below Normal)
  - $70\% \le P_{\mathrm{med}} < 90\%$: Orange (Below Normal)
  - $90\% \le P_{\mathrm{med}} < 110\%$: Green (Near Normal)
  - $110\% \le P_{\mathrm{med}} < 130\%$: Light Blue (Above Normal)
  - $P_{\mathrm{med}} \ge 130\%$: Dark Blue / Purple (Well Above Normal)

- **Current SWE Color Scale:** When Current SWE is selected, use a sequential color scale based on the minimum and maximum SWE values of the currently visible stations. Update the legend to show that range.

## 4. Outputs

- **Interactive Map (Leaflet):** Utah map showing color-coded circular station markers, clickable popups, and a color-scale legend.

- **Summary KPI Cards:** Statewide or selected-basin average $SWE$ (in), average Percent of Median (%), active station count ($n$), and peak station reading (in).

- **Station Detail Panel & Time-Series Plot (Chart.js / Plotly):** Displays selected station name, ID, basin, elevation (ft), current $SWE$ (in), snow depth (in), snow density (%), $\Delta SWE$ (in), and a water-year hydrograph comparing the current year's $SWE$ curve against the 1991–2020 median curve.

- **Sortable Station Data Table:** Columns for Station Name, Basin, Elevation (ft), Current $SWE$ (in), Median $SWE$ (in), % of Median, and Status.

## 5. Look and Feel

- **Desktop Layout:** Clean two-column dashboard with a top header bar containing the title and global filters (Basin, Date, Elevation, Metric Toggle); the left 60% shows the interactive map with a floating legend; the right 40% stacks KPI summary cards above the selected station's SWE time-series chart, with the sortable station table below.
- **Initial View on Load:** Center on Utah (latitude 39.3, longitude −111.7, zoom 7) and show all active Utah SNOTEL sites colored by Percent of 1991–2020 Median for the most recent available date, with statewide summary metrics populated and no station selected.
- **Mobile / Phone Behavior:** Use a single-column vertical stack below 768 px wide. Collapse the filter bar into a stacked group, resize the map to 50vh with touch-friendly markers, and allow horizontal table scrolling without breaking page width.

## 6. Validation

- **Hand-Worked Test Case (e.g., Trial Lake SNOTEL — Site 828, Elevation 9,992 ft, Provo–Utah Lake–Jordan Basin):**
  - **Inputs:**
    - $SWE_{\mathrm{current}} = 24.6\ \mathrm{in}$
    - $SWE_{\mathrm{median}} = 20.5\ \mathrm{in}$
    - $D_{\mathrm{snow}} = 72.0\ \mathrm{in}$
  - **Expected Outputs:**
    - $P_{\mathrm{med}} = \frac{24.6}{20.5} \times 100 = 120.0\%$
    - $\Delta SWE = 24.6 - 20.5 = +4.1\ \mathrm{in}$
    - Density (%) $= \frac{24.6}{72.0} \times 100 = 34.2\%$ ($\rho_{\mathrm{snow}} = 21.3\ \mathrm{lb/ft^3}$)
    - **Marker Color Category:** Light Blue (Above Normal, since $110\% \le 120.0\% \le 129\%$)

- *(Plus a multi-station basin average check with 2–3 stations to verify your basin aggregation math.)*

## 7. Out of Scope

- Streamflow runoff volume forecasting or reservoir routing models (e.g., acre-feet inflow predictions).
- Avalanche danger ratings or slope-aspect stability modeling.
- User accounts, custom data uploads, or backend server databases; everything runs client-side in a single `index.html` file.
- SNOTEL stations located outside Utah, including those in multi-state border basins such as Bear River.
