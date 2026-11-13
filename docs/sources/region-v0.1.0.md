<!--
Harvested from https://github.com/stac-extensions/region (v0.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Region (v0.1.0)

- **Source repository:** [stac-extensions/region](https://github.com/stac-extensions/region)
- **Upstream version:** v0.1.0
- **Upstream schema:** <https://stac-extensions.github.io/region/v0.1.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Region* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Region
- **Identifier:** <https://stac-extensions.github.io/region/v0.1.0/schema.json>
- **Field Name Prefix:** region
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Region Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This is the place to add a short introduction.

- Examples:
  - [Collection example](https://github.com/stac-extensions/region/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/region/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/region/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name         | Type   | Description                                  |
| ------------------ | ------ | -------------------------------------------- |
| copernicus:name        | string | A human-readable name of the relevant region. |
| copernicus:country     | string | ISO 3166-1 alpha-2 country code. Two-letter country code for the country that is primarily covered by the data. |
| copernicus:subdivision | string | ISO 3166-2 codes for identifying the principal subdivisions (e.g., provinces or states) of a country that is primarily covered by the data. Only provide the second part of the ISO 3166-2 code to reduce redundancy. |

#### Additional Field Information

##### copernicus:name

In general this is a free-text field, but to make it most useful for search and discovery, please follow the following guidelines:

- Always provide **all names in the language of the metadata**.
  
  For example, if your document title and description are English, provide the names in English, too.
- **Use commas** (`,`) for separating names, don't use semicolon (`;`) or other separator characters.

  For example, provide it as *"Lüneburg Heath, Germany"* instead of *"Lüneburg Heath; Germany"* or *"Lüneburg Heath in Germany"*.
- List the names **from the most specific part to the most unspecific part**.
  
  For example, *"Hyde Park, London, United Kingdom"*.
- **Do not use abbreviations**.
  
  For example, use "United Kingdom" instead of "UK" or "United States" instead of "US".
- **Capitalize names** as required by the language.

  For example, write "United States of America" instead of "United states of america"

##### copernicus:country

The ISO 3166-1 alpha-2 country code can be found at <https://www.iso.org/obp/ui/#search>.
Search for country codes at  via the Alpha-2 code column.

##### copernicus:subdivision

The ISO 3166-2 codes can be found at <https://www.iso.org/obp/ui/#iso:pub:PUB500001:en>.
Only provide the second part of the ISO 3166-2 code to reduce redundancy.

Please note that for some countries subdivision codes are not available.
