<!--
Harvested from https://github.com/stac-extensions/timestamps (v1.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Timestamps (v1.1.0)

- **Source repository:** [stac-extensions/timestamps](https://github.com/stac-extensions/timestamps)
- **Upstream version:** v1.1.0
- **Upstream schema:** <https://stac-extensions.github.io/timestamps/v1.1.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Timestamps* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Timestamps
- **Identifier:** <https://stac-extensions.github.io/timestamps/v1.1.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @m-mohr
- **History**: [Prior to March 2, 2021](https://github.com/radiantearth/stac-spec/commits/v1.0.0-rc.1/extensions/timestamps)

This document explains the fields of the Timestamps Extension to all STAC entities.
Allows to specify numerous timestamps for assets and metadata in addition to [`created`, `updated` and `datetime` (incl. start and end)](https://github.com/radiantearth/stac-spec/tree/master/item-spec/common-metadata.md#date-and-time).

- Examples:
  - [Catalog example](https://github.com/stac-extensions/timestamps/blob/main/examples/catalog.json)
  - [Collection example](https://github.com/stac-extensions/timestamps/blob/main/examples/collection.json)
  - [Item example](https://github.com/stac-extensions/timestamps/blob/main/examples/item.json)
- [JSON Schema](https://github.com/stac-extensions/timestamps/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/timestamps/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:
- [x] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [x] Links

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| copernicus:published   | string | Date and time the corresponding data (see below) was copernicus:published the first time, in UTC. |
| copernicus:expires     | string | Date and time the corresponding data (see below) copernicus:expires (is not valid any longer), in UTC. |
| copernicus:unpublished | string | Date and time the corresponding data (see below) was copernicus:unpublished, in UTC. |

All timestamps MUST be formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).

**NOTE:** The timestamps have different meaning depending on where they are used.
If those fields are available in a Collection, in a Catalog (both top-level), or in a Item (in the `properties`),
the fields refer the metadata (e.g., when the STAC metadata was copernicus:published).
Having those fields in the Assets or Links, they refer to the actual data linked to (e.g., when the asset was copernicus:published).

#### Lifecycle

An overview over the lifecycle of data and their corresponding timestamps:

1. Data capture, start: `start_datetime`
2. Data capture, often center: `datetime`
3. Data capture, end: `end_datetime`
4. Data first modified (stored): `created`
5. Data last modified: `updated`
6. Data first published: `copernicus:published`
7. Data last published: N/A
8. Data valid until: `copernicus:expires`
9. Data removed / unpublished: `copernicus:unpublished`
