# Prompt log

## 1

> Set up the folders for this project, a single-file web app for Problem 6 (Utah Snowpack Map). Put `AGENTS.md`, `spec.md`, `prompts.md`, and `index.html` at the top level. Create numbered folders for supporting files: `00_planning` for notes, sketches, and feature ideas; `01_data` for data files; `02_validation` for hand calculations and test cases; and `03_output` for screenshots and exported results. Put a short `README.md` in each numbered folder explaining what belongs there, and document the folder layout and file-placement rules in `AGENTS.md`. Also include the standing instruction in `AGENTS.md` to log every prompt I give you in `prompts.md` (and make sure `prompts.md` exists). Don't build the app yet.

## 2

> Create an AGENTS.md at the top level of this project containing these two lines: "After each request, add an entry to prompts.md: what I asked, what you changed, and whether it worked." and "After each request, commit all changes with a clear message." Then commit. Don't build anything else.

- Changed: Added the two requested instructions to `AGENTS.md` and recorded this prompt.
- Worked: Yes; verified the requested instructions and log entry, and included the project changes in the requested commit.

## 3

> dont build anything - fix the format of the calculations info in the spec

- Changed: Reformatted the calculations section in `spec.md` into readable Markdown lists and equations; no app code was built.
- Worked: Yes; the calculations are now consistently formatted and will be included in the requested commit.

## 4

> yeah! should be like this

> Reference: attached screenshot showing numbered heading, bullet descriptions, and typeset inline/display equations.

- Changed: Matched the calculations section in `spec.md` to the screenshot's numbered heading, bullet layout, and typeset equations.
- Worked: Yes; verified the section formatting and included the change in the requested commit.

## 5

> make the outputs look like this

> Reference: attached screenshot showing the numbered Outputs heading and four bulleted output descriptions.

- Changed: Reformatted the Outputs section in `spec.md` to match the screenshot.
- Worked: Yes; verified the section content and formatting, and included the change in the requested commit.

## 6

> add this to validation

> Reference: attached screenshot showing a hand-worked Trial Lake test case and multi-station basin-average check.

- Changed: Added the screenshot's hand-worked inputs, expected calculations, marker color, and basin-average check to Validation in `spec.md`.
- Worked: Yes; verified the listed calculations and included the change in the requested commit.

## 7

> look at the spec and make all of the sections the same style

- Changed: Standardized the spec's numbered section headings, bold-labeled bullet lists, and section spacing while preserving its requirements.
- Worked: Yes; the sections now follow one consistent structure and will be included in the requested commit.

## 8

> I have drafted my initial `spec.md` for the Utah Snowpack Map app, including my hand-worked validation case under Validation. Review `spec.md` to confirm all seven required sections are present without rewriting my engineering equations or changing my validation numbers. Stage and commit the project setup and first draft of `spec.md` with a clear commit message.

- Changed: Reviewed the seven numbered sections and confirmed the hand-worked inputs and expected results are unchanged. No `spec.md` edits were needed because the project setup and draft are already committed.
- Worked: Yes; the project setup is in `692ea3c` and the full draft is in `ca0958d`. This review prompt is recorded here.

## 9

> Read `spec.md` carefully. Do not write any application code yet. Tell me what is unclear, ambiguous, or missing across the seven sections for a Utah snowpack map web app, and list questions I should answer before we build.

- Changed: Reviewed all seven sections and recorded the request; no application code or spec changes were made.
- Worked: Yes; the review findings and questions are provided in the response.

## 10

> what should we build? necause of this

- Changed: Prepared a focused v1 recommendation based on the open decisions in `spec.md`; no application code or spec changes were made.
- Worked: Yes; the recommended scope and decisions are provided in the response.

## 11

> https://wcc.sc.egov.usda.gov/awdbRestApi/swagger-ui/index.html

- Changed: Reviewed the AWDB REST API documentation; no application code or spec changes were made.
- Worked: Yes; verified station metadata, data retrieval, and 30-year median support in the API description.

## 12

> https://www.nrcs.usda.gov/conservation-basics/conservation-by-state/utah/utah-snow-survey

- Changed: Checked the Utah Snow Survey page URL; no application code or spec changes were made.
- Worked: The supplied URL returned 404 during review; this is noted for follow-up.

## 13

> give me questions for things to change and give suggestions, ill pick the thing i want until our spec is clear

- Changed: Started an iterative spec-clarification process with a recommended first decision; no spec or application-code changes were made.
- Worked: Yes; the first decision is presented for the user to choose.

