<!--
Harvested from https://github.com/stac-extensions/vpp (v0.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Vegetation Phenology and Productivity (v0.1.0)

- **Source repository:** [stac-extensions/vpp](https://github.com/stac-extensions/vpp)
- **Upstream version:** v0.1.0
- **Upstream schema:** <https://stac-extensions.github.io/vpp/v0.1.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Vegetation Phenology and Productivity* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Vegetation Phenology and Productivity
- **Identifier:** <https://stac-extensions.github.io/vpp/v0.1.0/schema.json>
- **Field Name Prefix:** vpp
- **Scope:** Collection, Item
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Vegetation Phenology and Productivity Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

Vegetation Phenology and Productivity (VPP) parameters describe the seasonal development of vegetation,
such as the start and end of the growing season, and the productivity of the vegetation during a season.
The term is primarily used in the [Copernicus Land Monitoring Service (CLMS)](https://land.copernicus.eu/).
This extension defines the fields used to describe the VPP season and sub-parameter that a STAC object relates to.

- Examples:
  - [Item example](https://github.com/stac-extensions/vpp/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/vpp/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/vpp/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/vpp/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections and Asset Templates)
- [ ] Links (incl. Link Templates)
- [ ] Bands

| Field Name        | Type   | Description                                                              |
| ----------------- | ------ | ------------------------------------------------------------------------ |
| copernicus:season        | string | The VPP season number. One of `S1` or `S2`. See below for details.       |
| copernicus:sub_parameter | string | The VPP sub-parameter acronym. See below for the list of allowed values. |

#### Additional Field Information

##### copernicus:season

The Vegetation Phenology and Productivity (VPP) season number. Two seasons can be detected per year.

| Value | Description    |
| ----- | -------------- |
| `S1`  | First season.  |
| `S2`  | Second season. |

##### copernicus:sub_parameter

The Vegetation Phenology and Productivity (VPP) sub-parameter acronym.

| Value    | Description                                   |
| -------- | --------------------------------------------- |
| `AMPL`   | Season amplitude                              |
| `EOSD`   | Day of end-of-season                          |
| `EOSV`   | Vegetation index value at end-of-season       |
| `LENGTH` | Length of season                              |
| `LSLOPE` | Slope of the greening up period               |
| `MAXD`   | Day of maximum value in season                |
| `MAXV`   | Maximum value of the season                   |
| `MINV`   | Minimum value of the season                   |
| `QA`     | Quality assurance / quality flag              |
| `RSLOPE` | Slope of the senescent period                 |
| `SOSD`   | Day of start-of-season                        |
| `SOSV`   | Vegetation index value at start-of-season     |
| `SPROD`  | Seasonal productivity                         |
| `TPROD`  | Total productivity                            |
