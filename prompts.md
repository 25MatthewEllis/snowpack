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