> Fixed 1991–2020.

- Changed: Recorded the fixed 1991–2020 baseline in `spec.md` and aligned chart references; flagged that the AWDB median field must be verified against that period.
- Worked: Yes; the baseline is now consistent across the spec.

> dynamic_visible_range

- Changed: Specified that Current SWE marker colors use the filtered visible stations' SWE range and that the legend updates accordingly.
- Worked: Yes; the raw-SWE marker scale is now defined in the spec.

> statewide_summary

- Changed: Set the initial station state to statewide summary with no station selected.
- Worked: Yes; the initial selection behavior is now explicit in the spec.

> valid_per_metric

- Changed: Defined the active station count and metric-specific average eligibility, including handling for missing or zero medians.
- Worked: Yes; KPI inclusion rules are now explicit in the spec.

> date_picker_latest_available

- Changed: Specified a date picker limited to dates with AWDB data, defaulting to the latest date; the selected date determines the water-year chart window.
- Worked: Yes; date-control and default behavior are now explicit in the spec.

> continuous_unrounded

- Changed: Defined continuous marker bands using the unrounded Percent of Median value, with no gaps between thresholds.
- Worked: Yes; every numeric Percent of Median value now falls into a defined color category.

> preserve_fixed_baseline

- Changed: Specified that AWDB medians are used only if they match 1991–2020; otherwise, the app must source or calculate the matching baseline.
- Worked: Yes; the fallback preserves the chosen baseline rather than silently substituting another period.

> utah_only

- Changed: Limited included SNOTEL stations to locations physically within Utah, including for border basins.
- Worked: Yes; geographic scope is now explicit.

> all_station_basins

- Changed: Replaced the open-ended basin list with all basins represented by included Utah SNOTEL stations and required a canonical station-to-basin mapping.
- Worked: Yes; the filter scope no longer relies on an unspecified “etc.” list.

> online_direct_api

- Changed: Specified an online-only client-side app that calls AWDB directly and loads map/chart libraries from a CDN, subject to CORS verification.
- Worked: Yes; the runtime assumption is now explicit.

> chartjs

- Changed: Selected Chart.js for the water-year SWE chart and named it in the runtime and output requirements.
- Worked: Yes; the charting library is now specified.

> filtered_selected_date

- Changed: Defined the peak KPI as the highest current SWE among stations remaining after filters on the selected date, and to include its station name.
- Worked: Yes; the peak KPI scope is now explicit.

> global_clear_excluded

- Changed: Specified that filters apply across all views and clear a station selection if it becomes excluded.
- Worked: Yes; filter interaction behavior is now explicit.

> same_percent_median_bands

- Changed: Defined the table Status column to use the map's Percent-of-Median categories and show `N/A` when unavailable.
- Worked: Yes; table status behavior now matches the map legend.

> percent_median_ascending

- Changed: Set the station table's default sort to Percent of Median ascending, with unavailable values last.
- Worked: Yes; the initial table order is now specified.

> display_na

- Changed: Specified that snow density displays as `N/A` when snow depth is missing or non-positive.
- Worked: Yes; the density edge case now has explicit display behavior.

> compact_station_summary

- Changed: Specified the marker popup fields and that selecting a popup opens the station detail panel.
- Worked: Yes; map popup content and behavior are now explicit.

> show_gaps

- Changed: Specified that missing hydrograph observations appear as gaps rather than zeroes or interpolated values.
- Worked: Yes; missing chart-data behavior is now explicit.

> same_water_year_day

- Changed: Aligned 1991–2020 median comparisons and the chart to the same day of water year, using available historical observations.
- Worked: Yes; the comparison period and date alignment are now specified.

> awdb_plus_curated

- Changed: Specified AWDB station metadata, including HUC codes, as mapping input and a curated HUC-to-basin mapping for canonical names and missing codes.
- Worked: Yes; basin membership now has a defined source/fallback.

> visible_error_retry

- Changed: Specified a visible AWDB error and retry state, with no zero-value or success-shaped fallback.
- Worked: Yes; external data failure behavior is now explicit.

> synthetic_three_station

- Changed: Added a fixed three-station synthetic basin-average validation case with hand-worked expected averages.
- Worked: Yes; the average calculations are reproducible and distinguish mean station percentages from a ratio of means.

> Accepted the no-current-reading form without selecting a value; used the recommended default, `show_na_neutral`.

- Changed: Specified that active stations with no current reading remain visible with a neutral marker and `N/A`, but are excluded from counts and averages.
- Worked: Yes; missing-current-reading visibility is explicit.

