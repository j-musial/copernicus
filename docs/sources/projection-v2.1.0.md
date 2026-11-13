<!--
Harvested from https://github.com/stac-extensions/projection (v2.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Projection (v2.1.0)

- **Source repository:** [stac-extensions/projection](https://github.com/stac-extensions/projection)
- **Upstream version:** v2.1.0
- **Upstream schema:** <https://stac-extensions.github.io/projection/v2.1.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Projection* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Projection
- **Identifier:** <https://stac-extensions.github.io/projection/v2.1.0/schema.json>
- **Field Name Prefix:** proj
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Stable
- **Owner**: @matthewhanson
- **History:** [Prior to March 30, 2021](https://github.com/radiantearth/stac-spec/commits/v1.0.0-rc.2/extensions/projection)

This document explains the Projection Extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

When specified in Item Properties, the values are assumed to apply to all Assets in that Item. For example, an Item may have
several related Assets each representing a band or layer for the Item, and which typically all use the same CRS,
e.g., a UTM Zone. However, there may also be Assets intended for display, like a preview image or thumbnail, that have
been reprojected to a different CRS, e.g., Web Mercator, or resized to better accommodate that use case. In this case, the
fields should be specified at the Item Asset level, while those Item Asset objects that use the defaults can remain unspecified.

The `proj` prefix is short for "projection", and is not a reference to the PROJ/PROJ4 formats.

- Examples:
  - [Item example](https://github.com/stac-extensions/projection/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Assets in Item example](https://github.com/stac-extensions/projection/blob/main/examples/assets.json): Shows the basic usage of the extension in STAC Assets (in a STAC Item)
  - [Collection example](https://github.com/stac-extensions/projection/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection (Item Assets Definiton and Summaries)
  - [Bands example](https://github.com/stac-extensions/projection/blob/main/examples/bands.json): Shows the usage of the extension in Bands (in a STAC Item Asset)
- [JSON Schema](https://github.com/stac-extensions/projection/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/projection/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections and Asset Templates)
- [x] Links (incl. Link Templates)
- [x] Bands

| Field Name     | Type          | Description |
| -------------- | ------------- | ----------- |
| copernicus:code      | string\|null  | Authority and specific code of the data source (e.g., `EPSG:3857`) |
| copernicus:wkt2      | string\|null  | [WKT2](http://docs.opengeospatial.org/is/12-063r5/12-063r5.html) string representing the Coordinate Reference System (CRS) that the `copernicus:geometry` and `copernicus:bbox` fields represent |
| copernicus:projjson  | [PROJJSON Object](https://proj.org/specifications/projjson.html)\|null | PROJJSON object representing the Coordinate Reference System (CRS) that the `copernicus:geometry` and `copernicus:bbox` fields represent |
| copernicus:geometry  | [GeoJSON Geometry Object](https://tools.ietf.org/html/rfc7946#section-3.1) | Defines the footprint of this Item. |
| copernicus:bbox      | \[number]     | Bounding box of the Item in the asset CRS in 2 or 3 dimensions. |
| copernicus:centroid  | [Centroid Object](#centroid-object) | Coordinates representing the centroid of the Item (in lat/long) |
| copernicus:shape     | \[integer]    | Number of pixels in Y and X directions for the default grid |
| copernicus:transform | \[number]     | The affine transformation coefficients for the default grid  |

At least one of the fields MUST be specified, but it is RECOMMENDED to provide more information as detailed in the
[Best Practices section](#best-practices) so that, for example, GDAL can read your data without issues.

Generally, it is preferrable to provide the projection information on the Asset level
as they are specific to assets and may not apply to all assets.
For example, if you provide a smaller and unlocated thumbnail, having the projection information in the Item Properties
would imply that the projection information also applies to the thumbnail if not specified otherwise in the asset.
You may want to add the `copernicus:code` to the Item Properties though as this would provide an easy way to
filter for specific projection codes in an API. In this case you could override the `copernicus:code` for the thumbnail on the asset level.

> \[!WARNING]
> The field `proj:epsg` has been deprecated in v1.2.0 in favor of `copernicus:code` and has been removed in v2.0.0.
> For example, the former field `"proj:epsg": 32659` must be migrated to `"copernicus:code": "EPSG:32659"`.

#### Additional Field Information

##### copernicus:code

Projection codes are identified by a string. The [PROJ](https://proj.org/) library defines projections
using "authority:code", e.g., "EPSG:4326" or "IAU_2015:30100". Different projection authorities may define
different string formats. Examples of known projection authorities, where when can find well known codes that
clients are likely to support are listed in the following table.

| Authority Name                          | URL                                                        |
| --------------------------------------- | ---------------------------------------------------------- |
| European Petroleum Survey Groups (EPSG) | <http://www.opengis.net/def/crs/EPSG> or <http://epsg.org> |
| International Astronomical Union (IAU)  | <http://www.opengis.net/def/crs/IAU>                       |
| Open Geospatial Consortium (OGC)        | <http://www.opengis.net/def/crs/OGC>                       |
| ESRI                                    | <https://spatialreference.org/ref/esri/>                   |

The `copernicus:code` field SHOULD be set to `null` in the following cases:

- The asset data does not have a CRS, such as in the case of non-rectified imagery with Ground Control Points.
- A CRS exists, but there is no valid EPSG code for it. In this case, the CRS should be provided in `copernicus:wkt2` and/or `copernicus:projjson`.
  Clients can prefer to take either, although there may be discrepancies in how each might be interpreted.

##### copernicus:wkt2

A Coordinate Reference System (CRS) is the data reference system (sometimes called a 'projection')
used by the asset data. This value is a [WKT2](http://docs.opengeospatial.org/is/12-063r5/12-063r5.html) string.

This field SHOULD be set to `null` in the following cases:

- The asset data does not have a CRS, such as in the case of non-rectified imagery with Ground Control Points.
- A CRS exists, but there is no valid WKT2 string for it.

##### copernicus:projjson

A Coordinate Reference System (CRS) is the data reference system (sometimes called a 'projection')
used by the asset data. This value is a [PROJJSON](https://proj.org/specifications/projjson.html) object,
see the [JSON Schema](https://proj.org/schemas/v0.5/projjson.schema.json) for details.

This field SHOULD be set to `null` in the following cases:

- The asset data does not have a CRS, such as in the case of non-rectified imagery with Ground Control Points.
- A CRS exists, but there is no valid WKT2 string for it.

##### copernicus:geometry

A GeoJSON Geometry object as defined in [RFC 7946, sections 3.1](https://tools.ietf.org/html/rfc7946)
representing the footprint of this Item, except not necessarily in EPSG:4326 as required by RFC7946.
Specified based on the `copernicus:code`, `copernicus:projjson` or `copernicus:wkt2` fields (not necessarily EPSG:4326).
Usually, this will be represented by a Polygon with five coordinates, as the item in the asset data CRS should be
a square aligned to the original CRS grid.
If the CRS is WGS 84, this field SHOULD be omitted in Items, see [Data in WGS 84](#data-in-wgs-84).

##### copernicus:bbox

Bounding box of the assets represented by this Item in the asset data CRS. Specified as 4 or 6
coordinates based on the CRS defined in the `copernicus:code`, `copernicus:projjson` or `copernicus:wkt2` fields.  First two numbers are coordinates
of the lower left corner, followed by coordinates of upper right corner, , e.g., \[west, south, east, north],
\[xmin, ymin, xmax, ymax], \[left, down, right, up], or \[west, south, lowest, east, north, highest].
The length of the array must be 2\*n where n is the number of dimensions. The array contains all axes of the southwesterly
most extent followed by all axes of the northeasterly most extent specified in Longitude/Latitude or Longitude/Latitude/Elevation
based on [WGS 84](http://www.opengis.net/def/crs/OGC/1.3/CRS84). When using 3D geometries, the elevation of the southwesterly most
extent is the minimum elevation in meters and the elevation of the northeasterly most extent is the maximum in meters.
If the CRS is WGS 84, this field SHOULD be omitted in Items, see [Data in WGS 84](#data-in-wgs-84).

##### copernicus:centroid

Coordinates representing the centroid of the Item. Coordinates are defined in latitude and longitude, even if
the data coordinate system does not use lat/long. This is to enable less sophisticated mapping tools to be able to render the
location of the Item, as some only handle points. Note that the centroid is best calculated in the native CRS and then projected
into lat/long, as some projections can wrap the centroid location.

##### copernicus:shape

An array of integers that represents the number of pixels in the most common pixel grid used by the Item Asset objects.
The number of pixels should be specified in Y, X order. If the shape is defined in Item Properties, it is used as
the default shape for all assets that don't have an overriding shape. This can be be easily determined with 
[`gdalinfo`](https://gdal.org/programs/gdalinfo.html) (the 'size' result) or [`rio info`](https://rasterio.readthedocs.io/en/latest/cli.html#info)
(the 'shape' field) on the command line.

##### copernicus:transform

Linear mapping from pixel coordinate space (Pixel, Line) to projection coordinate space (Xp, Yp). It is
a `3x3` matrix stored as a flat array of 9 elements in row major order. Since the last row is always `0,0,1` it can be omitted,
in which case only 6 elements are recorded. This mapping can be obtained from 
GDAL([`GetGeoTransform`](https://gdal.org/api/gdaldataset_cpp.html#_CPPv4N11GDALDataset15GetGeoTransformEPd), requires re-ordering)
or the Rasterio ([`Transform`](https://rasterio.readthedocs.io/en/stable/api/rasterio.io.html#rasterio.io.BufferedDatasetWriter.transform)).
To get it on the command line you can use the [Rasterio CLI](https://rasterio.readthedocs.io/en/latest/cli.html) with the
[info](https://rasterio.readthedocs.io/en/latest/cli.html#info) command: `$ rio info`.

```txt
  [Xp]   [a0, a1, a2]   [Pixel]
  [Yp] = [a3, a4, a5] * [Line ]
  [1 ]   [0 ,  0,  1]   [1    ]
```

If the transform is defined in Item Properties, it is used as the default transform for all assets that don't have an overriding transform.

Note that `GetGeoTransform` and `rasterio` use different formats for reporting transform information. Order expected in `copernicus:transform` is the
same as reported by `rasterio`. When using GDAL method you need to re-order in the following way:

```python
g = GetGeoTransform(...)
proj_transform = [g[1], g[2], g[0],
                  g[4], g[5], g[3],
                     0,    0,    1]
```

### Centroid Object

This object represents the centroid of the Item Geometry.

| Field Name | Type   | Description                    |
| ---------- | ------ | ------------------------------ |
| lat        | number | The latitude of the centroid.  |
| lon        | number | The longitude of the centroid. |

### Best Practices

There are several projection extension fields with potentially overlapping functionality. This section attempts to
give an overview of which ones you should consider using. They fit into three general categories:

- **Description of the coordinate reference system:** [copernicus:code](#projcode) is recommended, but it is just a
  reference to known projection information.

  [WKT2](#projwkt2) and [PROJJSON](#projprojjson) are two options to
  fully describe the projection information.
  This is typically done for projections that aren't available or fully described in a known registry
  (e.g., [EPSG Registry](https://epsg.org/) or [IAU Registry](http://www.opengis.net/def/crs/IAU/2015)).
  For example, the MODIS Sinusoidal projection does not have an EPSG code, but can be described using WKT2 or PROJJSON.

- **Description of the native geometry information:** STAC requires the geometry and bounding box, but they are only available
  in lat/long (EPSG:4326, IAU_2015:30100, IAU_2015:49900, etc.). But most remote sensing data does not come in
  that projection, so it is often useful for clients to have
  the geometry information ([geometry](#projgeometry), [bbox](#projbbox), [centroid](#projcentroid)) in the coordinate reference system
  of the asset's data, so it doesn't have to reproject (which can be lossy and takes time).

- **Information to enable cataloging of data without opening assets:** Often it is useful to be able to construct a 'virtual layer',
  like GDAL's [VRT](https://gdal.org/drivers/raster/vrt.html) without having to open the actual imagery file. [shape](#projshape) and
  [transform](#projtransform) together with the core description of the CRS provide enough information about the size and shape of
  the data in the file so that tools don't have to open it.

  For example, the GDAL implementation requires the following fields:

  1. `copernicus:code` or `copernicus:wkt2` or `copernicus:projjson` (one of them filled with non-null values)
  2. Any of the following:
     - `copernicus:transform` and `copernicus:shape`
     - `copernicus:transform` and `copernicus:bbox`
     - `copernicus:bbox` and `copernicus:shape`

None of these are necessary for 'search' of data, the main use case of STAC. But all enable more 'cloud native' use of data, as they
describe the metadata needed to stream data for processing and/or display on the web. We do recommend including at least the code if it's
available, as it's a fairly standard piece of metadata, and [see below](#crs-description-recommendations) for more
information about when to use WKT and PROJJSON. We do recommend including the shape and transform fields if you have cloud
optimized geotiff's or some other cloud native format, to enable online tools to work with the assets more efficiently. This is
especially useful if the data is likely to be mosaiced or otherwise processed together, so that tools don't have to open every
single file to show or process aggregates of hundreds or thousands. Finally, the descriptions of the native geometry information
are useful when STAC is the complete metadata for an Item. If other metadata is also included it likely has this information, but
we provide it because some modern systems are just using STAC for their entire metadata description.

#### CRS Description Recommendations

WKT2 and PROJJSON are mostly recommended when you have data that is not part of a standard registry. Providing one of them
supplies the exact information for projection software to do the exact projection transform.
WKT2 and PROJJSON are equivalent to one another - more clients understand WKT2, but PROJJSON fits more nicely in the STAC JSON
structure, since they are both JSON. For now it's probably best to use both for maximum interoperability, but just using PROJJSON
is likely ok if you aren't worried about legacy client support.

#### Data in WGS 84

If the CRS is WGS 84 (e.g., `EPSG:4326`), `copernicus:bbox` and `copernicus:geometry` SHOULD be omitted in Items
as they would duplicate the `bbox` and `geometry` of the Item.
Clients that need these fields (e.g., to create a VRT in GDAL) SHOULD fall back to `bbox` and `geometry` in this case.

#### Thumbnails

For (unlocated) thumbnails and similar imagery, it is recommended set `copernicus:code` to `null` and include `copernicus:shape`
so that

1. clients can read the image dimensions upfront (and reserve space for them), and
2. you explicitly state that the thumbnail is not geolocated.

This is also recommended in case you have 'global' projection information in the Item properties.
The fields on the asset level override the Item Properties and as such client don't apply the 'global' projection details
falsely to the thumbnails.

Client implementations should be careful about the order in `copernicus:shape`.
Usually, image dimensions are given in width-height (x-y) order, but `copernicus:shape` lists the height first.

#### Links

Projection information in links is useful for resources that don't expose their CRS,
e.g., [web map links](https://github.com/stac-extensions/web-map-links).
For example, clients usually assume that XYZ tiles are in Web Mercator (`EPSG:3857`).
If they are in a different CRS, e.g., `EPSG:3031` for Antarctica, provide it in the link (e.g., via `copernicus:code`).

Projection information in Item Properties or Collections doesn't apply to links.

#### Bands

Projection information in bands is useful if the bands of an asset don't share the same grid,
e.g., a multi-resolution file with bands in 10, 20 and 60 meters (see the [Bands example](https://github.com/stac-extensions/projection/blob/main/examples/bands.json)).
Fields specified in a band override the corresponding fields in the asset for this band.
