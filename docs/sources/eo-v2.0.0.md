<!--
Harvested from https://github.com/stac-extensions/eo (v2.0.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Electro-Optical (v2.0.0)

- **Source repository:** [stac-extensions/eo](https://github.com/stac-extensions/eo)
- **Upstream version:** v2.0.0
- **Upstream schema:** <https://stac-extensions.github.io/eo/v2.0.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Electro-Optical* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Electro-Optical
- **Identifier:** <https://stac-extensions.github.io/eo/v2.0.0/schema.json>
- **Field Name Prefix:** eo
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Stable
- **Owner**: @matthewhanson
- **History:** [Prior to March 30, 2021](https://github.com/radiantearth/stac-spec/commits/v1.0.0-rc.2/extensions/eo)

This document explains the fields of the Electro-Optical (EO) Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

EO data is considered to be data that represents a snapshot of the Earth for a single date and time. It
could consist of multiple spectral bands in any part of the electromagnetic spectrum. Examples of EO
data include sensors with visible, short-wave and mid-wave IR bands (e.g., the OLI instrument on
Landsat-8), long-wave IR bands (e.g. TIRS aboard Landsat-8).

It is strongly recommended to use [Instrument Fields](https://github.com/radiantearth/stac-spec/tree/master/item-spec/common-metadata.md#instrument)
with the EO extension, to provide information about the platform (satellite, aerial, etc) used to capture the images.

For defining view geometry of data, it is strongly recommended to use the [View Extension](https://github.com/stac-extensions/view).

- Examples:
  - [Collection example](https://github.com/stac-extensions/eo/blob/main/examples/collection.json)
  - [Item example](https://github.com/stac-extensions/eo/blob/main/examples/item.json)
- [JSON Schema](https://github.com/stac-extensions/eo/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/eo/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [ ] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [x] Bands
- [ ] Links

| Field Name             | Type   | Description                                                                                                                                                        |
| ---------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| copernicus:cloud_cover         | number | Estimate of cloud cover as a percentage (0-100).                                                                                                                   |
| copernicus:snow_cover          | number | Estimate of snow and ice cover as a percentage (0-100).                                                                                                            |
| copernicus:common_name         | string | The name commonly used to refer to the band to make it easier to search for bands across instruments. See the [list of accepted common names](#common-band-names). |
| copernicus:center_wavelength   | number | The center wavelength of the band, in micrometers (μm).                                                                                                            |
| copernicus:full_width_half_max | number | Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm).                                       |
| copernicus:solar_illumination  | number | The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers.                                                             |

*At least one of the fields must be specified.*

#### Coverages

This extension defines some common coverage types (cloud and snow/ice cover) as a percentages (0-100) of the entire scene:
- `copernicus:cloud_cover`
- `copernicus:snow_cover`

It is important to consider only the valid data regions, excluding any "nodata" areas while calculating both the coverages.
If such information is not available or can't be calculated, the fields should not be provided.

Usually, the properties should be used in Item Properties rather than Item Assets,
as an Item from an electro-optical source is a single snapshot of the Earth, so the coverages usually apply to all assets.

#### Spectral Bands

> \[!NOTE]
> This extension formerly had a field `bands`, which has been removed in favor of a general field `bands`
> in STAC common metadata. The structure is the same, it's an array of Band Objects.
> The fields in the Band Object may change, fields from the EO extension will have a `eo:` prefix, but some more
> general fields like `description` have been moved to common metadata and don't need a prefix and as such don't change.
> Please note that bands in Item Properties are not the union of all bands in the assets any longer.
> If you specify bands in the Item Properties, the bands apply to all assets unless you have a bands object at the asset level.

The presence of one of the `eo:` fields in a Band Object makes the band
"[spectral](https://www.sciencedirect.com/topics/earth-and-planetary-sciences/spectral-band)".
This enables clients to read the file and understand which band is 'red' and which is 'nir' (near infrared) so that it can perform an
[NDVI](https://en.wikipedia.org/wiki/Normalized_difference_vegetation_index) operation, for example.
Each Asset should specify its own band object.
If the individual bands are repeated in different assets they should all use the same values and
include the optional bands `name` field to enable clients to easily combine and summarize the bands.

##### copernicus:center_wavelength and copernicus:full_width_half_max

These fields are a common way to approximately describe a spectral band. In most cases even these numbers are not as useful as the
`copernicus:common_name` that should be supplied with the spectral bands, where they exist. For non-standard bands (such as with hyperspectral sensors)
the wavelength fields indicate where the band is.

Another common way to define a spectral band with a minimum and maximum wavelength, where outside these bounds the transmission is 0%,
and non-zero inside the bounds (e.g., 80%). The maximum transmission of a band is not captured in any of these metrics,
nor is it important in most cases.

However, spectral transmission for a filter does not go from 0% to a constant max value (e.g., 80%) then back to 0%. Such a filter is
referred to as a "top-hat" filter due to it's shape, but does not exist in reality. Thus, the minimum and maximum wavelengths are
typically selected to be the point at which transmission drops below some threshold, and this threshold is often half of the maximum
transmission. Thus if a filter's maximum transmission is 80%, the min and max thresholds would be the points where the transmission drops below 40%.

The `copernicus:center_wavelength` of a band is the midpoint between the min and max wavelengths:

```python
center_wavelength = (min_wavelength + max_wavelength) / 2
```

The `copernicus:full_width_half_max` (FWHM) is the difference between the min and max wavelengths,
thus representing the width of the band at half it's maximum transmission.

```python
full_width_half_max = max_wavelength - min_wavelength
```

For example, if we were given a band described as (0.4um - 0.5um) the `copernicus:center_wavelength` would be 0.45um
and the `copernicus:full_width_half_max` would be 0.1um.

In some cases the full transmission profile is needed, such as when harmonizing between two sensor modalities. It is recommended
 that the full spectral profile be included as a link or an asset (preferably at the
 [Collection](https://github.com/radiantearth/stac-spec/tree/master/collection-spec/collection-spec.md) level).

##### copernicus:solar_illumination

In satellite-based remote sensing applications, the calibration of the sensor recorded top-of-atmosphere reflectance to radiance, or vice-versa,
is carried out using a reference spectral solar irradiance value.
It depends of the extra-terrestrial solar irradiance (e.g. [[Thuillier et al., 2003](https://link.springer.com/article/10.1023/A:1024048429145)])
at a specific spectral wavelength,
of the illumination conditions during the calibration data acquisition (through platform navigation and attitude),
of the instrument viewing geometry on the diffuser panel.
The value in this field is the mean value representing the solar illumination in W/m2/micrometers
at a specific level (e.g. Top of Atmosphere) for the asset.
For instance, this value is used for optical calibration of an asset (e.g. [ESUN(b) value in OTB optical calibration application](https://www.orfeo-toolbox.org/CookBook/Applications/app_OpticalCalibration.html#description))

##### Common Band Names

The band's `copernicus:common_name` is the name that is commonly used to refer to that band's spectral
properties. The table below shows the allowed common names based on the average band range for the band
numbers of several popular instruments.

| Common Name | Band Range (μm) | Landsat 5 TM / 7 ETM+ | Landsat 8 | Landsat Next | Sentinel-2 | Sentinel-3 OLCI / SLSTR | MODIS | NAIP | Planetscope | Worldview 2 / 3 |
| ----------- | --------------- | --------------------- | --------- | ------------ | ---------- | ----------------------- | ----- | ---- | ----------- | --------------- |
| pan         | 0.40 - 1.00     | - / 8                 | 8         |              |            |                         |       |      |             | (1)             |
| coastal     | 0.40 - 0.45     |                       | 1         | 2            | 1          | 3 / -                   |       |      | 1           | 1               |
| blue        | 0.45 - 0.53     | 1                     | 2         | 3            | 2          | 4 / -                   | 3     | 3    | 2           | 2               |
| green       | 0.51 - 0.60     | 2                     | 3         | 4            | 3          | 6 / 1                   | 4     | 2    | 4           | 3               |
| green05     | 0.51 - 0.55     |                       |           |              |            | 5 / -                   | 11    |      | 3           |                 |
| yellow      | 0.58 - 0.62     |                       |           | 5            |            | 7 / -                   |       |      | 5           | 4               |
| red         | 0.62 - 0.69     | 3                     | 4         | 8            | 4          | 9 / 2                   | 1     | 1    | 6           | 5               |
| rededge     | 0.69 - 0.79     |                       |           |              |            |                         |       |      |             | 6               |
| rededge071  | 0.69 - 0.73     |                       |           | 9            | 5          | 11 / -                  |       |      | 7           |                 |
| rededge075  | 0.73 - 0.76     |                       |           | 10           | 6          | 12 / -                  |       |      |             |                 |
| rededge078  | 0.76 - 0.79     |                       |           |              | 7          | 16 / -                  |       |      |             |                 |
| nir         | 0.76 - 1.00     | 4                     |           | 11           | 8          |                         | 2     | 4    |             | 7               |
| nir08       | 0.80 - 0.90     |                       | 5         | 12           | 8a         | 17 / 3                  |       |      | 8           |                 |
| nir09       | 0.90 - 1.00     |                       |           | 13           | 9          | 20 / -                  |       |      |             |                 |
| cirrus      | 1.35 - 1.40     |                       | 9         | 17           | 10         | - / 4                   | 26    |      |             |                 |
| swir16      | 1.55 - 1.75     | 5                     | 6         | 18           | 11         | - / 5                   | 6     |      |             |                 |
| swir22      | 2.08 - 2.35     | 7                     | 7         | 21           | 12         | - / 6                   | 7     |      |             |                 |
| lwir        | 10.4 - 12.5     | 6                     |           |              |            |                         |       |      |             |                 |
| lwir11      | 10.5 - 11.5     |                       | 10        | 25           |            |                         | 31    |      |             |                 |
| lwir12      | 11.5 - 12.5     |                       | 11        | 26           |            |                         | 32    |      |             |                 |

The difference between the `nir`, `nir08`, and `nir09` bands are that the `nir` band is a wider band that covers
most of the spectral range of 0.76μm to 1.0μm. `nir08` and `nir09` are narrow bands centered 0.85μm and 0.95μm
respectively. The same applies for all variants that have numerical suffixes, e.g. green, lwir and rededge.

Common band names should be uniquely assigned, i.e. there should never be two bands that share the same common
name in an Item or Collection.

### Best Practices

One of the emerging best practices is to use [Asset Roles](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#asset-roles)
to provide clients with more information about the assets in an item. The following list includes a shared vocabulary for some common EO assets.
This list should not be considered definitive, and implementors are welcome to use other asset roles. If consensus and tooling consolidates around
these role names then they will be specified in the future as more standard than just 'best practices'.

| Role Name    | Description                                                                                                                                                                                            |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| reflectance  | An asset the provides [reflectance](https://www.l3harrisgeospatial.com/Support/Self-Help-Tools/Help-Articles/Help-Articles-Detail/ArtMID/10220/ArticleID/19247/3377) values, instead of just radiance. |
| temperature  | An asset that provides actual temperature measurements.                                                                                                                                                |
| saturation   | Points to a file that indicates where pixels in the input spectral bands are saturated.                                                                                                                |
| cloud        | Points to a file that indicates whether a pixel is assessed as being cloud                                                                                                                             |
| cloud-shadow | Points to a file that indicates whether a pixel is assessed as being cloud shadow.                                                                                                                     |
