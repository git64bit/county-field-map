# County Field Map

Reduces the county map to roads, water and buildings.

County Field Map is a single-purpose county classification ledger. It divides Kane County into 16 main sectors, each sector into a 16 × 16 inspection grid, and each inspection cell into an 8 × 8 practical grid.

## Classification

- Gray: undiscovered
- Green: discovered; the cell contains useful roads, water, or buildings
- Black: muted void; the cell contains no useful information

Clicking a practical cell marks it discovered. Shift-clicking marks it muted immediately. Select a cell and use **Mute selected sector** to mark it black. **Return to undiscovered** corrects a classification.

At the final 8 × 8 level, **Mute all 64 cells** marks the entire current inspection grid as muted after confirmation.

An inspection cell turns green when all 64 practical cells are classified. A main sector turns green when all 256 inspection cells are complete.

## Prepared field data

Place these read-only GeoJSON files together in one folder:

- `county_boundary.json`
- `roads.json`
- `water.json`
- `buildings.json`

The default folder is `processing/output/prepared`, matching the existing Kane County prepared bundle. The loader also checks `data/kane-county`, `data`, and `prepared`. A different folder can be supplied in the URL:

```text
?bundle=/path/to/prepared-data
```

## Classification storage

The browser keeps a compact local safety journal. When the included TrivialHTTP server is used, the 16 sector ledgers are also written under:

```text
project-data/sectors/
```

The application can read existing Kane-Map sector-state files and translates active practical cells to discovered and muted practical cells to black voids. New files use the `county-field-map-sector-state` format.

## TrivialHTTP

Build from the `trivialhttp` folder.

Linux:

```sh
./scripts/build-linux.sh
```

Windows cross-build on Debian or Ubuntu:

```sh
./scripts/build-windows-mingw.sh
```

macOS:

```sh
./scripts/build-macos.sh
```

Run the executable from the application root, or use `--root` to point to it.
