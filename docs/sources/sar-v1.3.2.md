<!--
Harvested from https://github.com/stac-extensions/sar (v1.3.2) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Synthetic Aperture Radar (v1.3.2)

- **Source repository:** [stac-extensions/sar](https://github.com/stac-extensions/sar)
- **Upstream version:** v1.3.2
- **Upstream schema:** <https://stac-extensions.github.io/sar/v1.3.2/schema.json>
- **License:** Apache-2.0

The following is the specification text of the *Synthetic Aperture Radar* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** SAR
- **Identifier:** <https://stac-extensions.github.io/sar/v1.3.2/schema.json>
- **Field Name Prefix:** sar
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/blob/master/extensions/README.md#extension-maturity):** Stable
- **Owner**: @m-mohr, @emmanuelmathot
- **History**: [Prior to March 2, 2021](https://github.com/radiantearth/stac-spec/commits/v1.0.0-rc.1/extensions/sar)

This document explains the fields of the Synthetic-Aperture Radar (SAR) Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

SAR data is considered to be data that represents a snapshot of the earth for a single date and time taken by a synthetic-aperture radar system
such as Sentinel-1, RADARSAT or EnviSAT.

If the data has been collected by a satellite, it is recommended to use the
[Satellite extension](https://github.com/stac-extensions/sat).
If the data has been collected on an airborne platform it is recommended to use the
[Instrument Fields](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#instrument).

To describe frame start and end times, use the
[Date and Time Range fields](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#date-and-time-range).

To describe the product type, use the [Product extension](https://github.com/stac-extensions/product).

- Examples:
  - [Envisat](https://github.com/stac-extensions/sar/blob/main/examples/envisat.json)
  - [Sentinel-1 GRD EW](https://github.com/stac-extensions/sar/blob/main/examples/sentinel-1-grd-ew.json)
  - [Sentinel-1 GRD S4](https://github.com/stac-extensions/sar/blob/main/examples/sentinel-1-grd-s4.json)
  - [Sentinel-1 SLC IW](https://github.com/stac-extensions/sar/blob/main/examples/sentinel-1-slc-iw.json)
- [JSON Schema](https://github.com/stac-extensions/sar/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/sar/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

> \[!IMPORTANT]  
>
> In this specification *range* values are meant to be measured perpendicular to the flight path
> and *azimuth* values are meant to be measured parallel to the flight path.

| Field Name                  | Type      | Description |
| --------------------------- | --------- | ----------- |
| copernicus:polarizations           | \[string] | RECOMMENDED. Any combination of polarizations. |
| copernicus:frequency_band          | string    | RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names. |
| copernicus:center_frequency        | number    | RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz). |
| copernicus:bandwidth               | number    | The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation. |
| copernicus:resolution_range        | number    | The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m). |
| copernicus:resolution_azimuth      | number    | The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m). |
| copernicus:pixel_spacing_range     | number    | The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| copernicus:pixel_spacing_azimuth   | number    | The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| copernicus:looks_range             | number    | Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path. |
| copernicus:looks_azimuth           | number    | Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path. |
| copernicus:looks_equivalent_number | number    | The equivalent number of looks (ENL). |
| copernicus:observation_direction   | string    | Antenna pointing direction relative to the flight trajectory of the satellite, either `left` or `right`. |
| copernicus:relative_burst          | number    | Identification number that uniquely identifies a burst cycle within each repeat cycle. |
| copernicus:beam_ids                | \[string] | Composition of the swath of the SAR acquision referencing the beam identifiers. |
| copernicus:product_type            | string    | ***DEPRECATED** in favor of [`copernicus:product_type`](https://github.com/stac-extensions/product).* See [Product type](#product-type). |
| copernicus:instrument_mode         | string    | ***DEPRECATED** in favor of [`instrument_modes`](https://github.com/stac-extensions/instruments#instrument_modes).* |

> \[!CAUTION]  
>
> - v1.0 of the extension did require `copernicus:product_type`.
> - v1.1 deprecates `copernicus:product_type` and it's not required any longer, but
>   [`copernicus:product_type`](https://github.com/stac-extensions/product) is **strongly recommended**.
> - v2.0 is going to remove `copernicus:product_type`.
>
> ---
>
> - v1.0 of the extension did recommend `copernicus:instrument_mode`.
> - v1.3.2 deprecates `copernicus:instrument_mode`, but
>   [`instrument_modes`](https://github.com/stac-extensions/instruments) is **strongly recommended**.
> - v2.0 is going to remove `copernicus:instrument_mode`.

#### Additional Field Information

##### copernicus:polarizations

Specifies a single polarization or a polarization combination.
Allowed values: `HH`, `VV`, `HV`, `VH`, `LH`, `LV`, `RH`, `RV`, `CH` or `CV`
For single polarized radars, one the allowed values must be set.
For dual polarized radars and alternating polarization, add the corresponding polarizations to the array.
For fully polarimetric radars, add all polarizations to the array.
For instance, for `HH+HV`, add both `HH` and `HV`.

> \[!IMPORTANT]  
>
> In Item Properties and Collections, `copernicus:polarizations` must be a set with unique elements.
> In assets `copernicus:polarizations` can contain duplicate elements and, if possible, the polarizations must appear in the same order as in the file.

##### copernicus:beam_ids

The `copernicus:beam_ids` field is used to reference the beam identifiers of the SAR acquisition. According to the mission and the sensor mode,
the beam identifiers can be used to identify the composition of the swath of the SAR acquisition.
The beam identifiers are usually provided in the metadata of the SAR data.

#### copernicus:frequency_band - Common Frequency Band Names

The `copernicus:frequency_band` is the name that is commonly used to refer to that band's spectral
properties. The table below shows the common name based on the wavelength and frequency ranges for several SAR satellites.

| Common Name | Wavelength Range (cm) | Frequency Range (GHz) | Satellites                                         |
| ----------- | --------------------- | --------------------- | -------------------------------------------------- |
| P           | 30 - 120              | 0.25 - 1              |                                                    |
| L           | 15 - 30               | 1 - 2                 | ALOS, JERS, NISAR, SOACOM                          |
| S           | 7.5 - 15              | 2 - 4                 | HJ-1C                                              |
| C           | 3.8 - 7.5             | 4 - 8                 | EnviSat, ERS, Radarsat, Risat-1, Sentinel-1        |
| X           | 2.4 - 3.8             | 8 - 12.5              | Cosmo-SkyMed, TerraSAR-X, TanDEM-X, PAZ, KOMPSat-5 |
| Ku          | 1.7 - 2.4             | 12.5 - 18             |                                                    |
| K           | 1.1 - 1.7             | 18 - 26.5             |                                                    |
| Ka          | 0.75 - 1.1            | 26.5 - 40             |                                                    |

#### Product type

It is RECOMMENDED to include the `copernicus:product_type` field.
The product type for SAR data defines the type of processed data contained in the assets.
A list of suggestions for [`copernicus:product_type`](https://github.com/stac-extensions/product) include:

| copernicus:product_type | Type      | Description                                                     |
| ------------ | --------- | --------------------------------------------------------------- |
| SSC          | complex   | Single-look Slant-range Complex image (standard SLC)            |
| MGD          | amplitude | Multilooked Ground-range Detected image                         |
| GRD          | amplitude | Multilooked Ground-range Detected image (used by Sentinel-1)    |
| GEC          | amplitude | Geocoded Ellipsoid Corrected image                              |
| GTC          | amplitude | Geocoded Terrain Corrected image                                |
| RTC          | amplitude | Geocoded Radiometrically Terrain Corrected image                |
| SGC          | complex   | Single-look Ground projected Complex image                      |
| SLC          | complex   | Single-look Ground projected Complex image (used by Sentinel-1) |

This can vary by data provider, who all may use slightly different names.
Sentinel-1 for instance uses `GRD`, which is the same as the more general `MGD` and `SLC` instead of `SGC`.

#### Date and Time

In SAR, you usually have frame start and end time. To describe this information it is recommended to use the [Date and Time Range fields](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#date-and-time-range).
The center time of the frame should be specified with the `datetime` property for STAC Items.

### Best Practices

One of the emerging best practices is to use [Asset Roles](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md#asset-roles)
to provide clients with more information about the assets in an item. The following list includes a shared vocabulary for some common SAR assets.
This list should not be considered definitive, and implementors are welcome to use other asset roles. If consensus and tooling consolidates around
these role names then they will be specified in the future as more standard than just 'best practices'.

| Role Name                 | Description                                                                                                                                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| local-incidence-angle     | Points to the local incidence angle file.                                                                                                                                                       |
| ellipsoid-incidence-angle | Points to the ellipsoid incidence angle file.                                                                                                                                                   |
| noise-power               | Points to the noise power file.                                                                                                                                                                 |
| amplitude                 | Points to the intensity file with focused SAR data that has been ground range detected (e.g. GRD).                                                                                              |
| magnitude                 | Points to the intensity file where data are represented as complex numbers containing amplitude and phase information (e.g SLC).                                                                |
| sigma0                    | Points to the radar backscatter file where data is referenced in ground surface. It is often derived from an `amplitude` or a `magnitude` role asset.                                           |
| beta0                     | Points to the radar backscatter file where data is referenced in the slant range plane and is radiometrically calibrated.  It is often derived from an `amplitude` or a `magnitude` role asset. |
| gamma0                    | Points to the radar backscatter file where data is referenced in the plane perpendicular to the line of sight. It is often derived from an `amplitude` or a `magnitude` role asset.             |
| date-offset               | Points to the date-offset file.                                                                                                                                                                 |
| covmat                    | Points to the Points to the Normalized Polarimetric Radar Covariance Matrix (CovMat) file.                                                                                                      |
| prd                       | Points to the Polarimetric Radar Decomposition (PRD) file.                                                                                                                                      |
