# Who's been flying over your place?

A single-page website that replays the last 7 days of Earth-observation satellite orbits over any place on Earth. It then finds the public Sentinel-2 and Landsat photos those satellites took of that spot.

Everything is in one file, `index.html`. There are no build tools and no API keys: open it in Chrome and search for a place.

## What it does

- **Place search** with suggestions as you type (Photon), or Nominatim when you press Enter, shown on a Leaflet map.
- **Orbit replay:** downloads TLEs for CelesTrak's `resource` group (cached for 2 hours in `localStorage`) and propagates them with satellite.js 5.0.0. Satellites with fewer than 11 orbits a day are skipped.
  - Steps are 2 minutes when a satellite is over 3,500 km from the place and 10 seconds when it's closer.
  - A pass counts when Sentinel-2 is within 145 km, Landsat 8/9 is within 93 km, or any other satellite is at least 10° above the horizon.
- **Public photos:** searches Microsoft Planetary Computer (`sentinel-2-l2a`, `landsat-c2-l2`) for the last 7 days and crops each preview to the place ± 0.03°. Each photo is matched to a pass of the same satellite from 10 minutes before to 60 minutes after the photo was taken.
- **Results:**
  - A headline with the number of satellites that passed and the number of public photos.
  - A table per satellite with a status: *Watched, photo public*, *Likely watched* or *Passed overhead*.
  - A country tag from CelesTrak's satellite catalog, with Indian satellites highlighted in orange.
  - Animated ground tracks on the map.

## Data & credits

- Orbit data and satellite owners: [CelesTrak](https://celestrak.org)
- Sentinel-2 imagery: contains modified [Copernicus](https://www.copernicus.eu) Sentinel data (ESA)
- Landsat imagery: courtesy of [USGS/NASA](https://www.usgs.gov/landsat-missions)
- Photo search and rendering: [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com)
- Place search and map data: © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors (Nominatim); suggestions by [Photon](https://photon.komoot.io) (komoot)
- Map tiles: © Esri, HERE, Garmin, OpenStreetMap contributors
- Libraries: [Leaflet](https://leafletjs.com), [satellite.js](https://github.com/shashwatak/satellite-js)

Statuses are estimates. "Likely watched" means an imaging satellite flew close by in daylight. It doesn't mean it took a picture.
