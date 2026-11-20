# Riverwood Preserve: Photo-Calibrated Habitat Map

Interactive habitat map of Westerly Land Trust's Riverwood Preserve, Westerly, Rhode Island (RIGIS tax lots WY 50-6 and 50-8; 153.9 GIS acres, which WLT lists as 148 acres) and the adjoining 4.5-acre lot WY 39-37, which by size and location is likely Camp Quequatuck. Built by PPLT AGIKS (Pocasset Pokanoket Land Trust, Indigenous Stewardship Program) with parcelmap v0.1 from a 19 November 2026 site visit, 2022 USGS 3DEP lidar and RIGIS imagery.

It is a static site with no build step. Leaflet 1.9.4 is bundled in `lib/`.

## Publish with GitHub Pages

1. Put the contents of this folder at the root of the repository, so `index.html` and `.nojekyll` are at the top level.
2. In the repository, open **Settings → Pages → Build and deployment**, set **Source** to **Deploy from a branch**, choose branch `main` and folder `/ (root)`, and click **Save**.
3. After the first build, which takes a minute or two, the map is at `https://pplt-agiks.github.io/RiverwoodPreserve/`.
4. To put it in an ArcGIS StoryMap, add an **Embed** block and paste that URL.

**Visibility.** On GitHub Free and GitHub Free for organizations, Pages only publishes from a public repository, and the site is open to anyone with the URL. Only GitHub Enterprise Cloud can publish a Pages site privately. The page carries `<meta name="robots" content="noindex">` to keep it out of search engines; delete that line in `index.html` if you want it indexed.

## Contents

| Path | What it is |
|---|---|
| `index.html` | The map page |
| `data.json` | Map geometry and photo records for the page, in metres offset from a UTM origin (`origin` = NAD83 / UTM zone 19N easting and northing of the grid's lower-left corner) |
| `img/` | Base and overlay rasters on one 1,360 × 1,230 m grid: `leafoff_2026.jpg` (0.5 m), `leafon_2022.jpg`, `hillshade.jpg`, `canopy_height.png`, `evergreen_heath.png`, `water.png` (1 m), `forest_type.png`, `basal_density.png`, `invasive_watch.png` (5 m). Each has a world file (`.jgw` or `.pgw`), a `.prj` and an `.aux.xml` in NAD83 / UTM zone 19N (EPSG:26919), so it opens georeferenced in QGIS or ArcGIS |
| `data/boundaries.geojson` | Riverwood Preserve (RIGIS Local Conservation Lands 2026) and tax lot WY 39-37 |
| `data/photo_points.geojson` | 108 photo positions with caption, time, position source, uncertainty and draft tags |
| `data/next_photo_spots.geojson` | The 10 places where new photos would help the laurel/rhododendron model most |
| `data/channel_heads.geojson` | Lidar channel heads (possible seeps or springs, not field-checked) |
| `thumbs/` | Photo thumbnails used in the map popups |

GeoJSON is WGS84 (EPSG:4326).

## Status

- The photo tags were drafted by Claude from the photos and have not yet been confirmed by the steward. The laurel/rhododendron layer was fitted on these drafts.
- No track log was run on the visit. Photos with stale or poor phone fixes were placed by time between good fixes, and each record gives its uncertainty.

## Withheld from this public build

- 17 photos of stone features, rock-face close-ups and ledge settings. They are tagged restricted and held under PPLT and Tribal governance.
- 2 photos with people in them.

## Layers

| Layer | Basis |
|---|---|
| Laurel and rhododendron cover (Tier 1) | Photo tags fitted through each photo's footprint, using lidar structure, terrain, wetness and imagery. It is hatched outside the area the photos support (49% of the two lots). Photo-level spatial cross-validation gave a Spearman of 0.47, with 86% of photos within one cover class; the tool treats this score as a floor. |
| Cover and forest type (Tier 0) | Lidar height and cover crossed with NWI water regime, soil drainage and lidar depth to water |
| Canopy height, basal density index | 2022 lidar. The basal density index is uncalibrated: prism counts at photo stations would turn it into basal area |
| Water and wet ground | Lidar flow routing, channel heads and depth to water |
| Invasive watch zones | The tool's public-data invasive prior (distance to roads, buildings and the railroad, by forest type), run with a "trace" field rating. It is not fitted to the photos, because nearly every photo read trace |
| Forest history since 1939 | PPLT's Westerly Land Trust historic-landscape map (RyanPocasset/WesterlyLandTrust) |

Photo-calibrated layers are mapped at 5 m and should be read as patterns at 10–20 m. Boundaries are RIGIS lines, not survey.

## Sources

- Lidar: USGS 3DEP Rhode Island statewide 2022 (QL1, flown 26–30 March 2022, leaf-off): https://s3-us-west-2.amazonaws.com/usgs-lidar-public/RI_Statewide_1_D22/ept.json
- Imagery: RIGIS orthophotography, March 2026 leaf-off 3-inch, July 2022 leaf-on, April 2020 color-infrared, April and November 2025 seasonal flights
- Boundaries: RIGIS Local Conservation Lands 2026 (Riverwood: fee The Westerly Land Trust, conservation easement The Nature Conservancy) and RIGIS tax parcels
- Context: NWI wetlands 2014, RIGIS soils 2022, E-911 roads, 2022 building footprints and stone walls (RIGIS)
- Westerly Land Trust, Riverwood Preserve: https://westerlylandtrust.org/portfolio/riverwood-preserve/
- Westerly Land Trust, Camp Quequatuck: https://westerlylandtrust.org/?p=11911

Map: PPLT AGIKS, 2026. Built with Leaflet (BSD-2-Clause).
