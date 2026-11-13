<!--
Harvested from https://github.com/stac-extensions/table (v1.3.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Table (v1.3.0)

- **Source repository:** [stac-extensions/table](https://github.com/stac-extensions/table)
- **Upstream version:** v1.3.0
- **Upstream schema:** <https://stac-extensions.github.io/table/v1.3.0/schema.json>
- **License:** Apache-2.0

The following is the specification text of the *Table* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Table
- **Identifier:** <https://stac-extensions.github.io/table/v1.3.0/schema.json>
- **Field Name Prefix:** table
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @m-mohr, @TomAugspurger

This document explains the table Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
It can be used with the [projection] extension to describe geospatial tabular data.

An Collection or Item can describe a *tabular data assets*, using a list of [Column objects](#column-object).
Additionally, Collections can describe many tabular datasets using [Table objects](#table-object).

- Examples:
  - [Item example](https://github.com/stac-extensions/table/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/table/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/table/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/table/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)

| Field Name             | Type                               | Description |
| ---------------------- | ---------------------------------- | ----------- |
| copernicus:columns          | \[[Column Object](#column-object)] | A list of Column Objects describing each column. |
| copernicus:primary_geometry | string                             | The primary geometry column name. |
| copernicus:primary_datetime | string                             | The primary date/time column name. |
| copernicus:row_count        | number                             | The number of rows in the dataset. |

#### copernicus:primary_geometry

This is the column name of the "primary" or "active" geometry. This is used by libraries like [geopandas] and [sf]
to control which geometry column is used. When a STAC item uses both the [projection] and `table` extensions, it's understood that the
values in `copernicus:code`, `copernicus:bbox`, etc. that (implicitly) apply to the asset refer to the `primary_geometry` column.

---

The fields in the table below can be used in these parts of STAC documents:

- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)

| Field Name             | Type                                | Description |
| ---------------------- | ----------------------------------- | ----------- |
| copernicus:storage_options  | Map<string, any>                    | **DEPRECATED** Additional keywords for opening the dataset. |

#### copernicus:storage_options

This can be used with [fsspec](https://filesystem-spec.readthedocs.io/en/latest/) to specify additional keywords
necessary to open the data. For example, an asset might use ``{"account_name": "ai4edataeuwest"}`` to indicate that the asset is
in the ``ai4edataeuwest`` storage account. Libraries like [adlfs](https://github.com/dask/adlfs) use this information to open the dataset.

A potential alternative for storage options could be the [Storage Extension](https://github.com/stac-extensions/storage).

---

The fields in the table below can be used in these parts of STAC documents:

- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)

They can be used to catalog a collection of tables, where each table is stored as an `Item`, without
having to include column-level metadata from each table on the Collection.

|  Field Name  |                    Type                    |               Description                  |
| ------------ | ------------------------------------------ | ------------------------------------------ |
| copernicus:tables | \[[Table Object](#table-object)] | **DEPRECATED** A list of Table Objects (see below). |

---

### Column Object

Column objects contain information about each column in the table.

| Field Name    |  Type  | Description |
| ------------- | ------ | ----------- |
| name          | string | **REQUIRED**. The column name. |
| description   | string | Detailed multi-line description to explain the dimension. CommonMark 0.29 syntax MAY be used for rich text representation. |
| type          | string | Native data type of the column. If using a file format with a type system (like Parquet), we recommend you use those types. |

Other properties such as `description`, `license`, `unit`, `data_type` and `statistics` from
[STAC common metadata](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md)
can be used in the Column Object.

It is also recommended to add `copernicus:geometry_types` from the [Vector Extension](https://github.com/stac-extensions/vector)
to the columns that describe geometry data, e.g. the column identified by the `copernicus:primary_geometry` field.

`type` and `data_type` describe the same information, but `type` should use the native name in the given file format and `data_type` describes the [standardized data type name according to the STAC specification](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types).

Columns can also include additional information from other extensions that are not otherwise covered on the asset-level
and are column specific, e.g. [projection] extension information for additional geometry columns.

### Table Object

**DEPRECATED:** Table objects contain high-level summaries about a table.

| Field Name  |  Type  |                                                        Description                                                         |
| ----------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| name        | string | **REQUIRED**. The table name                                                                                               |
| description | string | Detailed multi-line description to explain the dimension. CommonMark 0.29 syntax MAY be used for rich text representation. |

### Best Practices

STAC allows for some flexibility in how to catalog assets. In general, we recommend using the following hierarchy:

- Use `Collection` objects to catalog a dataset consisting of one or more tables.
- Use `Item` objects to catalog an individual table.

For a dataset consisting of a single table or many tables with the same schema (for example
[gbif](https://github.com/microsoft/AIforEarthDataSets/blob/main/data/gbif.md), which provides snapshots of the same database at
different points in time), you might include `copernicus:columns` on the `Collection` itself, or both the `Collection` and `items`.

For datasets with many tables (for example, [USF Forest Inventory and Analysis](https://github.com/microsoft/AIforEarthDataSets/blob/main/data/forest-inventory-and-analysis.md)),
we recommend cataloging the columns at just the `Item` level in `copernicus:columns`
on each Item.
