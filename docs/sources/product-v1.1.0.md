<!--
Harvested from https://github.com/stac-extensions/product (v1.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Product (v1.1.0)

- **Source repository:** [stac-extensions/product](https://github.com/stac-extensions/product)
- **Upstream version:** v1.1.0
- **Upstream schema:** <https://stac-extensions.github.io/product/v1.1.0/schema.json>
- **License:** Apache-2.0

The following is the specification text of the *Product* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Product
- **Identifier:** <https://stac-extensions.github.io/product/v1.1.0/schema.json>
- **Field Name Prefix:** product
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Product Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

This extension provides a generic framework to describe products related to the data in a STAC catalog.
A product is a package offer of the STAC item and thus describes properties specific to what the product is and how it is packaged.
It doesn't describe how or where the product is distributed.
For example, whether the data can be downloaded directly is described in the [Access Extension](https://github.com/stac-extensions/access).
Several products may be specified at assets level, each with its own properties.
This extension is intended to be adapted by other extensions that provide best practises or definitions about the product like
specific dictionaries for the product type or the timeliness of the product.

- Examples:
  - [Item example](https://github.com/stac-extensions/product/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/product/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/product/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/product/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name                  | Type   | Description                                                  |
| --------------------------- | ------ | ------------------------------------------------------------ |
| copernicus:product_type                | string | The product type.                                            |
| copernicus:timeliness          | string | The average expected timeliness of the product as an [ISO 8601 Duration](https://en.wikipedia.org/wiki/ISO_8601#Durations). |
| copernicus:timeliness_category | string | A proprietary category identifier for the timeliness of the product. |
| copernicus:acquisition_type    | string | The acquisition type of the product.                         |
| copernicus:product_status              | string | The lifecycle/status of the product.                         |
| copernicus:quality_status      | string | The quality status of the product: `nominal` or `degraded`.  |

> \[!IMPORTANT]  
> `copernicus:timeliness` is REQUIRED if `copernicus:timeliness_category` is provided.

#### Additional Field Information

##### Timeliness

Below you can find an example that shows how the timeliness fields could be used.

The Copernicus programme releases products on three levels of timeliness:

| Name                | Description                                                  | `copernicus:timeliness`    | `copernicus:timeliness_category` |
| ------------------- | ------------------------------------------------------------ | ----------------------- | ----------------------------- |
| Near Real-Time      | Delivered less than 3 hours after data acquisition.          | e.g. `PT3H` (3 hours)   | `NRT`                         |
| Short Time-Critical | Delivered within 36 (Sentinel-6) to 48 (Sentinel-3) hours after data acquisition. | e.g. `PT36H` (36 hours) | `STC`                         |
| Non Time-Critical   | Delivered typically within 1 month after data acquisition.   | e.g `P1M` (1 month)     | `NTC`                         |

> \[!WARNING]
>
> Be careful when specifying the durations for `copernicus:timeliness`.
> It is recommended to closely reflect the semantics of timeliness as specified by the provider.
> For example, if the timeliness is 36 hours, specify  `PT36H` instead of  `P1DT12H`, although allowed:
>
> > The standard does not prohibit date and time values in a duration  representation from exceeding their "carry over points".
> > Thus, `PT36H` could be used as well as `P1DT12H` for representing the same duration.
> > But keep in mind that `PT36H` is not the same as  `P1DT12H` when switching from or to Daylight saving time.
>
> Source: <https://en.wikipedia.org/wiki/ISO_8601#Durations>

##### copernicus:product_type

The product type in this extension is a free-form text that providers can freely use to descibe their product types.
Some extensions may specify more specific rules for this field.

This field superceedes the `copernicus:product_type` field.

##### copernicus:acquisition_type

The product acquisition type describes the purpose of the acquisition.
It is similar to the `acquisitionType` field from the
[OGC® Earth Observation Metadata profile of Observations & Measurements , Table 5](https://docs.ogc.org/is/10-157r4/10-157r4.html#24):

> Used to distinguish at a high level the appropriateness of the acquisition for "general" use,
> whether the product is a nominal acquisition, special calibration product or other.

Allowed values are:

- `nominal`
- `calibration`
- `other`

Sentinel-2 [Annex A (page 90)](https://sentinels.copernicus.eu/documents/247904/2047089/Sentinel-2_Cal-Val_Phase-E2)
provides the calibration sites so some acquisitions over those areas will be acquired for calibration purposes.
The `copernicus:acquisition_type` field brings the possibility to "flag" products as `nominal`, `calibration`
or `other` (not `nominal`, not `calibration`).

[Sentinel-1](https://sentinels.copernicus.eu/web/sentinel/-/copernicus-sentinel-1-calibration-campaign-on-going-in-europe) provides few acquisitions
in given dates and orbits that were acquired in a different mode. Those products would have `calibration`.

##### copernicus:product_status

Refers to product status.
It is similar to the `status` field (of kind `StatusValue`) from the
[OGC® Earth Observation Metadata profile of Observations & Measurements , Table 5](https://docs.ogc.org/is/10-157r4/10-157r4.html#24):

Allowed values are:

- `archived`
- `acquired`
- `cancelled`
- `failed`
- `planned`
- `potential`
- `rejected`
- `qualitydegraded` (**deprecated**, see below)
- `accepted`

The value `accepted` is an addition to the OGC list.
It means that the product passed its quality control or validation checks and is fit for downstream use.
It is the positive counterpart of `rejected`.

In the OGC model, `archived` is the nominal value, but it only tells that the product is in the archive.
OGC refines `archived` with a separate `statusSubType` field (`ON-LINE` or `OFF-LINE`).
This extension does not define a status subtype.
Instead, `accepted` states directly that the product is usable, with a single field.
Whether the data is online or offline is described by
[`access:availability`](https://github.com/stac-extensions/access#accessavailability) in the Access Extension.

> \[!WARNING]
> The value `qualitydegraded` is **deprecated** and may be removed in a future major version.
> This follows OGC 10-157r4, which deprecates it in favour of the `productQualityStatus` element.
> Use [`copernicus:quality_status`](#productquality_status) with the value `degraded` to describe the product quality,
> and keep `copernicus:product_status` for the lifecycle or disposition of the product.
> For example, replace `"copernicus:product_status": "qualitydegraded"` with
> `"copernicus:product_status": "accepted"` and `"copernicus:quality_status": "degraded"`.

###### Relationship with the Order Extension

`copernicus:product_status` and `copernicus:order_status` may appear similar but they describe different entities and lifecycle concerns.

- `copernicus:order_status` describes the lifecycle or execution state of a request, order, or processing transaction.
- `copernicus:product_status` describes the disposition or usability status of the resulting catalogued product artifact itself.

A processing order may therefore complete successfully while the generated product is later considered unsuitable for downstream use.

For example, in a processing chain, a derived product may be successfully generated and catalogued,
 but later excluded from downstream processing after quality control validation:

```json
{
  "properties": {
    "copernicus:product_status": "rejected"
  }
}
```

###### Relationship with the Access Extension

`copernicus:product_status` is a property of the product itself.
[`access:availability`](https://github.com/stac-extensions/access#accessavailability)
is a property of a copy of the data at a distributor.
Both are independent of each other.
For example, `archived` doesn't imply that the data must be retrieved before it can be downloaded.

##### copernicus:quality_status

Indicates whether the quality of the product is degraded or not.
It is similar to the `productQualityStatus` field from the
[OGC® Earth Observation Metadata profile of Observations & Measurements , Table 5](https://docs.ogc.org/is/10-157r4/10-157r4.html#24):

> Indicator that specifies whether the product quality is degraded or not.
> This optional field shall be provided if the product has passed a quality check.

Allowed values are:

- `nominal`: the product passed the quality check without degradation.
- `degraded`: the product passed the quality check, but its quality is degraded.

Do not set this field if no quality check was done on the product.

`copernicus:quality_status` and `copernicus:product_status` are independent.
`copernicus:product_status` tells whether the product can be used, and `copernicus:quality_status` tells the quality of a usable product.
For example, a product can be `accepted` with a `degraded` quality.

###### Mapping from GEODES `product_validity`

The [GEODES STAC API](https://geodes.cnes.fr/metadonnees-offertes-par-lapi-stac-de-geodes/) of CNES
uses a boolean `product_validity` field.
It tells whether the product has passed quality checks or meets specific predefined criteria.
The recommended mapping is:

| `product_validity` | `copernicus:product_status` | `copernicus:quality_status` |
| ------------------ | ---------------- | ------------------------ |
| `true`             | `accepted`       | `nominal` or `degraded`  |
| `false`            | `rejected`       | not set                  |
| not set            | not set          | not set                  |

```json
{
  "properties": {
    "copernicus:product_status": "accepted",
    "copernicus:quality_status": "nominal"
  }
}
```
