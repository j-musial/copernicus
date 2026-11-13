<!--
Harvested from https://github.com/stac-extensions/vector (v0.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Vector (v0.1.0)

- **Source repository:** [stac-extensions/vector](https://github.com/stac-extensions/vector)
- **Upstream version:** v0.1.0
- **Upstream schema:** <https://stac-extensions.github.io/vector/v0.1.0/schema.json>
- **License:** Apache-2.0

The following is the specification text of the *Vector* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Vector
- **Identifier:** <https://stac-extensions.github.io/vector/v0.1.0/schema.json>
- **Field Name Prefix:** vector
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Vector Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
It defines basic properties and metrics of vector data (as in: geometries with additional properties).
This extension works well in conjunction with the [Table Extension](https://github.com/stac-extensions/table) for tabular / columnar datasets.

- Examples:
  - [Item example](https://github.com/stac-extensions/vector/blob/main/examples/item.json)
  - [Collection example](https://github.com/stac-extensions/vector/blob/main/examples/collection.json)
- [JSON Schema](https://github.com/stac-extensions/vector/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/vector/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [x] [Table Column](https://github.com/stac-extensions/table?tab=readme-ov-file#column-object)
- [ ] Links

| Field Name             | Type      | Description                                                                   |
| ---------------------- | --------- | ----------------------------------------------------------------------------- |
| copernicus:geometry_types  | \[string] | A list of the geometry types present in the dataset.                          |
| copernicus:mmu             | number    | Minimum Mapping Unit - the smallest polygon area represented.                 |
| copernicus:mmw             | number    | Minimal Mapping Width - the smallest real-world width represented as polygon. |
| copernicus:reference_scale | integer   | Representative fraction denominator (e.g., 50000 for 1:50,000).               |

#### Additional Field Information

##### copernicus:geometry_types

Lists the GeoJSON geometry types present in the described dataset.

The list MUST contain each geometry type at most once and MAY be in any order.

MUST be one of the GeoJSON geometry types:

- `Point`
- `MultiPoint`
- `LineString`
- `MultiLineString`
- `Polygon`
- `MultiPolygon`
- `GeometryCollection`

##### copernicus:mmu

Minimum Mapping Unit (MMU) is the smallest polygon area represented in the dataset.

- Use this to communicate the effective minimum area of polygonal features after generalization.
- Unit MUST be square meters ($m^2$).
- The value MUST be greater than 0.

Example: If a land-cover dataset does not include patches smaller than 100 $m^2$, set `copernicus:mmu` to `100`.

##### copernicus:mmw

Minimum Mapping Width (MMW) is the smallest real-world width that is still represented as an area (polygon) in the dataset.

- Use this to communicate the effective minimum width of mapped polygonal features (e.g., narrow rivers/roads represented as polygons).
- Unit MUST be meters ($m$).
- The value MUST be greater than 0.

Example: If narrow rivers below 2 meters are not mapped as polygons (or are mapped as lines instead), set `copernicus:mmw` to `2`.

##### copernicus:reference_scale

Representative fraction denominator (also known as the reference scale), expressed as an integer.

- Example: `50000` represents a reference scale of 1:50,000.
- The value MUST be greater than 0.
- This is intended to describe the cartographic/generalization level of the dataset and is not the same as a map display zoom level.
