# Planning

Store project notes, sketches, and feature ideas in this folder.

## Suggested features

### Ski recommendation finder

**Inputs**

- Utah city selector with coordinates for Provo, Salt Lake City, Orem, Ogden, Logan, Park City, Heber City, St. George, Cedar City, Vernal, and Price.
- Default city: Provo.

**Calculations**

- Calculate straight-line distance from the selected city to each Utah ski resort's paired SNOTEL station, or to the nearest active SNOTEL station.
- Use the Haversine formula with an Earth radius of 3,958.8 miles.
- Keep the 10 closest locations.
- Rank the first-place recommendation by the highest current SWE, using Percent of Median as a tie-breaker.

**Outputs**

- Recommendation card for the top pick, showing station name, distance, current SWE, snow depth, and Percent of Median.
- Ranked list of the 10 closest locations.
- Hand-worked validation case for Provo.

### Selected-station snowflake highlight

**Behavior**

- When a station is selected from the map or ski recommender, highlight it on the Leaflet map with a snowflake ring or icon.
- Start one 5-second snowfall-wave animation inside the map container.

**Constraints**

- Use `pointer-events: none` for the snowfall overlay so map panning and marker clicks continue to work.
- Cleanly stop and restart the animation if another station is selected during the wave.