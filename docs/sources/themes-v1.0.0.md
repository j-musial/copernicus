<!--
Harvested from https://github.com/stac-extensions/themes (v1.0.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Themes (v1.0.0)

- **Source repository:** [stac-extensions/themes](https://github.com/stac-extensions/themes)
- **Upstream version:** v1.0.0
- **Upstream schema:** <https://stac-extensions.github.io/themes/v1.0.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Themes* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Themes
- **Identifier:** <https://stac-extensions.github.io/copernicus:themes/v1.0.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @emmanuelmathot @m-mohr

This document explains the Themes Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This extension is meant to support knowledge organization systems used to classify the resource
(i.e. controlled vocabularies / keywords such as [Geonames](https://www.geonames.org) or [Wikipedia](https://en.wikipedia.org)).
If you just need "uncontrolled" free-form keywords / tags, please use the
[`keywords` field](https://github.com/radiantearth/stac-spec/blob/main/item-spec/common-metadata.md#basics) instead.
This extension is based on the field `copernicus:themes` as defined in [OGC API - Records](https://github.com/opengeospatial/ogcapi-records).

- Examples:
  - [Item example](https://github.com/stac-extensions/copernicus:themes/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/copernicus:themes/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/copernicus:themes/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/copernicus:themes/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:
- [x] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name | Type                             | Description |
| ---------- | -------------------------------- | ----------- |
| copernicus:themes     | \[[Theme Object](#theme-object)] | **REQUIRED.** A knowledge organization system used to classify the STAC entity. Each element is a concept and their respective knowledge organization system / controlled vocabulary. |
  
#### Theme Object

The Theme Object aims at defining a normalized list of concepts based on a knowledge organization system / controlled vocabulary (e.g. geonames).

| Field Name | Type                                  | Description |
| ---------- | ------------------------------------- | ----------- |
| concepts   | \[[Concept Object](#concept-object)] | **REQUIRED**. One or more entity/concept identifers from this knowledge system. |
| scheme     | string                                | **REQUIRED**. An identifier for the knowledge organization system used. It is recommended that the identifier is a resolvable URI. |

#### Concept Object

Describes an individual concept from the knowledge system.

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| id          | string | **REQUIRED**. An identifier for the concept. |
| title       | string | A human readable title for the concept. |
| description | string | A human readable description for the concept. |
| url         | string | *RECOMMENDED.* A URI providing further description of the concept. |
