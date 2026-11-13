<!--
Harvested from https://github.com/stac-extensions/alternate-assets (v1.2.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Alternate Assets (v1.2.0)

- **Source repository:** [stac-extensions/alternate-assets](https://github.com/stac-extensions/alternate-assets)
- **Upstream version:** v1.2.0
- **Upstream schema:** <https://stac-extensions.github.io/alternate-assets/v1.2.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Alternate Assets* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Alternate Assets
- **Identifier:** <https://stac-extensions.github.io/alternate-assets/v1.2.0/schema.json>
- **Field Name Prefix:** `alternate`
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @matthewhanson

The Alternate Assets extension to STAC provides a way to specify alternate locations (e.g., URLs) for assets.
Sometimes, assets can be retrieved via multiple methods.
For example an asset on AWS may have a public facing http URL but also a direct access s3 URL.
Or an asset is mirrored on multiple servers that have different URLs.
The file the asset points to must always be exactly the same (i.e. both assets have the same checksum and file size),
but different protocols, authentication mechanisms or cloud services may be used to access it.

- Examples:
  - [Item example](https://github.com/stac-extensions/alternate-assets/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/alternate-assets/blob/main/examples/collection.json): Shows usage in Collection assets and [item assets](https://github.com/stac-extensions/item-assets)
- [JSON Schema](https://github.com/stac-extensions/alternate-assets/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/alternate-assets/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [ ] Collections
- [ ] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name     | Type                                                           | Description |
| -------------- | -------------------------------------------------------------- | ----------- |
| alternate      | Map<string, [Alternate Asset Object](#alternate-asset-object)> | An array of alternate location information for an asset |
| alternate:name | string                                                         | A short name to distinguish the asset from the alternate assets. |

Each alternate asset consists of a key and an Alternate Asset Object.

Example:
```json
"alternate": {
  "s3": {
    "href": "s3://bucket/key"
  }
}
```

The Alternate Asset Objects are similar to the
[Asset Object](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md#asset-object)
as defined in the STAC Item Specification.

The key should be used consistently across all assets (and items) if from the same source.
In other words, if all the assets in an Item are all available via s3 direct access, the key for all of them should be the same.

#### Alternate Asset Object

The Alternate Asset Object are similar to the core Asset object, except only contain fields relevant to the location and access of the asset.

| Field Name     | Type   | Description |
| -------------- | ------ | ----------- |
| href           | string | **REQUIRED.** URI to the asset object. Relative and absolute URI are both allowed. |
| alternate:name | string | A short name to distinguish the alternate assets. |

In the simplest case, the object consists of a single `href` field, but could include additional details regarding the alternate location or URL.

Some fields that are commonly provided:

- `title` and `description` as specified in [STAC's Common Metadata](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#basics).
- The [Storage Extension](https://github.com/stac-extensions/storage) could be used to provide additional details on its host or location.
- The [Authentication Extension](https://github.com/stac-extensions/authentication) could provide details about specific authentication requirements.

It is also recommended that the [Item Assets Definition](https://github.com/stac-extensions/item-assets)
Extension is provided in Collections to convey to users what the options are for alternate access.

The `name` field could potentially also be provided in the core Asset Object as a short name to distinguish them from the alternate assets.
