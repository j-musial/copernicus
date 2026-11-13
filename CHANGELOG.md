# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-11-13

### Added

- Initial release of the Copernicus STAC Extension.
- Merges 31 STAC extensions into a single `copernicus:` namespace:
  - [alternate-assets](https://github.com/stac-extensions/alternate-assets)
  - [altimetry](https://github.com/stac-extensions/altimetry)
  - [authentication](https://github.com/stac-extensions/authentication)
  - [cf](https://github.com/stac-extensions/cf)
  - [classification](https://github.com/stac-extensions/classification)
  - [contacts](https://github.com/stac-extensions/contacts)
  - [datacube](https://github.com/stac-extensions/datacube)
  - [eo](https://github.com/stac-extensions/eo)
  - [embeddings](https://github.com/stac-extensions/embeddings)
  - [grid](https://github.com/stac-extensions/grid)
  - [order](https://github.com/stac-extensions/order)
  - [processing](https://github.com/stac-extensions/processing)
  - [product](https://github.com/stac-extensions/product)
  - [projection](https://github.com/stac-extensions/projection)
  - [raster](https://github.com/stac-extensions/raster)
  - [region](https://github.com/stac-extensions/region)
  - [render](https://github.com/stac-extensions/render)
  - [sar](https://github.com/stac-extensions/sar)
  - [sat](https://github.com/stac-extensions/sat)
  - [scientific](https://github.com/stac-extensions/scientific)
  - [stats](https://github.com/stac-extensions/stats)
  - [storage](https://github.com/stac-extensions/storage)
  - [table](https://github.com/stac-extensions/table)
  - [themes](https://github.com/stac-extensions/themes)
  - [timestamps](https://github.com/stac-extensions/timestamps)
  - [vector](https://github.com/stac-extensions/vector)
  - [vpp](https://github.com/stac-extensions/vpp)
  - [view](https://github.com/stac-extensions/view)
  - [web-map-links](https://github.com/stac-extensions/web-map-links)
  - [xarray-assets](https://github.com/stac-extensions/xarray-assets)
  - [eopf-stac-extension](https://github.com/CS-SI/eopf-stac-extension)
- 134 fields under the `copernicus:` prefix, defined across Item Properties,
  Assets, Links, Bands, Collections, and Catalogs.
- Single merged JSON Schema (draft-07) including storage platform sub-schemas
  (aws-s3, custom-s3, ms-azure).
- Example [Item](examples/item.json) and [Collection](examples/collection.json).
- Harvested specification text of all 31 source extensions in
  [docs/sources/](docs/sources/README.md), named `<extension>-<version>.md`, with
  field names rewritten to `copernicus:` equivalents and relative links pointing
  to the upstream repositories.
- Conflict resolution for name collisions:
  - `grid:code` → `copernicus:grid_code` and `proj:code` → `copernicus:code`
  - `order:status` → `copernicus:order_status` and `product:status` → `copernicus:product_status`
  - `storage:schemes`/`auth:schemes` → `copernicus:storage_schemes`/`copernicus:auth_schemes`
  - `storage:refs`/`auth:refs` → `copernicus:storage_refs`/`copernicus:auth_refs`
  - `emb:dimensions` → `copernicus:embedding_dimensions` (vs `cube:dimensions` → `copernicus:dimensions`)
  - `emb:type` → `copernicus:embedding_type` (vs `product:type` → `copernicus:type`)
  - web-map-links link fields flattened (e.g. `wms:layers` → `copernicus:wms_layers`)
- Fields defined by multiple sources merged into single definitions:
  `copernicus:instrument_mode` (altimetry + sar + eopf),
  `copernicus:datastrip_id` (processing + eopf),
  `copernicus:product_type` (product + sar),
  `copernicus:storage_options` (table + xarray-assets).
