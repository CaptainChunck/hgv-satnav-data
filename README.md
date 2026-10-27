# HGV Satnav map data

Offline map packs for the HGV Satnav Android app. The app downloads these by itself the first
time it runs and checks for newer ones once a day on Wi-Fi. You do not need to download anything
here by hand.

Everything here is built from free, open data. There is no app code in this repository.

## What a release contains

| File | What it is | Size |
| --- | --- | --- |
| `valhalla_tiles.tar.part1`, `.part2` | Truck routing graph (Valhalla 3.9.1 tile extract) | 2.9 GB |
| `basemap.pmtiles.part1`, `.part2` | Offline map picture (PMTiles, OpenMapTiles schema) | 1.6 GB |
| `overlay.sqlite` | Height, width and weight limits, tunnel categories and other hazards, for warnings | 48 MB |
| `search.sqlite` | Offline postcode and place search | 175 MB |
| `manifest.json` | Every file's size and SHA-256 checksum; the app reads this | 2 KB |

GitHub limits a release file to 2 GiB, so the two big packs are split. The app joins the parts
and checks the checksum of the whole file before using it. To join them by hand:

```bash
cat valhalla_tiles.tar.part1 valhalla_tiles.tar.part2 > valhalla_tiles.tar
cat basemap.pmtiles.part1 basemap.pmtiles.part2 > basemap.pmtiles
```

On Windows: `copy /b valhalla_tiles.tar.part1 + valhalla_tiles.tar.part2 valhalla_tiles.tar`.

## Sources and licences

- **OpenStreetMap.** Map data © OpenStreetMap contributors, available under the
  [Open Database License (ODbL) 1.0](https://www.openstreetmap.org/copyright). The routing,
  map and restriction packs are derived from the Geofabrik United Kingdom extract, and are
  themselves made available under the ODbL.
- **Map pack.** Uses the [OpenMapTiles](https://openmaptiles.org/) schema (© OpenMapTiles,
  CC-BY 4.0), built with [Planetiler](https://github.com/onthegomap/planetiler), and includes
  [Natural Earth](https://www.naturalearthdata.com/) data (public domain).
- **Search pack.** OS Code-Point Open and OS Open Names. Contains OS data © Crown copyright and
  database right 2026. Contains Royal Mail data © Royal Mail copyright and database right 2026.
  Contains National Statistics data © Crown copyright and database right 2026. Under the
  [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
  Coordinates converted with OSTN15, © Copyright and database rights Ordnance Survey Limited
  2016 (BSD licence). Northern Ireland postcodes are not included.
- **ADR tunnel categories.** Department for Transport, "Transporting dangerous goods: ADR tunnel
  categories" (Open Government Licence v3.0), checked against the tunnel operators' published
  restrictions. Each overlay row records its own source.

Each SQLite pack also carries its sources in its `meta` table.

## Accuracy

Map data can be incomplete, wrong or out of date. Always follow road signs and your company's
route instructions.
