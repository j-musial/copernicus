<!--
Harvested from https://github.com/stac-extensions/xarray-assets (v1.0.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Xarray Assets (v1.0.0)

- **Source repository:** [stac-extensions/xarray-assets](https://github.com/stac-extensions/xarray-assets)
- **Upstream version:** v1.0.0
- **Upstream schema:** <https://stac-extensions.github.io/xarray-assets/v1.0.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Xarray Assets* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** xarray Assets
- **Identifier:** <https://stac-extensions.github.io/xarray-assets/v1.0.0/schema.json>
- **Field Name Prefix:** xarray
- **Scope:** Asset
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Deprecated
- **Owner**: @TomAugspurger


## Deprecation Notice

This extension has been deprecated. While useful, it ended up being to specific to xarray and Python.
Instead of this extension, we recommend the following extensions and libraries to enable opening
xarray Datasets from a STAC item / asset:

1. A yet to create `zarr` extension to capture metadata about a Zarr hierarchy, like whether it is `consolidated`. Proposals are welcome.
2. The [`storage` extension](https://github.com/stac-extensions/storage) for additional storage-specific information
3. The [xpystac](https://github.com/stac-utils/xpystac) library for opening xarray datasets from STAC metadata, rather than manually extracting information and calling `xarray.open_dataset` directly.

## Description

This document explains the xarray Assets Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

This extension helps users open STAC Assets with [xarray](https://xarray.pydata.org/en/stable/). It gives a place
for catalog maintainers to specify various required or recommended options. Without this extension,
users would somehow need to know which options are required in order to load the dataset.
See [Python Example](#python-example) for an example of how consumers of this extension can use it to simplify data loading.

See also [xpystac](https://github.com/stac-utils/xpystac), which enables opening a variety of STAC assets with xarray.

- Examples:
  - [Item example](https://github.com/stac-extensions/xarray-assets/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/xarray-assets/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/xarray-assets/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/xarray-assets/blob/main/CHANGELOG.md)

### Item Properties and Collection Fields

| Field Name               | Type                      | Description                                           |
| ------------------------ | ------------------------- | ----------------------------------------------------- |
| copernicus:open_kwargs       | Map<string, Any>          | Keyword arguments to provide to the xarray opener     |
| copernicus:storage_options   | Map<string, Any>          | Additional keywords to provide to `fsspec.filesystem` |

#### Additional Field Information

##### copernicus:open_kwargs

Keyword arguments to provide to the xarray opener, for example  [`xarray.open_zarr`](https://xarray.pydata.org/en/stable/generated/xarray.open_zarr.html).
The opener should be determined by the media type of the asset.

The are in addition to the positional argument, for example the `store`, which is obtained from the Assets `href`. For example, to specify [consolidated metadata](https://zarr.readthedocs.io/en/stable/tutorial.html):

```json
{
  "copernicus:open_kwargs": {
    "consolidated": true
  }
}
```

##### copernicus:storage_options

[`fsspec.filesystem`](https://filesystem-spec.readthedocs.io/en/latest/api.html#fsspec.filesystem) enables opening a filesystem from URI (e.g. `abfs://path/to/blob`, `https://path/to/file`, `s3://path/to/file`). The various filesystems support and require backend-specific keyword arguments, which can be provided as `**storage_options`.

### Python Example

This example demonstrates how consumers of this extension can use the data to simplify the process of loading
an asset from STAC into an xarray Dataset.

```python
>>> import pystac, planetary_computer, xarray as xr

>>> collection = planetary_computer.sign(
...     pystac.read_file("https://planetarycomputer.microsoft.com/api/stac/v1/collections/terraclimate")
... )
>>> asset = collection.assets["zarr-abfs"]
>>> asset.media_type

>>> ds = xr.open_dataset(
...    asset.href,
...    **asset.extra_fields["copernicus:open_kwargs"]
... )
>>> ds
<xarray.Dataset> Size: 2TB
Dimensions:  (time: 768, lat: 4320, lon: 8640, crs: 1)
Coordinates:
  * crs      (crs) int16 2B 3
  * lat      (lat) float64 35kB 89.98 89.94 89.9 89.85 ... -89.9 -89.94 -89.98
  * lon      (lon) float64 69kB -180.0 -179.9 -179.9 ... 179.9 179.9 180.0
  * time     (time) datetime64[ns] 6kB 1958-01-01 1958-02-01 ... 2021-12-01
Data variables: (12/14)
    aet      (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    def      (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    pdsi     (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    pet      (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    ppt      (time, lat, lon) float64 229GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    q        (time, lat, lon) float64 229GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    ...       ...
    swe      (time, lat, lon) float64 229GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    tmax     (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    tmin     (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    vap      (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    vpd      (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
    ws       (time, lat, lon) float32 115GB dask.array<chunksize=(12, 1024, 1024), meta=np.ndarray>
Attributes: (12/52)
    Conventions:                     CF-1.6
    acknowledgment:                  Please cite the references included here...
    cdm_data_type:                   GRID
    contributor_email:               khegewisch@ucmerced.edu
    contributor_name:                Katherine Hegewisch
    contributor_role:                Postdoctoral Fellow
    ...                              ...
    time_coverage_duration:          P1Y
    time_coverage_end:               1958-12-01T00:0
    time_coverage_resolution:        P1M
    time_coverage_start:             1958-01-01T00:0
    title:                           TerraClimate: monthly climate and climat...
    version:                         v1.0
```
