# Problem 6: Utah Snowpack Map

## Status

## Purpose
map of the SNOTEL snow-monitoring sites in Utah that shows how this year's snowpack compares to normal.
Water resource engineers, hydrologists, municipal water planners, and backcountry recreationists evaluating Utah's spring runoff potential and drought/flood status.

## Inputs (values, units, ranges, defaults, controls)
Basin / Watershed Filter: Dropdown selector (Options: All Utah Basins, Bear, Weber, Provo–Utah Lake–Jordan, Duchesne, Price–San Rafael, Sevier, Virgin, etc.; Default: All Utah Basins).

Target Date / Water Year Selector: Date picker or water-year dropdown (Range: Oct 1 of selected water year to current date; Default: Today's latest reading).

Minimum Elevation Filter: Slider or numeric box in feet ( Range: 6000ft6,000ftto11500 ft11,500 ft, Step: 250ft250 ft, Default: 6,000ft 6,000 ft).

Station Selection: Clicking a SNOTEL marker on the map or selecting a station from a searchable dropdown/list (Default: Highest-SWE station or state summary).

Display Metric Toggle: Radio buttons to color-code map markers by either Current SWE (in) or Percent of 1991–2020 Median (%) (Default: Percent of Median).
## Calculations (equations, thresholds/rules, data processing, all variables & units defined)

- **Snow Water Equivalent (`SWE`, in):** Depth of liquid water contained in the snowpack, retrieved from the NRCS SNOTEL WTEQ sensor. The value is in inches.

- **Percent of Normal / Median (`P_median`, %):**

  ```text
  P_median = (SWE_current / SWE_median) × 100
  ```

  If `SWE_median = 0` (including early- or late-season cases), display `N/A` instead of dividing by zero.

- **SWE Anomaly (`ΔSWE`, in):**

  ```text
  ΔSWE = SWE_current − SWE_median
  ```

- **Estimated Snow Density (`ρ_snow`, % or lb/ft³):** When snow depth (`D_snow`, in) is available and greater than zero:

  ```text
  Density (%) = (SWE_current / D_snow) × 100
  ρ_snow (lb/ft³) = (SWE_current / D_snow) × 62.4 lb/ft³
  ```

- **Basin Average SWE and Percent of Median:** Arithmetic means of `SWE_current` and `P_median` across all active, non-null stations within the selected basin and elevation filter.

- **Marker Status Thresholds (Color Rules):**
  - `<70%`: Red (Well Below Normal)
  - `70% to 89%`: Orange (Below Normal)
  - `90% to 109%`: Green (Near Normal)
  - `110% to 129%`: Light Blue (Above Normal)
  - `≥130%`: Dark Blue / Purple (Well Above Normal)

## Outputs (numbers with units, tables, plots, diagrams)

## Look and feel (layout, initial view on load, mobile/phone behavior)

## Validation (at least one hand-worked case with exact inputs and expected outputs)

## Out of scope