> map_first

- Changed: Specified the mobile content order as filters, map, KPIs, selected-station details/chart, then table.
- Worked: Yes; mobile stack order is now clear.

> keep_as_illustrative

- Changed: Labeled the Trial Lake hand-worked case as illustrative and removed the unverified elevation claim, without changing its calculation inputs or results.
- Worked: Yes; the example no longer implies the values are a verified observation.

> selection_prompt

- Changed: Specified that an unselected detail panel shows “Select a station” while KPIs remain visible and the station-specific chart is hidden.
- Worked: Yes; the no-selection state is now defined.

> daily_all

- Changed: Specified daily AWDB data consistently for current measurements, historical medians, and all views.
- Worked: Yes; data resolution is now explicit.

## 14

> Read `spec.md`. Don't write any code. Write a short overview of the whole app, then suggest how to build it in 4 to 6 stages, starting with a mockup of the page layout. For each stage, tell me what will be built and what I should check when it's done.

- Changed: Prepared a six-stage build outline beginning with a static layout mockup; no application code or spec changes were made.
- Worked: Yes; each stage includes its build scope and completion checks.

## 15

> Add the short overview to the top of `spec.md` and add the agreed build stages under `## Build stages` at the end of `spec.md`. Do not write `index.html` yet. Commit this updated `spec.md`.

- Changed: Added the overview and six build stages to `spec.md`; left `index.html` untouched.
- Worked: Yes; the documentation changes are verified and committed.

## 16

> Build stage 1 from the `Build stages` section of `spec.md`. Only build this stage.

- Changed: Created a static responsive layout mockup in `index.html` with visual-only filters, a map placeholder, empty KPI cards, station-detail/chart placeholders, and an empty station table. No data fetching, calculations, or working filters were added.
- Worked: Yes; opened the page in a browser and verified the desktop two-column proportions, mobile stacking order, and absence of horizontal page overflow.

## 17

> I've checked Stage 1 in the browser and [describe any tweaks made or confirm it matches what you want]. Commit Stage 1 to Git.

- Changed: No additional UI tweaks were specified. Stage 1 was already committed as `56bd68a`; recorded this review and commit request.
- Worked: Yes; confirmed the Stage 1 commit is present and the worktree had no pending changes.

## 18

> build stage 2 to scheck

- Changed: Connected the page to AWDB active Utah SNOTEL metadata and current-water-year daily SWE, snow-depth, and median fields; mapped HUC-8 codes to USGS watershed names; added visible loading, failure, retry, and coverage states. Percent-of-Median remains uncalculated because AWDB does not identify the median's reference years.
- Worked: Yes; browser CORS and live loading succeeded for 141 stations (latest data date: 2026-11-23). Simulated a failed request and confirmed the error/retry flow recovers. The 1991–2020 baseline still needs verification or calculation in a later stage.

## 19

> in order build step 3,4,5 and 6, and show it to me after each one for me to check

- Changed: Recorded the requested stage-by-stage review workflow. I will stop after Stage 2 and wait for your check before starting Stage 3; later stages will likewise be shown one at a time.
- Worked: Pending your Stage 2 review.

## 20

> Let's validate the app against my hand calculation in `spec.md` (inputs: [paste exact validation inputs]; expected outputs: [paste exact expected outputs]). Walk through how the app computes those values so I can verify them in the UI, save my validation notes/results in `02_validation/`, and commit the validated version to Git.
>
> Here are two worked validation cases—one single-station check and one multi-station basin average check—using the exact equations from your spec so you can compare them directly against what your app displays in VS Code.
>
> **Case 1: Trial Lake SNOTEL**
>
> Inputs: current SWE = 24.6 in; median SWE = 20.5 in; snow depth = 72.0 in; liquid-water density = 62.4 lb/ft³.
>
> Expected: Percent of Median = (24.6 / 20.5) × 100 = 120.0%; SWE anomaly = 24.6 − 20.5 = +4.1 in; density = (24.6 / 72.0) × 100 = 34.167% ≈ 34.2%; bulk density = (24.6 / 72.0) × 62.4 = 21.32 ≈ 21.3 lb/ft³; Above Normal (Light Blue).
>
> **Case 2: supplied three-station basin check**
>
> Inputs: A = 18.0 in SWE, 20.0 in median, 60.0 in depth, 90.0%; B = 12.0 in SWE, 15.0 in median, 48.0 in depth, 80.0%; C = 27.0 in SWE, 25.0 in median, 80.0 in depth, 108.0%.
>
> Expected: average SWE = 19.0 in; average median SWE = 20.0 in; mean of station percentages = 92.667% ≈ 92.7%; ratio of basin means = 95.0%; mean SWE anomaly = −1.0 in. The prompt asks to confirm which Percent-of-Median aggregation the app uses.
>
> Edge cases: zero median must show N/A for Percent of Median; zero or missing snow depth must show N/A for density.

