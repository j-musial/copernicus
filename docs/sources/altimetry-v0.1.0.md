<!--
Harvested from https://github.com/stac-extensions/altimetry (v0.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Altimetry (v0.1.0)

- **Source repository:** [stac-extensions/altimetry](https://github.com/stac-extensions/altimetry)
- **Upstream version:** v0.1.0
- **Upstream schema:** <https://stac-extensions.github.io/altimetry/v0.1.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Altimetry* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Altimetry
- **Identifier:** <https://stac-extensions.github.io/altimetry/v0.1.0/schema.json>
- **Field Name Prefix:** altm
- **Scope:** Item
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @emmanuelmathot

This document explains the [Altimetry](https://www.aviso.altimetry.fr/en/techniques/altimetry/principle.html) Extension 
to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

- Examples:
  - [Sentinel-3 example](https://github.com/stac-extensions/altimetry/blob/main/examples/sentinel3.json): Shows the basic usage of the extension in a STAC Item with Sentinel-3 data.
- [JSON Schema](https://github.com/stac-extensions/altimetry/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/altimetry/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [ ] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name           | Type                                                                                                | Description                                                                                                                                                                                                                                                                                 |
| -------------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| copernicus:instrument_type | string                                                                                              | Primary instrument type. See the list of [primary instrument types](#primary-instrument-types).                                                                                                                                                                                             |
| copernicus:instrument_mode | string                                                                                              | Instrument mode.                                                                                                                                                                                                                                                                            |
| copernicus:sampling_rate   | number                                                                                              | Sampling rate of the instrument in Hz.                                                                                                                                                                                                                                                      |
| copernicus:nominal_track   | [GeoJSON LineString Coordinates Array](https://datatracker.ietf.org/doc/html/rfc7946#section-3.1.4) | An array of coordinates used to define the nominal track on the earths surface. This value is recommended ONLY if the item geometry is not representative of the acquisition track. |

> \[!NOTE]
> Various fields and objects in this extensions replace [deprecated fields](https://github.com/stac-extensions/sentinel-3/blob/main/deprecated.md)
> from the [sentinel-3 extension](https://github.com/stac-extensions/sentinel-3).
> Please see the section [sentinel-3 mapping](#sentinel-3-mapping) for more information.

#### Primary Instrument Types

The following values are valid for the `copernicus:instrument_type` field:

| Value     | Description              |
| --------- | ------------------------ |
| sar       | Synthetic Aperture Radar |
| doppler   | Doppler                  |
| laser     | Laser                    |
| microwave | Microwave Radiometer     |
| other     |                          |

#### Sentinel-3 Mapping

The following table shows the mapping between the [deprecated fields](https://github.com/stac-extensions/sentinel-3/blob/main/deprecated.md)
in the [Sentinel-3 extension](https://github.com/stac-extensions/sentinel-3) and the fields in the Altimetry extension.

| Sentinel-3 Field Name | Altimetry Field Name   | Altimetry Field Value |
| --------------------- | ---------------------- | --------------------- |
| `s3:lrm_mode`         | `copernicus:instrument_mode` | `lrm`                 |
| `s3:sar_mode`         | `copernicus:instrument_mode` | `sar`                 |
