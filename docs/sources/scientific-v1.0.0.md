<!--
Harvested from https://github.com/stac-extensions/scientific (v1.0.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Scientific Citation (v1.0.0)

- **Source repository:** [stac-extensions/scientific](https://github.com/stac-extensions/scientific)
- **Upstream version:** v1.0.0
- **Upstream schema:** <https://stac-extensions.github.io/scientific/v1.0.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Scientific Citation* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Scientific Citation
- **Identifier:** <https://stac-extensions.github.io/scientific/v1.0.0/schema.json>
- **Field Name Prefix:** sci
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/README.md#extension-maturity):** Stable
- **Owner**: @m-mohr
- **History:** [Prior to March 30, 2021](https://github.com/radiantearth/stac-spec/commits/v1.0.0-rc.2/extensions/scientific)

This document explains the Scientific Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

This extension adds the ability to indicate from which publication data originates and how
the data itself should be cited or referenced. Overall, it helps to increase reproducibility and citability.

Human-readable references and [DOIs](https://www.doi.org/) can be used in this extension. DOIs are
persistent digital interoperable identifier that uniquely identify for digital publications. They
can be registered at registration agencies affiliated with the
[International DOI Foundation](https://www.doi.org/).

This extension applies to STAC [Item](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md)
and STAC [Collections](https://github.com/radiantearth/stac-spec/tree/master/collection-spec/collection-spec.md).
As these citation information are often closely bound to the Collection level and therefore are shared across all items,
it is recommended adding the fields to the corresponding Collection.

- Examples:
  - [Item](https://github.com/stac-extensions/scientific/blob/main/examples/item.json): The extension in a STAC Item
  - [Collection](https://github.com/stac-extensions/scientific/blob/main/examples/collection.json): The extension in a STAC Collection
  - [Collection (Assets)](https://github.com/stac-extensions/scientific/blob/main/examples/collection-assets.json): The extension in a STAC Collection with assets
  - [Collection (Item Asset Definition)](https://github.com/stac-extensions/scientific/blob/main/examples/collection-item-assets.json): The extension in a STAC Collection in Item Asset Defintions
  - [Collection (Summaries)](https://github.com/stac-extensions/scientific/blob/main/examples/collection-summaries.json): The extension in a STAC Collection in Summaries
- [JSON Schema](https://github.com/stac-extensions/scientific/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/scientific/blob/main/CHANGELOG.md)

### Item Properties and Collection Fields

For Items, the fields are placed in the `properties`. For Collections, the fields are placed on the top level of the Collection.

| Field Name       | Type                 | Description |
| ---------------- | -------------------- | ----------- |
| copernicus:doi          | string               | The DOI of the data, e.g. `10.1000/xyz123`. This MUST NOT be a DOIs link. For all DOI names respective DOI links SHOULD be added to the links section (see chapter "Relation types"). |
| copernicus:citation     | string               | The recommended human-readable reference (citation) to be used by publications citing the data. No specific citation style is suggested, but the citation should contain all information required to find the publication distinctively. |
| copernicus:publications | [[Publication Object](#publication-object)] | List of relevant publications referencing and describing the data. |

*At least one of the fields must be specified.*

#### Publication Object

| Field Name | Type   | Description |
| ---------- | ------ | ----------- |
| doi        | string | The DOI of a publication referencing the data. This MUST NOT be a DOIs link. |
| citation   | string | Citation of a publication referencing the data. |

**doi** - The DOI name of a publication which describes and references the data. The publications
should include more information about the data and how it was processed. This MUST NOT be a DOI
link. For all DOI names respective DOI links SHOULD be added to the links section
(see chapter "Relation types").

**citation** - Human-readable reference (citation) of a publication which describes and references
the data. The publications should include more information about the data and how it was
processed. No specific citation style is suggested, but a citation should contain all information
required to find the publication distinctively.

### Relation types

The following types should be used as applicable `rel` types in the
[Link Object](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#link-object).

| Type    | Description |
| ------- | ----------- |
| cite-as | A DOI link SHOULD be added to the links section for the publication referenced by the `copernicus:doi` property with the `rel` type `cite-as` (see the [RFC 8574](https://tools.ietf.org/html/rfc8574)). |