- Clarification: Build Stage 3 calculations now, add an in-app validation panel, and include the supplied basin test as an additional case without replacing the existing spec test.
- Changed: Added shared metric and basin-summary calculations, a labeled UI panel that computes the Trial Lake, existing spec, and supplemental basin cases, live SWE summary outputs, missing-value handling, and threshold checks. Saved hand calculations and browser results in `02_validation/stage_3_calculation_results.md`. Live Percent of Median stays unavailable because the AWDB median period is unverified.
- Worked: Yes; the browser panel reports 24 passing calculation, missing-value, and threshold checks. The supplied basin mean-of-station-percentages result is 92.7%; 95.0% is shown as a comparison only.

## 21

> keep validating

- Clarification: Stage 4 was selected; build only the map and global filters, then pause for review.
- Changed: Added a Leaflet Utah station map, AWDB-derived basin/date/elevation filters, a Percent of Median / Current SWE toggle, a data-scaled SWE legend, neutral markers while the median period remains unverified, station popups and selection, and synchronized KPI/table/detail updates. Kept map/data loading failures visible.
- Worked: Yes; live browser testing loaded 141 stations, verified all filters and selection clearing, confirmed the statewide map and station popup, and found no horizontal overflow at 375 px.

## 22

> is the app done?

- Changed: No application code. Clarified that Stage 4 is complete, while Stages 5 and 6 remain.
- Worked: Yes; also noted the 1991–2020 median period is still unverified, so live median comparisons remain unavailable.

## 23

> would any of this help? how can we get this app continuing

- Changed: Reviewed the attached AWDB Swagger screenshot and OpenAPI schema, then continued with Stage 5: added the Chart.js water-year SWE hydrograph, omitted the unverified median curve with an explicit note, implemented sortable table columns with Percent of Median ascending and N/A last by default, and made the station count reflect the filtered active stations.
- Worked: Yes; live browser checks confirmed the chart, date updates, sorting, station selection, 140 filtered stations, no console errors, and no mobile page overflow. The API documents a generic 30-year median but does not identify its reference years; Stage 6 remains.

## 24

> finish the app!

- Changed: Completed Stage 6 responsive and end-to-end validation, fixed the stale map data-error message after a successful retry, marked the app complete, and clarified that 1991–2020 comparisons remain withheld until the AWDB median reference period is verified.
- Worked: Yes; verified live AWDB load and recovery after a simulated outage, filters and no-data state, chart and station selection, mobile layout with no page overflow and a horizontally scrollable table, and all 24 calculation checks.

## 25

> wha5 do 6ou need now? the naomoly is still blank

- Changed: Traced the unavailable anomaly to the app withholding AWDB's unspecified 30-year median, checked that raw historical daily SWE can support a fixed baseline, and asked which baseline to use.
- Worked: Yes; confirmed the source path and received the choice to preserve 1991–2020.

## 26

> preserve_1991_2020

- Changed: Calculated daily medians from available AWDB observations in water years 1991–2020, connected them to the map, KPIs, station details, and chart, and showed the selected date's contributing-water-year count. Clarified the baseline window and data method in `spec.md`.
- Worked: Yes; live AWDB loaded 141 stations and calculated a median for 132 on Nov 23, 2026. Lakefork #3 (1116:UT:SNTL) now displays `+0.8 in` anomaly (`1.8 − 1.0`), based on 11 of 30 available water years. Date changes update the anomaly, mobile layout remains overflow-free, and all 27 calculation checks pass.

## 27

> this validation does not need to be in the app nor does the data

- Changed: Removed the in-app calculation validation fixtures and live station data table, including their unused rendering, sorting, fixture, and responsive styles.
- Worked: Yes; local verification confirmed the page loads and the removed section names and fixture/sorting code are absent.

## 28

> clean up my two suggested features in planning

- Changed: Replaced the rough planning notes with a clean, structured description of the Ski Recommendation Finder and Selected-Station Snowflake Highlight features, preserving their inputs, calculations, outputs, behavior, and constraints.
- Worked: Yes; verified both suggestions are now clearly formatted in `00_planning/README.md`.
