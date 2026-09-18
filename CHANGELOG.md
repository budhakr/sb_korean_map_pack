# Changelog — Korean Maps Pack

---

## v0.4.0

### New Maps

- **Jeonju–Gunsan–Iksan combined map (CHN)** — a single 92km×71km map covering all three cities, joining the pack as the 16th city.

### New Demand Data

- **2024 KTDB baseline data** — every city's O/D travel demand has been regenerated from the newly released 2024 reference-year dataset (previously 2023).
- **5 new Minor POI demand categories** on every map — schools, parks, shopping centers, tourist attractions, and ferry terminals, each estimated from real facility-level statistics (student counts, retail floor area, visitor stats, port passenger records) rather than population alone.
- **Consistent English romanization on place labels** — fixed roughly 46 district-level (구) labels across 12 cities that previously fell back to Korean-only due to a naming-format mismatch in the source administrative data.

### Improvements

- **Simpler in-game map names** — dropped the redundant size suffix (e.g. "Gangneung 40km*40km") from every map's display name.
- **Faster map generation** — nationwide airport data is now fetched once instead of separately for every city, and driving-route cache size per city is reduced 20-300x.

### Bug Fixes

- **Regenerated demand for several cities that was silently built from the wrong source** — a 2-month-old regression could cause a city's travel demand to be generated from an unintended data source under specific conditions; affected cities were identified and regenerated from the correct source.

- **Fixed a resident-count mismatch on many maps** — demand routed through POI-based arrival points (train stations, airports, tourist attractions, etc.) wasn't being counted toward that point's resident total, which could surface as an in-game "resident totals mismatch" warning.

- **Jeonju–Gunsan–Iksan, Cheongju, Daejeon, Sejong: missing buildings in the Chungnam-region portion of the map** — a data-provider export limit silently capped Chungnam-region buildings at 1,000,000, dropping the overflow. Fixed by reading the provider's separate overflow file.

- **Fixed generation crashes (out of memory) for large, multi-province cities and for the new Jeonju–Gunsan–Iksan map.**

---

## v0.3.1

### New Maps

- **6 new minor cities** — Suwon, Cheongju, Changwon, Gyeongju–Pohang, Gangneung, and Chuncheon join the pack, each shipping as a single map at its largest size.
- **Gyeongju–Pohang 50km dual-city composite** — a single large map covering both cities, bounded by the southwest corner of a Gyeongju-centered 40km box and the northeast corner of a Pohang-centered 30km box.

### Map Changes

- **One map per city, going forward** — every city now ships only its largest size variant. Jeju now ships only as the Full Island map (CJUF); the separate Jeju 30km/40km maps are removed.
- **Map codes no longer carry a size suffix** — e.g. `SEL4` is now just `SEL`. Since every city ships a single map, the size letter is no longer needed to tell maps apart. If you have an existing save built on an old-style code, re-download the map under its new code.

### Improvements

- **More accurate rivers, lakes, and green space on every map**
  Water and land-cover data now comes from official government surveys (National Geographic Information Institute stream/lake data, Ministry of Environment land-cover maps) instead of crowdsourced OSM data, improving the shape and coverage of rivers, lakes, parks, and other green areas across the whole pack.
- **Low-rise buildings restored on every map** — a density filter that thinned out low-rise buildings (previously disabled for Seoul only) has now been turned off everywhere, so every city shows its full building footprint like Seoul does.
- **Smaller download size** — per-pop driving routes are now stored in a separate file instead of being duplicated inside the main demand file, shrinking most map packages noticeably.
- Added game-version compatibility metadata and richer per-map statistics (commute time/distance/speed distributions, demand-point categorization) to each map's info file.

### Bug Fixes

- **Stations could fail to place in certain areas of a map**
  A small number of duplicate, zero-length points in the road data could make the game's nearest-point lookup fail, silently blocking station placement in that spot. Cleaned up the road geometry pipeline to remove these; verified fixed in-game.

- **Gwangju (KWJ): 3D buildings were missing across the entire map**
  A regional boundary re-code (following the Jeolla-Gwangju administrative merger) left Gwangju's building data pointing at a folder that no longer existed, so building extraction silently skipped it and shipped an empty building layer. Fixed by updating the map to the correct region codes — Gwangju's ~252,000 buildings are back.

- **Coastal cities were missing the ocean entirely** — Gangneung, Ulsan, and other coastal maps rendered their landmass but not the surrounding sea. Fixed by adding the terrain and seabed-depth layers the game expects alongside the water layer.

---

## v0.2.0

### New Features

- **Special Demand Points — Train Stations, Bus Terminals, Airports, Universities, Hospitals**
  Maps now include demand points for major transit hubs and facilities that generate large-scale travel demand.
  - **KTX / SRT stations:** Passengers travelling to and from high-speed rail stations are now reflected as demand. The volume is based on actual 2024 daily boarding/alighting figures.
  - **Intercity & express bus terminals:** Bus terminal demand added using actual 2024 ridership data (349 terminals nationwide, ≥100 passengers/day).
  - **Airports:** Passenger demand distributed proportionally to the surrounding population catchment area. Both large international airports and small regional airports are covered (14 airports total).
  - **Universities:** Commuting students generate inbound demand scaled by actual enrollment, dormitory capacity, and the age distribution of the surrounding population. (208 universities)
  - **Hospitals:** Patient visits generate inbound demand. Tertiary hospitals draw from a wider regional catchment (up to 150 km); general hospitals are more locally focused. Demand is weighted by real age-specific healthcare utilization rates from 2024 national health insurance statistics. (385 hospitals)

  These facilities appear as dedicated demand points on the map. Your subway needs to serve them to capture their ridership.

### Improvements

- **More complete base demand — all trip purposes included**
  The underlying travel demand now accounts for all trip purposes (commute, school, business, return home, and other), not just commuting and school trips. This brings the total demand density back up to the level of v0.1.1.

- **Demand now reflects actual population distribution at the neighborhood level**
  Travel demand points are distributed using 2026 resident registration data (행정동-level, all age groups), giving a more accurate picture of where people actually live.

- **Demand density tuned per city**
  A scaling factor is applied per city to calibrate total demand to realistic levels. Seoul and Incheon are scaled at 0.8×; all other cities at 1.0×.

### Bug Fixes

- **Jeju Full Island (CJUF): POI demand was completely missing**
  Due to a configuration error, special demand points (airport, university, hospitals) were generating no demand at all on the Jeju Full Island map. This has been fixed — Jeju now correctly shows POI demand including Jeju International Airport.

- **Seoul 40km (SEL4): western boundary adjusted**
  The western edge of the SEL4 map has been trimmed back by ~1 km to its original boundary.

- **Demand points on water (rivers/lakes) were causing demand loss**
  Demand points that landed on rivers or lakes are now correctly redistributed to the nearest land-based point, preventing silent demand loss.

---

## v0.1.1

### Bug Fixes

- **Fixed lag caused by empty worker list**
  Workplace demand points were displaying an empty worker list in the detail panel, causing a recurring performance lag every 15 minutes during gameplay. Fixed.

- **Fixed Yeouido park rendering error**
  The interior of Yeouido Island was incorrectly rendered as a park due to a multipolygon handling bug in the greenery layer. Fixed.

### Improvements

- **More realistic demand distribution**
  Reduced demand concentration at single points; distribution now better reflects actual population spread.

- **Travel time calculated using real road network (OSRM)**
  Commuter travel times are now calculated using the actual road network instead of straight-line distance estimates.

- **Demand points on water removed**
  Demand points located on rivers or lakes are detected and their demand is redistributed to nearby land-based points.
