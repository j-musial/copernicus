<!--
Harvested from https://github.com/stac-extensions/stats (v0.2.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Stats (v0.2.0)

- **Source repository:** [stac-extensions/stats](https://github.com/stac-extensions/stats)
- **Upstream version:** v0.2.0
- **Upstream schema:** <https://stac-extensions.github.io/stats/v0.2.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Stats* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Stats
- **Identifier:** <https://stac-extensions.github.io/stats/v0.2.0/schema.json>
- **Field Name Prefix**: stats
- **Scope:** Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @tschaub

This document explains the Stats Extension to the [SpatioTemporal Asset
Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

Catalogs and collections using this extension include additional information summarizing the resource types included.
Top-level catalogs can report counts of child catalogs, collections, or items and can include information on the
versions, extensions, and asset types (in the case of items) used by those resources.  Collections or sub-catalogs
can also report statistics on child resources instead of having this reported at the top level.
 
- Examples:
  - [Catalog with all stats](https://github.com/stac-extensions/stats/blob/main/examples/catalog-with-all-stats/catalog.json): Shows the usage of the extension in a
    top-level Catalog
  - [Collection with item stats](https://github.com/stac-extensions/stats/blob/main/examples/catalog-with-no-stats/collection.json): Shows the usage of the extension
    in a Collection (instead of at the top-level Catalog)
- [JSON Schema](https://github.com/stac-extensions/stats/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/stats/blob/main/CHANGELOG.md)

### Top-Level Catalog or Collection Fields

| Field Name           | Type                                     | Description                                  |
| -------------------- | ---------------------------------------- | -------------------------------------------- |
| copernicus:stats_catalogs       | [Catalogs Stats](#catalogs-stats)        | A lookup of stats for all child catalogs.    |
| copernicus:stats_collections    | [Collections Stats](#collections-stats)  | A lookup of stats for all child collections. |
| copernicus:stats_items          | [Items Stats](#items-stats)              | A lookup of stats for all child items.       |

#### Catalogs Stats

Information about the resources included in all child catalogs.

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| count       | number | **REQUIRED.** The count of all child catalogs. |
| versions    | object | A lookup of counts for all versions. Keys are version identifiers, and values are integer counts. |
| extensions  | object | A lookup of counts for all extensions. Keys are extension identifiers, and values are integer counts. |
| conformance | object | A lookup of counts for STAC API conformance classes. Keys are conformance URIs, and values are integer counts. |

Example `copernicus:stats_catalogs` that might be found in a top-level catalog with three child sub-catalogs.

```json
{
  "copernicus:stats_catalogs": {
    "count": 3,
    "versions": {
      "1.0.0": 1,
      "1.0.0-beta.2": 2
    }
  }
}
```

#### Collections Stats

Information about the resources included in all child collections.

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| count       | number | **REQUIRED.** The count of all child collections. |
| versions    | object | A lookup of counts for all versions. Keys are version identifiers, and values are integer counts. |
| extensions  | object | A lookup of counts for all extensions. Keys are extension identifiers, and values are integer counts. |

Example `copernicus:stats_collections` that might be found in a top-level catalog with four child collections (two of which use an extension).

```json
{
  "copernicus:stats_collections": {
    "count": 4,
    "versions": {
      "1.0.0": 4
    },
    "extensions": {
      "https://stac-extensions.github.io/eo/v1.0.0/schema.json": 2
    }
  }
}
```

#### Items Stats

Information about the resources included in all child items.

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| count       | number | **REQUIRED.** The count of all child items. |
| versions    | object | A lookup of counts for all versions. Keys are version identifiers, and values are integer counts. |
| extensions  | object | A lookup of counts for all extensions. Keys are extension identifiers, and values are integer counts. |
| assets      | object | A lookup of counts for all assets. Keys are asset types, and values are integer counts. |

Example `copernicus:stats_items` that might be found in a collection with 100 items.

```json
{
  "copernicus:stats_items": {
    "count": 100,
    "versions": {
      "1.0.0-beta.2": 20,
      "1.0.0": 80
    },
    "extensions": {
      "https://stac-extensions.github.io/eo/v1.0.0/schema.json": 80,
      "https://stac-extensions.github.io/raster/v1.0.0/schema.json": 50
    },
    "assets": {
      "image/jpeg": 20,
      "image/png": 30,
      "image/tiff; application=geotiff; profile=cloud-optimized": 50
    }
  }
}
```
