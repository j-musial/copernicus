# Copernicus STAC Extension Specification

- **Title:** Copernicus
- **Identifier:** `https://j-musial.github.io/copernicus/v0.1.0/schema.json`
- **Field Name Prefix:** `copernicus`
- **Scope:** Catalog, Collection, Item, Asset, Link, Band
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal

This document defines the **Copernicus STAC Extension**, a single unified extension for
[Copernicus](https://www.copernicus.eu/en) programme data and services. It merges the field
vocabularies of **31 STAC extensions** under one namespace so that a single schema URI can be
used in `stac_extensions` to describe Copernicus collections, items, assets, links, and bands.

## Merged source extensions

This extension incorporates and supersedes the following upstream extensions for Copernicus
use. All fields have been renamed to use the single prefix `copernicus:`. See the
[mapping table](#field-mapping) for the original field names.

- [Alternate Assets](https://github.com/stac-extensions/alternate-assets)
- [Altimetry](https://github.com/stac-extensions/altimetry)
- [Authentication](https://github.com/stac-extensions/authentication)
- [Classification](https://github.com/stac-extensions/classification)
- [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf)
- [Contacts](https://github.com/stac-extensions/contacts)
- [Data Cube](https://github.com/stac-extensions/datacube)
- [EOPF](https://github.com/CS-SI/eopf-stac-extension)
- [Electro-Optical](https://github.com/stac-extensions/eo)
- [Embeddings](https://github.com/stac-extensions/embeddings)
- [Grid](https://github.com/stac-extensions/grid)
- [Order](https://github.com/stac-extensions/order)
- [Processing](https://github.com/stac-extensions/processing)
- [Product](https://github.com/stac-extensions/product)
- [Projection](https://github.com/stac-extensions/projection)
- [Raster](https://github.com/stac-extensions/raster)
- [Region](https://github.com/stac-extensions/region)
- [Render](https://github.com/stac-extensions/render)
- [Satellite](https://github.com/stac-extensions/sat)
- [Scientific Citation](https://github.com/stac-extensions/scientific)
- [Stats](https://github.com/stac-extensions/stats)
- [Storage](https://github.com/stac-extensions/storage)
- [Synthetic Aperture Radar](https://github.com/stac-extensions/sar)
- [Table](https://github.com/stac-extensions/table)
- [Themes](https://github.com/stac-extensions/themes)
- [Timestamps](https://github.com/stac-extensions/timestamps)
- [Vector](https://github.com/stac-extensions/vector)
- [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp)
- [View Geometry](https://github.com/stac-extensions/view)
- [Web Map Links](https://github.com/stac-extensions/web-map-links)
- [Xarray Assets](https://github.com/stac-extensions/xarray-assets)

## Fields

The fields in this extension can be used in these parts of STAC documents:

- Catalogs
- Collections (incl. Summaries)
- Item Properties
- Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- Links (incl. Link Templates)
- Bands

### Master table (alphabetical)

All `132` fields defined by this extension, sorted alphabetically.

| Field | Type | Applies To | Source Extension(s) | Description |
|-------|------|------------|---------------------|-------------|
| `copernicus:absolute_orbit` | integer | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The absolute orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the absolute orbit number at the start of the acquisition. |
| `copernicus:acquisition_station` | string | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The acquisition station (ground station) where the satellite data was downlinked. Equivalent to `eop:acquisition_station` in OGC 10-157r4 and OGC 17-003r2. |
| `copernicus:acquisition_type` | string (enum) | Collections, Item Properties, Assets | [Product](https://github.com/stac-extensions/product) | The acquisition type of the product. |
| `copernicus:alternate` | object | Assets | [Alternate Assets](https://github.com/stac-extensions/alternate-assets) | Alternate asset locations keyed by provider name, each an Asset Object without href. |
| `copernicus:alternate_name` | string | Assets | [Alternate Assets](https://github.com/stac-extensions/alternate-assets) | A human readable name for the alternate asset. |
| `copernicus:anx_datetime` | string | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The [Ascending Node](https://en.wikipedia.org/wiki/Orbital_node) Crossing (ANX) time, in UTC. It is formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `copernicus:auth_refs` | array of string | Catalogs, Collections, Item Properties, Assets, Links | [Authentication](https://github.com/stac-extensions/authentication) | The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link. |
| `copernicus:auth_schemes` | map of auth_scheme | Catalogs, Collections, Item Properties, Assets, Links | [Authentication](https://github.com/stac-extensions/authentication) | Dictionary of named authentication schemes that guard access to assets or links. |
| `copernicus:azimuth` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | Viewing azimuth angle. The angle measured from the sub-satellite point (point on the ground below the platform) between the scene center and true north. Measured clockwise from north in degrees (0-360). |
| `copernicus:bandwidth` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation. |
| `copernicus:bbox` | array of number | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | Bounding box of the Item in the asset CRS in 2 or 3 dimensions. |
| `copernicus:beam_ids` | array of string | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Composition of the swath of the SAR acquision referencing the beam identifiers. |
| `copernicus:bitfields` | [bit_field_object](#bit_field_object) | Item Properties, Assets, Bands | [Classification](https://github.com/stac-extensions/classification) | Classes stored in bit fields in the raster |
| `copernicus:bits_per_sample` | integer | Item Properties, Assets, Bands | [Raster](https://github.com/stac-extensions/raster) | The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the `datatype`, such as when a 1 bit TIFF is represented as byte. |
| `copernicus:cell_methods` | array of string/null | Collections, Item Properties, Assets, Bands, Data Cube Variables | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | null] |
| `copernicus:center_frequency` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz). |
| `copernicus:center_wavelength` | number | Item Properties, Assets, Bands | [Electro-Optical](https://github.com/stac-extensions/eo) | The center wavelength of the band, in micrometers (μm). |
| `copernicus:centroid` | object | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | Coordinates representing the centroid of the Item (in lat/long) |
| `copernicus:chip_size` | array of integer | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | Chip size in pixels as `[height, width]`. |
| `copernicus:citation` | string | Item Properties, Collections, Catalogs | [Scientific Citation](https://github.com/stac-extensions/scientific) | The recommended human-readable reference (citation) to be used by publications citing the data. No specific citation style is suggested, but the citation should contain all information required to find the publication distinctively. |
| `copernicus:classes` | [class_object](#class_object) | Item Properties, Assets, Bands | [Classification](https://github.com/stac-extensions/classification) | Classes stored in raster or bands |
| `copernicus:cloud_cover` | number | Item Properties, Assets, Bands | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of cloud cover as a percentage (0-100). |
| `copernicus:code` | string or null | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:columns` | array of object | Collections, Item Properties, Assets | [Table](https://github.com/stac-extensions/table) | A list of Column Objects describing each column. |
| `copernicus:common_name` | string (enum) | Item Properties, Assets, Bands | [Electro-Optical](https://github.com/stac-extensions/eo) | The name commonly used to refer to the band to make it easier to search for bands across instruments. See the [list of accepted common names](#common-band-names). |
| `copernicus:contacts` | array of object | Catalogs, Collections, Item Properties | [Contacts](https://github.com/stac-extensions/contacts) | **REQUIRED.** A list of contacts qualified by their role. |
| `copernicus:country` | string | Collections, Item Properties | [Region](https://github.com/stac-extensions/region) | ISO 3166-1 alpha-2 country code. Two-letter country code for the country that is primarily covered by the data. |
| `copernicus:datastrip_id` | string | Item Properties, Assets, Bands, Providers, Collections | [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Processing](https://github.com/stac-extensions/processing) | The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See [Datastrip ID](#datastrip-id) for details. |
| `copernicus:datatake_id` | string | Item Properties, Collections | [EOPF](https://github.com/CS-SI/eopf-stac-extension) | Datatake identification. Examples: for S1, datatake_id = 12032; for S2, datatake_id = GS2A_20231215T103431_044292_N05.10 |
| `copernicus:datetime` | string | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | Processing date and time of the corresponding data formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6), in UTC. |
| `copernicus:description` | string | Collections, Item Properties, Assets, Bands, Data Cube Variables | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `long_name`](https://cfconventions.org/cf-conventions/cf-conventions.html#long-name). |
| `copernicus:dimensions` | object | Collections, Item Properties | [Data Cube](https://github.com/stac-extensions/datacube) | **REQUIRED.** Uniquely named dimensions of the datacube. |
| `copernicus:doi` | string | Item Properties, Collections, Catalogs | [Scientific Citation](https://github.com/stac-extensions/scientific) | The DOI of the data, e.g. `10.1000/xyz123`. This MUST NOT be a DOIs link. For all DOI names respective DOI links SHOULD be added to the links section (see chapter "Relation types"). |
| `copernicus:embedding_dimensions` | array of integer | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding dimensions as an array of sizes, e.g. `[768]` for a single 768-dimensional vector. |
| `copernicus:embedding_type` | string (enum) | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding type: `pixel` or `chip`. |
| `copernicus:expires` | string | Catalogs, Collections, Item Properties, Assets, Links | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) expires (is not valid any longer), in UTC. |
| `copernicus:expression` | object | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type `processing-expression` (see below). |
| `copernicus:facility` | string | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | The name of the facility that produced the data. For example, `Copernicus S1 Core Ground Segment - DPA` for product of Sentinel-1 satellites. |
| `copernicus:frequency_band` | string (enum) | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names. |
| `copernicus:full_width_half_max` | number | Item Properties, Assets, Bands | [Electro-Optical](https://github.com/stac-extensions/eo) | Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm). |
| `copernicus:geometry` | Geometry.json | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | Defines the footprint of this Item. |
| `copernicus:geometry_types` | array of string | Collections, Item Properties, Assets, Table Columns | [Vector](https://github.com/stac-extensions/vector) | A list of the geometry types present in the dataset. |
| `copernicus:grid_code` | string | Item Properties | [Grid](https://github.com/stac-extensions/grid) | **REQUIRED**. The identifier for the grid element associated with the Item. |
| `copernicus:grid_id` | string | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | Grid system the chips are aligned to. See [Grid IDs](#grid-ids). |
| `copernicus:histogram` | object | Item Properties, Assets, Bands | [Raster](https://github.com/stac-extensions/raster) | Histogram distribution information of the pixels values in the band. |
| `copernicus:incidence_angle` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | The incidence angle is the angle between the vertical (normal) to the intercepting surface and the line of sight back to the satellite at the scene center. Measured in degrees (0-90). |
| `copernicus:instrument_configuration_id` | integer | Item Properties, Collections | [EOPF](https://github.com/CS-SI/eopf-stac-extension) | The instrument configuration ID is specific to S1 SAR instrument and refers to the onboard configuration. Each version of it has a specific identifier called "Instrument Configuration ID" (ICID) corresponding to a specific number. For more information, cf. ["What is the instrument configuration ID (ICID) ?"](https://sar-mpc.eu/about/faq/) |
| `copernicus:instrument_mode` | string | Item Properties, Collections, Assets | [Altimetry](https://github.com/stac-extensions/altimetry), [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Mode of the altimetry instrument used to collect the data. |
| `copernicus:instrument_type` | string (enum) | Item Properties | [Altimetry](https://github.com/stac-extensions/altimetry) | Type of altimetry instrument used to collect the data. |
| `copernicus:level` | string | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only `L`, not `Level`). See the [list of suggested processing levels](#suggested-processing-levels). |
| `copernicus:lineage` | string | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described [NASA ISO](https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information). For example, `GRD Post Processing` for "GRD" product of Sentinel-1 satellites. [CommonMark 0.29](https://commonmark.org/) syntax MAY be used for rich text representation. |
| `copernicus:looks_azimuth` | integer | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path. |
| `copernicus:looks_equivalent_number` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The equivalent number of looks (ENL). |
| `copernicus:looks_range` | integer | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path. |
| `copernicus:mmu` | number | Collections, Item Properties, Assets, Table Columns | [Vector](https://github.com/stac-extensions/vector) | Minimum Mapping Unit - the smallest polygon area represented. |
| `copernicus:mmw` | number | Collections, Item Properties, Assets, Table Columns | [Vector](https://github.com/stac-extensions/vector) | Minimal Mapping Width - the smallest real-world width represented as polygon. |
| `copernicus:moon_azimuth` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | Moon azimuth angle. From the scene center point on the ground, this is the angle between truth north and the moon. Measured clockwise in degrees (0-360). |
| `copernicus:moon_elevation` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | Moon elevation angle. The angle from the tangent of the scene center point to the moon. Measured from the horizon in degrees (`0`-`90`). |
| `copernicus:name` | string | Collections, Item Properties | [Region](https://github.com/stac-extensions/region) | A human-readable name of the relevant region. |
| `copernicus:nominal_track` | coordinates | Item Properties | [Altimetry](https://github.com/stac-extensions/altimetry) | An array of coordinates used to define the nominal track on the earths surface. This value is recommended ONLY if the item geometry is not representative of the acquisition track. |
| `copernicus:observation_direction` | string (enum) | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Antenna pointing direction relative to the flight trajectory of the satellite, either `left` or `right`. |
| `copernicus:off_nadir` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | The angle from the sensor between nadir (straight down) and the scene center. Measured in degrees (0-90). |
| `copernicus:offset` | number | Item Properties, Assets, Bands | [Raster](https://github.com/stac-extensions/raster) | Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:open_kwargs` | object | Assets | [Xarray Assets](https://github.com/stac-extensions/xarray-assets) | Keyword arguments to provide to the xarray opener |
| `copernicus:orbit_cycle` | integer | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The number of repeat cycle done by the satellite at the time of the acquisition. [Repeat cycle](https://ltb.itc.utwente.nl/page/498/concept/81577) is the time between two successive identical orbits. |
| `copernicus:orbit_state` | string (enum) | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The state of the orbit. Either `ascending` or `descending` for polar orbiting satellites, `geostationary` for geosynchronous satellites, or `crossing` when the acquisition spans a polar crossing. |
| `copernicus:orbit_state_vectors` | map of array | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The state vectors of the satellite at the time of acquisition. |
| `copernicus:order_date` | string | Collections, Item Properties, Assets | [Order](https://github.com/stac-extensions/order) | Indicates the order submission time, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `copernicus:order_expiration_date` | string | Collections, Item Properties, Assets | [Order](https://github.com/stac-extensions/order) | **DEPRECATED.** Indicates the validity time of the order, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Use [`expires` from the timestamps extension](https://github.com/stac-extensions/timestamps/) instead. |
| `copernicus:order_id` | string | Collections, Item Properties, Assets | [Order](https://github.com/stac-extensions/order) | Identifier of the order. |
| `copernicus:order_status` | string (enum) | Collections, Item Properties, Assets | [Order](https://github.com/stac-extensions/order) | **REQUIRED**. Describe the status of the ordering. One of the value listed [here](#orderstatus) |
| `copernicus:origin_datetime` | string | Item Properties, Collections | [EOPF](https://github.com/CS-SI/eopf-stac-extension) | Date time of the input data considered to create the item. Example: for PRIP, time of the availability of all CADU data on the CADIP/XBIP |
| `copernicus:original_data_type` | string (enum) | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | Data type before quantization. Uses the same [data type values](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types) as `data_type`. |
| `copernicus:pixel_spacing_azimuth` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| `copernicus:pixel_spacing_range` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| `copernicus:platform_international_designator` | string | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The International Designator, also known as COSPAR ID, and NSSDCA ID |
| `copernicus:pmtiles_layers` | array of string | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The PMTiles layers to display. |
| `copernicus:polarizations` | array of string | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. Any combination of polarizations. |
| `copernicus:primary_datetime` | string | Collections, Item Properties, Assets | [Table](https://github.com/stac-extensions/table) | The primary date/time column name. |
| `copernicus:primary_geometry` | string | Collections, Item Properties, Assets | [Table](https://github.com/stac-extensions/table) | The primary geometry column name. |
| `copernicus:product_status` | string (enum) | Collections, Item Properties, Assets | [Product](https://github.com/stac-extensions/product) | The lifecycle/status of the product. |
| `copernicus:product_type` | string | Collections, Item Properties, Assets | [Product](https://github.com/stac-extensions/product), [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The product type. |
| `copernicus:projjson` | any | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:publications` | array of object | Item Properties, Collections, Catalogs | [Scientific Citation](https://github.com/stac-extensions/scientific) | List of relevant publications referencing and describing the data. |
| `copernicus:published` | string | Catalogs, Collections, Item Properties, Assets, Links | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was published the first time, in UTC. |
| `copernicus:quality_status` | string (enum) | Collections, Item Properties, Assets | [Product](https://github.com/stac-extensions/product) | The quality status of the product: `nominal` or `degraded`. |
| `copernicus:quantization_method` | string | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | Quantization method (e.g. `linear`). |
| `copernicus:reference_scale` | integer | Collections, Item Properties, Assets, Table Columns | [Vector](https://github.com/stac-extensions/vector) | Representative fraction denominator (e.g., 50000 for 1:50,000). |
| `copernicus:relative_burst` | integer | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Identification number that uniquely identifies a burst cycle within each repeat cycle. |
| `copernicus:relative_orbit` | integer | Item Properties, Collections | [Satellite](https://github.com/stac-extensions/sat) | The relative orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the relative orbit number at the start of the acquisition. |
| `copernicus:renders` | object | Collections, Item Properties | [Render](https://github.com/stac-extensions/render) | Dictionary of rendering instructions that can be viewed, keyed by a unique render name. |
| `copernicus:resolution_azimuth` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m). |
| `copernicus:resolution_range` | number | Collections, Item Properties, Assets | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m). |
| `copernicus:row_count` | number | Collections, Item Properties, Assets | [Table](https://github.com/stac-extensions/table) | The number of rows in the dataset. |
| `copernicus:sampling` | string (enum) | Item Properties, Assets, Bands | [Raster](https://github.com/stac-extensions/raster) | One of `area` or `point`. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel. |
| `copernicus:sampling_rate` | number | Item Properties | [Altimetry](https://github.com/stac-extensions/altimetry) | Sampling rate of the altimetry instrument in Hz. |
| `copernicus:scale` | number | Item Properties, Assets, Bands | [Raster](https://github.com/stac-extensions/raster) | Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:season` | string (enum) | Collections, Item Properties, Assets, Bands | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP season number. One of `S1` or `S2`. See below for details. |
| `copernicus:servers` | array of string | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The servers to substitute for the {s} variable in the link href. |
| `copernicus:shape` | array of integer | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | Number of pixels in Y and X directions for the default grid |
| `copernicus:snow_cover` | number | Item Properties, Assets, Bands | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of snow and ice cover as a percentage (0-100). |
| `copernicus:software` | map of string | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes. |
| `copernicus:solar_illumination` | number | Item Properties, Assets, Bands | [Electro-Optical](https://github.com/stac-extensions/eo) | The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers. |
| `copernicus:spatial_resolution` | number | Item Properties, Assets, Bands | [Raster](https://github.com/stac-extensions/raster) | Average spatial resolution (in meters) of the pixels in the band. |
| `copernicus:standard_name` | string | Collections, Item Properties, Assets, Bands, Data Cube Variables | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF Standard Name](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html). |
| `copernicus:stats_catalogs` | object | Collections, Catalogs | [Stats](https://github.com/stac-extensions/stats) | A lookup of statistics for all child catalogs. |
| `copernicus:stats_collections` | object | Collections, Catalogs | [Stats](https://github.com/stac-extensions/stats) | A lookup of statistics for all child collections. |
| `copernicus:stats_items` | object | Collections, Catalogs | [Stats](https://github.com/stac-extensions/stats) | A lookup of statistics for all child items. |
| `copernicus:storage_options` | object | Collections, Item Properties, Assets | [Table](https://github.com/stac-extensions/table), [Xarray Assets](https://github.com/stac-extensions/xarray-assets) | **DEPRECATED** Additional keywords for opening the dataset. |
| `copernicus:stride` | array of integer | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | Step between the origins of neighboring chips in pixels as `[row_stride, col_stride]`. When `stride < chip_size`, chips overlap. |
| `copernicus:sub_parameter` | string (enum) | Collections, Item Properties, Assets, Bands | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP sub-parameter acronym. See below for the list of allowed values. |
| `copernicus:subdivision` | string | Collections, Item Properties | [Region](https://github.com/stac-extensions/region) | ISO 3166-2 codes for identifying the principal subdivisions (e.g., provinces or states) of a country that is primarily covered by the data. Only provide the second part of the ISO 3166-2 code to reduce redundancy. |
| `copernicus:sun_azimuth` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | Sun azimuth angle. From the scene center point on the ground, this is the angle between truth north and the sun. Measured clockwise in degrees (0-360). |
| `copernicus:sun_elevation` | number | Item Properties, Assets | [View Geometry](https://github.com/stac-extensions/view) | Sun elevation angle. The angle from the tangent of the scene center point to the sun. Measured from the horizon in degrees (`-90`-`90`). Negative values indicate the sun is below the horizon, e.g. sun elevation of -10° means the data was captured during [nautical twilight](https://www.timeanddate.com/astronomy/different-types-twilight.html). |
| `copernicus:tables` | array of object | Collections, Item Properties, Assets | [Table](https://github.com/stac-extensions/table) | **DEPRECATED** A list of Table Objects (see below). |
| `copernicus:temporal_period` | string | Collections, Item Properties, Assets, Bands | [Embeddings](https://github.com/stac-extensions/embeddings) | Temporal compositing period as an [ISO 8601 duration](https://en.wikipedia.org/wiki/ISO_8601#Durations) (e.g. `P1Y`, `P3M`). |
| `copernicus:themes` | array of object | Catalogs, Collections, Item Properties | [Themes](https://github.com/stac-extensions/themes) | **REQUIRED.** A knowledge organization system used to classify the STAC entity. Each element is a concept and their respective knowledge organization system / controlled vocabulary. |
| `copernicus:timeliness` | string | Collections, Item Properties, Assets | [Product](https://github.com/stac-extensions/product) | The average expected timeliness of the product as an [ISO 8601 Duration](https://en.wikipedia.org/wiki/ISO_8601#Durations). |
| `copernicus:timeliness_category` | string | Collections, Item Properties, Assets | [Product](https://github.com/stac-extensions/product) | A proprietary category identifier for the timeliness of the product. |
| `copernicus:transform` | array of number | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | The affine transformation coefficients for the default grid |
| `copernicus:unit` | string | Collections, Item Properties, Assets, Bands, Data Cube Variables | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `units`](https://cfconventions.org/cf-conventions/cf-conventions.html#units). |
| `copernicus:unpublished` | string | Catalogs, Collections, Item Properties, Assets, Links | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was unpublished, in UTC. |
| `copernicus:variables` | object | Collections, Item Properties | [Data Cube](https://github.com/stac-extensions/datacube) | Uniquely named variables of the datacube. |
| `copernicus:version` | string | Item Properties, Assets, Bands, Providers | [Processing](https://github.com/stac-extensions/processing) | The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions. |
| `copernicus:wkt2` | string or null | Collections, Item Properties, Assets, Links, Bands | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:wms_dimensions` | object | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | WMS dimensions and their values. |
| `copernicus:wms_layers` | array of string | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The WMS layers to display. |
| `copernicus:wms_styles` | array of string | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The WMS styles to apply. |
| `copernicus:wms_transparent` | boolean | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | Whether the WMS map background is transparent. |
| `copernicus:wmts_dimensions` | object | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | WMTS dimensions and their values. |
| `copernicus:wmts_encoding` | string (enum) | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The encoding to use for WMTS requests: `rest` or `kvp`. |
| `copernicus:wmts_layer` | string | Links | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The WMTS layer identifier. |

### Item Properties fields

Fields usable in Item Properties (and Collection Summaries).

| Field | Type | Source Extension(s) | Description |
|-------|------|----------------------|-------------|
| `copernicus:absolute_orbit` | integer | [Satellite](https://github.com/stac-extensions/sat) | The absolute orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the absolute orbit number at the start of the acquisition. |
| `copernicus:acquisition_station` | string | [Satellite](https://github.com/stac-extensions/sat) | The acquisition station (ground station) where the satellite data was downlinked. Equivalent to `eop:acquisition_station` in OGC 10-157r4 and OGC 17-003r2. |
| `copernicus:acquisition_type` | string (enum) | [Product](https://github.com/stac-extensions/product) | The acquisition type of the product. |
| `copernicus:anx_datetime` | string | [Satellite](https://github.com/stac-extensions/sat) | The [Ascending Node](https://en.wikipedia.org/wiki/Orbital_node) Crossing (ANX) time, in UTC. It is formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `copernicus:auth_refs` | array of string | [Authentication](https://github.com/stac-extensions/authentication) | The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link. |
| `copernicus:auth_schemes` | map of auth_scheme | [Authentication](https://github.com/stac-extensions/authentication) | Dictionary of named authentication schemes that guard access to assets or links. |
| `copernicus:azimuth` | number | [View Geometry](https://github.com/stac-extensions/view) | Viewing azimuth angle. The angle measured from the sub-satellite point (point on the ground below the platform) between the scene center and true north. Measured clockwise from north in degrees (0-360). |
| `copernicus:bandwidth` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation. |
| `copernicus:bbox` | array of number | [Projection](https://github.com/stac-extensions/projection) | Bounding box of the Item in the asset CRS in 2 or 3 dimensions. |
| `copernicus:beam_ids` | array of string | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Composition of the swath of the SAR acquision referencing the beam identifiers. |
| `copernicus:bitfields` | [bit_field_object](#bit_field_object) | [Classification](https://github.com/stac-extensions/classification) | Classes stored in bit fields in the raster |
| `copernicus:bits_per_sample` | integer | [Raster](https://github.com/stac-extensions/raster) | The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the `datatype`, such as when a 1 bit TIFF is represented as byte. |
| `copernicus:cell_methods` | array of string/null | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | null] |
| `copernicus:center_frequency` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz). |
| `copernicus:center_wavelength` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | The center wavelength of the band, in micrometers (μm). |
| `copernicus:centroid` | object | [Projection](https://github.com/stac-extensions/projection) | Coordinates representing the centroid of the Item (in lat/long) |
| `copernicus:chip_size` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | Chip size in pixels as `[height, width]`. |
| `copernicus:citation` | string | [Scientific Citation](https://github.com/stac-extensions/scientific) | The recommended human-readable reference (citation) to be used by publications citing the data. No specific citation style is suggested, but the citation should contain all information required to find the publication distinctively. |
| `copernicus:classes` | [class_object](#class_object) | [Classification](https://github.com/stac-extensions/classification) | Classes stored in raster or bands |
| `copernicus:cloud_cover` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of cloud cover as a percentage (0-100). |
| `copernicus:code` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:columns` | array of object | [Table](https://github.com/stac-extensions/table) | A list of Column Objects describing each column. |
| `copernicus:common_name` | string (enum) | [Electro-Optical](https://github.com/stac-extensions/eo) | The name commonly used to refer to the band to make it easier to search for bands across instruments. See the [list of accepted common names](#common-band-names). |
| `copernicus:contacts` | array of object | [Contacts](https://github.com/stac-extensions/contacts) | **REQUIRED.** A list of contacts qualified by their role. |
| `copernicus:country` | string | [Region](https://github.com/stac-extensions/region) | ISO 3166-1 alpha-2 country code. Two-letter country code for the country that is primarily covered by the data. |
| `copernicus:datastrip_id` | string | [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Processing](https://github.com/stac-extensions/processing) | The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See [Datastrip ID](#datastrip-id) for details. |
| `copernicus:datatake_id` | string | [EOPF](https://github.com/CS-SI/eopf-stac-extension) | Datatake identification. Examples: for S1, datatake_id = 12032; for S2, datatake_id = GS2A_20231215T103431_044292_N05.10 |
| `copernicus:datetime` | string | [Processing](https://github.com/stac-extensions/processing) | Processing date and time of the corresponding data formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6), in UTC. |
| `copernicus:description` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `long_name`](https://cfconventions.org/cf-conventions/cf-conventions.html#long-name). |
| `copernicus:dimensions` | object | [Data Cube](https://github.com/stac-extensions/datacube) | **REQUIRED.** Uniquely named dimensions of the datacube. |
| `copernicus:doi` | string | [Scientific Citation](https://github.com/stac-extensions/scientific) | The DOI of the data, e.g. `10.1000/xyz123`. This MUST NOT be a DOIs link. For all DOI names respective DOI links SHOULD be added to the links section (see chapter "Relation types"). |
| `copernicus:embedding_dimensions` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding dimensions as an array of sizes, e.g. `[768]` for a single 768-dimensional vector. |
| `copernicus:embedding_type` | string (enum) | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding type: `pixel` or `chip`. |
| `copernicus:expires` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) expires (is not valid any longer), in UTC. |
| `copernicus:expression` | object | [Processing](https://github.com/stac-extensions/processing) | An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type `processing-expression` (see below). |
| `copernicus:facility` | string | [Processing](https://github.com/stac-extensions/processing) | The name of the facility that produced the data. For example, `Copernicus S1 Core Ground Segment - DPA` for product of Sentinel-1 satellites. |
| `copernicus:frequency_band` | string (enum) | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names. |
| `copernicus:full_width_half_max` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm). |
| `copernicus:geometry` | Geometry.json | [Projection](https://github.com/stac-extensions/projection) | Defines the footprint of this Item. |
| `copernicus:geometry_types` | array of string | [Vector](https://github.com/stac-extensions/vector) | A list of the geometry types present in the dataset. |
| `copernicus:grid_code` | string | [Grid](https://github.com/stac-extensions/grid) | **REQUIRED**. The identifier for the grid element associated with the Item. |
| `copernicus:grid_id` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Grid system the chips are aligned to. See [Grid IDs](#grid-ids). |
| `copernicus:histogram` | object | [Raster](https://github.com/stac-extensions/raster) | Histogram distribution information of the pixels values in the band. |
| `copernicus:incidence_angle` | number | [View Geometry](https://github.com/stac-extensions/view) | The incidence angle is the angle between the vertical (normal) to the intercepting surface and the line of sight back to the satellite at the scene center. Measured in degrees (0-90). |
| `copernicus:instrument_configuration_id` | integer | [EOPF](https://github.com/CS-SI/eopf-stac-extension) | The instrument configuration ID is specific to S1 SAR instrument and refers to the onboard configuration. Each version of it has a specific identifier called "Instrument Configuration ID" (ICID) corresponding to a specific number. For more information, cf. ["What is the instrument configuration ID (ICID) ?"](https://sar-mpc.eu/about/faq/) |
| `copernicus:instrument_mode` | string | [Altimetry](https://github.com/stac-extensions/altimetry), [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Mode of the altimetry instrument used to collect the data. |
| `copernicus:instrument_type` | string (enum) | [Altimetry](https://github.com/stac-extensions/altimetry) | Type of altimetry instrument used to collect the data. |
| `copernicus:level` | string | [Processing](https://github.com/stac-extensions/processing) | The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only `L`, not `Level`). See the [list of suggested processing levels](#suggested-processing-levels). |
| `copernicus:lineage` | string | [Processing](https://github.com/stac-extensions/processing) | Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described [NASA ISO](https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information). For example, `GRD Post Processing` for "GRD" product of Sentinel-1 satellites. [CommonMark 0.29](https://commonmark.org/) syntax MAY be used for rich text representation. |
| `copernicus:looks_azimuth` | integer | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path. |
| `copernicus:looks_equivalent_number` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The equivalent number of looks (ENL). |
| `copernicus:looks_range` | integer | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path. |
| `copernicus:mmu` | number | [Vector](https://github.com/stac-extensions/vector) | Minimum Mapping Unit - the smallest polygon area represented. |
| `copernicus:mmw` | number | [Vector](https://github.com/stac-extensions/vector) | Minimal Mapping Width - the smallest real-world width represented as polygon. |
| `copernicus:moon_azimuth` | number | [View Geometry](https://github.com/stac-extensions/view) | Moon azimuth angle. From the scene center point on the ground, this is the angle between truth north and the moon. Measured clockwise in degrees (0-360). |
| `copernicus:moon_elevation` | number | [View Geometry](https://github.com/stac-extensions/view) | Moon elevation angle. The angle from the tangent of the scene center point to the moon. Measured from the horizon in degrees (`0`-`90`). |
| `copernicus:name` | string | [Region](https://github.com/stac-extensions/region) | A human-readable name of the relevant region. |
| `copernicus:nominal_track` | coordinates | [Altimetry](https://github.com/stac-extensions/altimetry) | An array of coordinates used to define the nominal track on the earths surface. This value is recommended ONLY if the item geometry is not representative of the acquisition track. |
| `copernicus:observation_direction` | string (enum) | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Antenna pointing direction relative to the flight trajectory of the satellite, either `left` or `right`. |
| `copernicus:off_nadir` | number | [View Geometry](https://github.com/stac-extensions/view) | The angle from the sensor between nadir (straight down) and the scene center. Measured in degrees (0-90). |
| `copernicus:offset` | number | [Raster](https://github.com/stac-extensions/raster) | Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:orbit_cycle` | integer | [Satellite](https://github.com/stac-extensions/sat) | The number of repeat cycle done by the satellite at the time of the acquisition. [Repeat cycle](https://ltb.itc.utwente.nl/page/498/concept/81577) is the time between two successive identical orbits. |
| `copernicus:orbit_state` | string (enum) | [Satellite](https://github.com/stac-extensions/sat) | The state of the orbit. Either `ascending` or `descending` for polar orbiting satellites, `geostationary` for geosynchronous satellites, or `crossing` when the acquisition spans a polar crossing. |
| `copernicus:orbit_state_vectors` | map of array | [Satellite](https://github.com/stac-extensions/sat) | The state vectors of the satellite at the time of acquisition. |
| `copernicus:order_date` | string | [Order](https://github.com/stac-extensions/order) | Indicates the order submission time, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `copernicus:order_expiration_date` | string | [Order](https://github.com/stac-extensions/order) | **DEPRECATED.** Indicates the validity time of the order, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Use [`expires` from the timestamps extension](https://github.com/stac-extensions/timestamps/) instead. |
| `copernicus:order_id` | string | [Order](https://github.com/stac-extensions/order) | Identifier of the order. |
| `copernicus:order_status` | string (enum) | [Order](https://github.com/stac-extensions/order) | **REQUIRED**. Describe the status of the ordering. One of the value listed [here](#orderstatus) |
| `copernicus:origin_datetime` | string | [EOPF](https://github.com/CS-SI/eopf-stac-extension) | Date time of the input data considered to create the item. Example: for PRIP, time of the availability of all CADU data on the CADIP/XBIP |
| `copernicus:original_data_type` | string (enum) | [Embeddings](https://github.com/stac-extensions/embeddings) | Data type before quantization. Uses the same [data type values](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types) as `data_type`. |
| `copernicus:pixel_spacing_azimuth` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| `copernicus:pixel_spacing_range` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| `copernicus:platform_international_designator` | string | [Satellite](https://github.com/stac-extensions/sat) | The International Designator, also known as COSPAR ID, and NSSDCA ID |
| `copernicus:polarizations` | array of string | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. Any combination of polarizations. |
| `copernicus:primary_datetime` | string | [Table](https://github.com/stac-extensions/table) | The primary date/time column name. |
| `copernicus:primary_geometry` | string | [Table](https://github.com/stac-extensions/table) | The primary geometry column name. |
| `copernicus:product_status` | string (enum) | [Product](https://github.com/stac-extensions/product) | The lifecycle/status of the product. |
| `copernicus:product_type` | string | [Product](https://github.com/stac-extensions/product), [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The product type. |
| `copernicus:projjson` | any | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:publications` | array of object | [Scientific Citation](https://github.com/stac-extensions/scientific) | List of relevant publications referencing and describing the data. |
| `copernicus:published` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was published the first time, in UTC. |
| `copernicus:quality_status` | string (enum) | [Product](https://github.com/stac-extensions/product) | The quality status of the product: `nominal` or `degraded`. |
| `copernicus:quantization_method` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Quantization method (e.g. `linear`). |
| `copernicus:reference_scale` | integer | [Vector](https://github.com/stac-extensions/vector) | Representative fraction denominator (e.g., 50000 for 1:50,000). |
| `copernicus:relative_burst` | integer | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Identification number that uniquely identifies a burst cycle within each repeat cycle. |
| `copernicus:relative_orbit` | integer | [Satellite](https://github.com/stac-extensions/sat) | The relative orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the relative orbit number at the start of the acquisition. |
| `copernicus:renders` | object | [Render](https://github.com/stac-extensions/render) | Dictionary of rendering instructions that can be viewed, keyed by a unique render name. |
| `copernicus:resolution_azimuth` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m). |
| `copernicus:resolution_range` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m). |
| `copernicus:row_count` | number | [Table](https://github.com/stac-extensions/table) | The number of rows in the dataset. |
| `copernicus:sampling` | string (enum) | [Raster](https://github.com/stac-extensions/raster) | One of `area` or `point`. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel. |
| `copernicus:sampling_rate` | number | [Altimetry](https://github.com/stac-extensions/altimetry) | Sampling rate of the altimetry instrument in Hz. |
| `copernicus:scale` | number | [Raster](https://github.com/stac-extensions/raster) | Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:season` | string (enum) | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP season number. One of `S1` or `S2`. See below for details. |
| `copernicus:shape` | array of integer | [Projection](https://github.com/stac-extensions/projection) | Number of pixels in Y and X directions for the default grid |
| `copernicus:snow_cover` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of snow and ice cover as a percentage (0-100). |
| `copernicus:software` | map of string | [Processing](https://github.com/stac-extensions/processing) | A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes. |
| `copernicus:solar_illumination` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers. |
| `copernicus:spatial_resolution` | number | [Raster](https://github.com/stac-extensions/raster) | Average spatial resolution (in meters) of the pixels in the band. |
| `copernicus:standard_name` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF Standard Name](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html). |
| `copernicus:storage_options` | object | [Table](https://github.com/stac-extensions/table), [Xarray Assets](https://github.com/stac-extensions/xarray-assets) | **DEPRECATED** Additional keywords for opening the dataset. |
| `copernicus:stride` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | Step between the origins of neighboring chips in pixels as `[row_stride, col_stride]`. When `stride < chip_size`, chips overlap. |
| `copernicus:sub_parameter` | string (enum) | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP sub-parameter acronym. See below for the list of allowed values. |
| `copernicus:subdivision` | string | [Region](https://github.com/stac-extensions/region) | ISO 3166-2 codes for identifying the principal subdivisions (e.g., provinces or states) of a country that is primarily covered by the data. Only provide the second part of the ISO 3166-2 code to reduce redundancy. |
| `copernicus:sun_azimuth` | number | [View Geometry](https://github.com/stac-extensions/view) | Sun azimuth angle. From the scene center point on the ground, this is the angle between truth north and the sun. Measured clockwise in degrees (0-360). |
| `copernicus:sun_elevation` | number | [View Geometry](https://github.com/stac-extensions/view) | Sun elevation angle. The angle from the tangent of the scene center point to the sun. Measured from the horizon in degrees (`-90`-`90`). Negative values indicate the sun is below the horizon, e.g. sun elevation of -10° means the data was captured during [nautical twilight](https://www.timeanddate.com/astronomy/different-types-twilight.html). |
| `copernicus:tables` | array of object | [Table](https://github.com/stac-extensions/table) | **DEPRECATED** A list of Table Objects (see below). |
| `copernicus:temporal_period` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Temporal compositing period as an [ISO 8601 duration](https://en.wikipedia.org/wiki/ISO_8601#Durations) (e.g. `P1Y`, `P3M`). |
| `copernicus:themes` | array of object | [Themes](https://github.com/stac-extensions/themes) | **REQUIRED.** A knowledge organization system used to classify the STAC entity. Each element is a concept and their respective knowledge organization system / controlled vocabulary. |
| `copernicus:timeliness` | string | [Product](https://github.com/stac-extensions/product) | The average expected timeliness of the product as an [ISO 8601 Duration](https://en.wikipedia.org/wiki/ISO_8601#Durations). |
| `copernicus:timeliness_category` | string | [Product](https://github.com/stac-extensions/product) | A proprietary category identifier for the timeliness of the product. |
| `copernicus:transform` | array of number | [Projection](https://github.com/stac-extensions/projection) | The affine transformation coefficients for the default grid |
| `copernicus:unit` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `units`](https://cfconventions.org/cf-conventions/cf-conventions.html#units). |
| `copernicus:unpublished` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was unpublished, in UTC. |
| `copernicus:variables` | object | [Data Cube](https://github.com/stac-extensions/datacube) | Uniquely named variables of the datacube. |
| `copernicus:version` | string | [Processing](https://github.com/stac-extensions/processing) | The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions. |
| `copernicus:wkt2` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |

### Asset fields

Fields usable in Assets and Item Asset Definitions.

| Field | Type | Source Extension(s) | Description |
|-------|------|----------------------|-------------|
| `copernicus:acquisition_type` | string (enum) | [Product](https://github.com/stac-extensions/product) | The acquisition type of the product. |
| `copernicus:alternate` | object | [Alternate Assets](https://github.com/stac-extensions/alternate-assets) | Alternate asset locations keyed by provider name, each an Asset Object without href. |
| `copernicus:alternate_name` | string | [Alternate Assets](https://github.com/stac-extensions/alternate-assets) | A human readable name for the alternate asset. |
| `copernicus:auth_refs` | array of string | [Authentication](https://github.com/stac-extensions/authentication) | The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link. |
| `copernicus:auth_schemes` | map of auth_scheme | [Authentication](https://github.com/stac-extensions/authentication) | Dictionary of named authentication schemes that guard access to assets or links. |
| `copernicus:azimuth` | number | [View Geometry](https://github.com/stac-extensions/view) | Viewing azimuth angle. The angle measured from the sub-satellite point (point on the ground below the platform) between the scene center and true north. Measured clockwise from north in degrees (0-360). |
| `copernicus:bandwidth` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation. |
| `copernicus:bbox` | array of number | [Projection](https://github.com/stac-extensions/projection) | Bounding box of the Item in the asset CRS in 2 or 3 dimensions. |
| `copernicus:beam_ids` | array of string | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Composition of the swath of the SAR acquision referencing the beam identifiers. |
| `copernicus:bitfields` | [bit_field_object](#bit_field_object) | [Classification](https://github.com/stac-extensions/classification) | Classes stored in bit fields in the raster |
| `copernicus:bits_per_sample` | integer | [Raster](https://github.com/stac-extensions/raster) | The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the `datatype`, such as when a 1 bit TIFF is represented as byte. |
| `copernicus:cell_methods` | array of string/null | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | null] |
| `copernicus:center_frequency` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz). |
| `copernicus:center_wavelength` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | The center wavelength of the band, in micrometers (μm). |
| `copernicus:centroid` | object | [Projection](https://github.com/stac-extensions/projection) | Coordinates representing the centroid of the Item (in lat/long) |
| `copernicus:chip_size` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | Chip size in pixels as `[height, width]`. |
| `copernicus:classes` | [class_object](#class_object) | [Classification](https://github.com/stac-extensions/classification) | Classes stored in raster or bands |
| `copernicus:cloud_cover` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of cloud cover as a percentage (0-100). |
| `copernicus:code` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:columns` | array of object | [Table](https://github.com/stac-extensions/table) | A list of Column Objects describing each column. |
| `copernicus:common_name` | string (enum) | [Electro-Optical](https://github.com/stac-extensions/eo) | The name commonly used to refer to the band to make it easier to search for bands across instruments. See the [list of accepted common names](#common-band-names). |
| `copernicus:datastrip_id` | string | [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Processing](https://github.com/stac-extensions/processing) | The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See [Datastrip ID](#datastrip-id) for details. |
| `copernicus:datetime` | string | [Processing](https://github.com/stac-extensions/processing) | Processing date and time of the corresponding data formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6), in UTC. |
| `copernicus:description` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `long_name`](https://cfconventions.org/cf-conventions/cf-conventions.html#long-name). |
| `copernicus:embedding_dimensions` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding dimensions as an array of sizes, e.g. `[768]` for a single 768-dimensional vector. |
| `copernicus:embedding_type` | string (enum) | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding type: `pixel` or `chip`. |
| `copernicus:expires` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) expires (is not valid any longer), in UTC. |
| `copernicus:expression` | object | [Processing](https://github.com/stac-extensions/processing) | An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type `processing-expression` (see below). |
| `copernicus:facility` | string | [Processing](https://github.com/stac-extensions/processing) | The name of the facility that produced the data. For example, `Copernicus S1 Core Ground Segment - DPA` for product of Sentinel-1 satellites. |
| `copernicus:frequency_band` | string (enum) | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names. |
| `copernicus:full_width_half_max` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm). |
| `copernicus:geometry` | Geometry.json | [Projection](https://github.com/stac-extensions/projection) | Defines the footprint of this Item. |
| `copernicus:geometry_types` | array of string | [Vector](https://github.com/stac-extensions/vector) | A list of the geometry types present in the dataset. |
| `copernicus:grid_id` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Grid system the chips are aligned to. See [Grid IDs](#grid-ids). |
| `copernicus:histogram` | object | [Raster](https://github.com/stac-extensions/raster) | Histogram distribution information of the pixels values in the band. |
| `copernicus:incidence_angle` | number | [View Geometry](https://github.com/stac-extensions/view) | The incidence angle is the angle between the vertical (normal) to the intercepting surface and the line of sight back to the satellite at the scene center. Measured in degrees (0-90). |
| `copernicus:instrument_mode` | string | [Altimetry](https://github.com/stac-extensions/altimetry), [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Mode of the altimetry instrument used to collect the data. |
| `copernicus:level` | string | [Processing](https://github.com/stac-extensions/processing) | The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only `L`, not `Level`). See the [list of suggested processing levels](#suggested-processing-levels). |
| `copernicus:lineage` | string | [Processing](https://github.com/stac-extensions/processing) | Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described [NASA ISO](https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information). For example, `GRD Post Processing` for "GRD" product of Sentinel-1 satellites. [CommonMark 0.29](https://commonmark.org/) syntax MAY be used for rich text representation. |
| `copernicus:looks_azimuth` | integer | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path. |
| `copernicus:looks_equivalent_number` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The equivalent number of looks (ENL). |
| `copernicus:looks_range` | integer | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path. |
| `copernicus:mmu` | number | [Vector](https://github.com/stac-extensions/vector) | Minimum Mapping Unit - the smallest polygon area represented. |
| `copernicus:mmw` | number | [Vector](https://github.com/stac-extensions/vector) | Minimal Mapping Width - the smallest real-world width represented as polygon. |
| `copernicus:moon_azimuth` | number | [View Geometry](https://github.com/stac-extensions/view) | Moon azimuth angle. From the scene center point on the ground, this is the angle between truth north and the moon. Measured clockwise in degrees (0-360). |
| `copernicus:moon_elevation` | number | [View Geometry](https://github.com/stac-extensions/view) | Moon elevation angle. The angle from the tangent of the scene center point to the moon. Measured from the horizon in degrees (`0`-`90`). |
| `copernicus:observation_direction` | string (enum) | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Antenna pointing direction relative to the flight trajectory of the satellite, either `left` or `right`. |
| `copernicus:off_nadir` | number | [View Geometry](https://github.com/stac-extensions/view) | The angle from the sensor between nadir (straight down) and the scene center. Measured in degrees (0-90). |
| `copernicus:offset` | number | [Raster](https://github.com/stac-extensions/raster) | Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:open_kwargs` | object | [Xarray Assets](https://github.com/stac-extensions/xarray-assets) | Keyword arguments to provide to the xarray opener |
| `copernicus:order_date` | string | [Order](https://github.com/stac-extensions/order) | Indicates the order submission time, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `copernicus:order_expiration_date` | string | [Order](https://github.com/stac-extensions/order) | **DEPRECATED.** Indicates the validity time of the order, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Use [`expires` from the timestamps extension](https://github.com/stac-extensions/timestamps/) instead. |
| `copernicus:order_id` | string | [Order](https://github.com/stac-extensions/order) | Identifier of the order. |
| `copernicus:order_status` | string (enum) | [Order](https://github.com/stac-extensions/order) | **REQUIRED**. Describe the status of the ordering. One of the value listed [here](#orderstatus) |
| `copernicus:original_data_type` | string (enum) | [Embeddings](https://github.com/stac-extensions/embeddings) | Data type before quantization. Uses the same [data type values](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types) as `data_type`. |
| `copernicus:pixel_spacing_azimuth` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| `copernicus:pixel_spacing_range` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type `GRD`. |
| `copernicus:polarizations` | array of string | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | RECOMMENDED. Any combination of polarizations. |
| `copernicus:primary_datetime` | string | [Table](https://github.com/stac-extensions/table) | The primary date/time column name. |
| `copernicus:primary_geometry` | string | [Table](https://github.com/stac-extensions/table) | The primary geometry column name. |
| `copernicus:product_status` | string (enum) | [Product](https://github.com/stac-extensions/product) | The lifecycle/status of the product. |
| `copernicus:product_type` | string | [Product](https://github.com/stac-extensions/product), [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The product type. |
| `copernicus:projjson` | any | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:published` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was published the first time, in UTC. |
| `copernicus:quality_status` | string (enum) | [Product](https://github.com/stac-extensions/product) | The quality status of the product: `nominal` or `degraded`. |
| `copernicus:quantization_method` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Quantization method (e.g. `linear`). |
| `copernicus:reference_scale` | integer | [Vector](https://github.com/stac-extensions/vector) | Representative fraction denominator (e.g., 50000 for 1:50,000). |
| `copernicus:relative_burst` | integer | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | Identification number that uniquely identifies a burst cycle within each repeat cycle. |
| `copernicus:resolution_azimuth` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m). |
| `copernicus:resolution_range` | number | [Synthetic Aperture Radar](https://github.com/stac-extensions/sar) | The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m). |
| `copernicus:row_count` | number | [Table](https://github.com/stac-extensions/table) | The number of rows in the dataset. |
| `copernicus:sampling` | string (enum) | [Raster](https://github.com/stac-extensions/raster) | One of `area` or `point`. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel. |
| `copernicus:scale` | number | [Raster](https://github.com/stac-extensions/raster) | Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:season` | string (enum) | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP season number. One of `S1` or `S2`. See below for details. |
| `copernicus:shape` | array of integer | [Projection](https://github.com/stac-extensions/projection) | Number of pixels in Y and X directions for the default grid |
| `copernicus:snow_cover` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of snow and ice cover as a percentage (0-100). |
| `copernicus:software` | map of string | [Processing](https://github.com/stac-extensions/processing) | A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes. |
| `copernicus:solar_illumination` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers. |
| `copernicus:spatial_resolution` | number | [Raster](https://github.com/stac-extensions/raster) | Average spatial resolution (in meters) of the pixels in the band. |
| `copernicus:standard_name` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF Standard Name](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html). |
| `copernicus:storage_options` | object | [Table](https://github.com/stac-extensions/table), [Xarray Assets](https://github.com/stac-extensions/xarray-assets) | **DEPRECATED** Additional keywords for opening the dataset. |
| `copernicus:stride` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | Step between the origins of neighboring chips in pixels as `[row_stride, col_stride]`. When `stride < chip_size`, chips overlap. |
| `copernicus:sub_parameter` | string (enum) | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP sub-parameter acronym. See below for the list of allowed values. |
| `copernicus:sun_azimuth` | number | [View Geometry](https://github.com/stac-extensions/view) | Sun azimuth angle. From the scene center point on the ground, this is the angle between truth north and the sun. Measured clockwise in degrees (0-360). |
| `copernicus:sun_elevation` | number | [View Geometry](https://github.com/stac-extensions/view) | Sun elevation angle. The angle from the tangent of the scene center point to the sun. Measured from the horizon in degrees (`-90`-`90`). Negative values indicate the sun is below the horizon, e.g. sun elevation of -10° means the data was captured during [nautical twilight](https://www.timeanddate.com/astronomy/different-types-twilight.html). |
| `copernicus:tables` | array of object | [Table](https://github.com/stac-extensions/table) | **DEPRECATED** A list of Table Objects (see below). |
| `copernicus:temporal_period` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Temporal compositing period as an [ISO 8601 duration](https://en.wikipedia.org/wiki/ISO_8601#Durations) (e.g. `P1Y`, `P3M`). |
| `copernicus:timeliness` | string | [Product](https://github.com/stac-extensions/product) | The average expected timeliness of the product as an [ISO 8601 Duration](https://en.wikipedia.org/wiki/ISO_8601#Durations). |
| `copernicus:timeliness_category` | string | [Product](https://github.com/stac-extensions/product) | A proprietary category identifier for the timeliness of the product. |
| `copernicus:transform` | array of number | [Projection](https://github.com/stac-extensions/projection) | The affine transformation coefficients for the default grid |
| `copernicus:unit` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `units`](https://cfconventions.org/cf-conventions/cf-conventions.html#units). |
| `copernicus:unpublished` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was unpublished, in UTC. |
| `copernicus:version` | string | [Processing](https://github.com/stac-extensions/processing) | The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions. |
| `copernicus:wkt2` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |

### Link fields

Fields usable in Links and Link Templates.

| Field | Type | Source Extension(s) | Description |
|-------|------|----------------------|-------------|
| `copernicus:auth_refs` | array of string | [Authentication](https://github.com/stac-extensions/authentication) | The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link. |
| `copernicus:auth_schemes` | map of auth_scheme | [Authentication](https://github.com/stac-extensions/authentication) | Dictionary of named authentication schemes that guard access to assets or links. |
| `copernicus:bbox` | array of number | [Projection](https://github.com/stac-extensions/projection) | Bounding box of the Item in the asset CRS in 2 or 3 dimensions. |
| `copernicus:centroid` | object | [Projection](https://github.com/stac-extensions/projection) | Coordinates representing the centroid of the Item (in lat/long) |
| `copernicus:code` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:expires` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) expires (is not valid any longer), in UTC. |
| `copernicus:geometry` | Geometry.json | [Projection](https://github.com/stac-extensions/projection) | Defines the footprint of this Item. |
| `copernicus:pmtiles_layers` | array of string | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The PMTiles layers to display. |
| `copernicus:projjson` | any | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:published` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was published the first time, in UTC. |
| `copernicus:servers` | array of string | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The servers to substitute for the {s} variable in the link href. |
| `copernicus:shape` | array of integer | [Projection](https://github.com/stac-extensions/projection) | Number of pixels in Y and X directions for the default grid |
| `copernicus:transform` | array of number | [Projection](https://github.com/stac-extensions/projection) | The affine transformation coefficients for the default grid |
| `copernicus:unpublished` | string | [Timestamps](https://github.com/stac-extensions/timestamps) | Date and time the corresponding data (see below) was unpublished, in UTC. |
| `copernicus:wkt2` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:wms_dimensions` | object | [Web Map Links](https://github.com/stac-extensions/web-map-links) | WMS dimensions and their values. |
| `copernicus:wms_layers` | array of string | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The WMS layers to display. |
| `copernicus:wms_styles` | array of string | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The WMS styles to apply. |
| `copernicus:wms_transparent` | boolean | [Web Map Links](https://github.com/stac-extensions/web-map-links) | Whether the WMS map background is transparent. |
| `copernicus:wmts_dimensions` | object | [Web Map Links](https://github.com/stac-extensions/web-map-links) | WMTS dimensions and their values. |
| `copernicus:wmts_encoding` | string (enum) | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The encoding to use for WMTS requests: `rest` or `kvp`. |
| `copernicus:wmts_layer` | string | [Web Map Links](https://github.com/stac-extensions/web-map-links) | The WMTS layer identifier. |

### Band fields

Fields usable in Band Objects (`bands` arrays on assets or item properties).

| Field | Type | Source Extension(s) | Description |
|-------|------|----------------------|-------------|
| `copernicus:bbox` | array of number | [Projection](https://github.com/stac-extensions/projection) | Bounding box of the Item in the asset CRS in 2 or 3 dimensions. |
| `copernicus:bitfields` | [bit_field_object](#bit_field_object) | [Classification](https://github.com/stac-extensions/classification) | Classes stored in bit fields in the raster |
| `copernicus:bits_per_sample` | integer | [Raster](https://github.com/stac-extensions/raster) | The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the `datatype`, such as when a 1 bit TIFF is represented as byte. |
| `copernicus:cell_methods` | array of string/null | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | null] |
| `copernicus:center_wavelength` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | The center wavelength of the band, in micrometers (μm). |
| `copernicus:centroid` | object | [Projection](https://github.com/stac-extensions/projection) | Coordinates representing the centroid of the Item (in lat/long) |
| `copernicus:chip_size` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | Chip size in pixels as `[height, width]`. |
| `copernicus:classes` | [class_object](#class_object) | [Classification](https://github.com/stac-extensions/classification) | Classes stored in raster or bands |
| `copernicus:cloud_cover` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of cloud cover as a percentage (0-100). |
| `copernicus:code` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:common_name` | string (enum) | [Electro-Optical](https://github.com/stac-extensions/eo) | The name commonly used to refer to the band to make it easier to search for bands across instruments. See the [list of accepted common names](#common-band-names). |
| `copernicus:datastrip_id` | string | [EOPF](https://github.com/CS-SI/eopf-stac-extension), [Processing](https://github.com/stac-extensions/processing) | The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See [Datastrip ID](#datastrip-id) for details. |
| `copernicus:datetime` | string | [Processing](https://github.com/stac-extensions/processing) | Processing date and time of the corresponding data formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6), in UTC. |
| `copernicus:description` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `long_name`](https://cfconventions.org/cf-conventions/cf-conventions.html#long-name). |
| `copernicus:embedding_dimensions` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding dimensions as an array of sizes, e.g. `[768]` for a single 768-dimensional vector. |
| `copernicus:embedding_type` | string (enum) | [Embeddings](https://github.com/stac-extensions/embeddings) | **REQUIRED**. Embedding type: `pixel` or `chip`. |
| `copernicus:expression` | object | [Processing](https://github.com/stac-extensions/processing) | An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type `processing-expression` (see below). |
| `copernicus:facility` | string | [Processing](https://github.com/stac-extensions/processing) | The name of the facility that produced the data. For example, `Copernicus S1 Core Ground Segment - DPA` for product of Sentinel-1 satellites. |
| `copernicus:full_width_half_max` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm). |
| `copernicus:geometry` | Geometry.json | [Projection](https://github.com/stac-extensions/projection) | Defines the footprint of this Item. |
| `copernicus:grid_id` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Grid system the chips are aligned to. See [Grid IDs](#grid-ids). |
| `copernicus:histogram` | object | [Raster](https://github.com/stac-extensions/raster) | Histogram distribution information of the pixels values in the band. |
| `copernicus:level` | string | [Processing](https://github.com/stac-extensions/processing) | The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only `L`, not `Level`). See the [list of suggested processing levels](#suggested-processing-levels). |
| `copernicus:lineage` | string | [Processing](https://github.com/stac-extensions/processing) | Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described [NASA ISO](https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information). For example, `GRD Post Processing` for "GRD" product of Sentinel-1 satellites. [CommonMark 0.29](https://commonmark.org/) syntax MAY be used for rich text representation. |
| `copernicus:offset` | number | [Raster](https://github.com/stac-extensions/raster) | Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:original_data_type` | string (enum) | [Embeddings](https://github.com/stac-extensions/embeddings) | Data type before quantization. Uses the same [data type values](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types) as `data_type`. |
| `copernicus:projjson` | any | [Projection](https://github.com/stac-extensions/projection) | null |
| `copernicus:quantization_method` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Quantization method (e.g. `linear`). |
| `copernicus:sampling` | string (enum) | [Raster](https://github.com/stac-extensions/raster) | One of `area` or `point`. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel. |
| `copernicus:scale` | number | [Raster](https://github.com/stac-extensions/raster) | Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance). |
| `copernicus:season` | string (enum) | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP season number. One of `S1` or `S2`. See below for details. |
| `copernicus:shape` | array of integer | [Projection](https://github.com/stac-extensions/projection) | Number of pixels in Y and X directions for the default grid |
| `copernicus:snow_cover` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | Estimate of snow and ice cover as a percentage (0-100). |
| `copernicus:software` | map of string | [Processing](https://github.com/stac-extensions/processing) | A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes. |
| `copernicus:solar_illumination` | number | [Electro-Optical](https://github.com/stac-extensions/eo) | The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers. |
| `copernicus:spatial_resolution` | number | [Raster](https://github.com/stac-extensions/raster) | Average spatial resolution (in meters) of the pixels in the band. |
| `copernicus:standard_name` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF Standard Name](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html). |
| `copernicus:stride` | array of integer | [Embeddings](https://github.com/stac-extensions/embeddings) | Step between the origins of neighboring chips in pixels as `[row_stride, col_stride]`. When `stride < chip_size`, chips overlap. |
| `copernicus:sub_parameter` | string (enum) | [Vegetation Phenology and Productivity](https://github.com/stac-extensions/vpp) | The VPP sub-parameter acronym. See below for the list of allowed values. |
| `copernicus:temporal_period` | string | [Embeddings](https://github.com/stac-extensions/embeddings) | Temporal compositing period as an [ISO 8601 duration](https://en.wikipedia.org/wiki/ISO_8601#Durations) (e.g. `P1Y`, `P3M`). |
| `copernicus:transform` | array of number | [Projection](https://github.com/stac-extensions/projection) | The affine transformation coefficients for the default grid |
| `copernicus:unit` | string | [Climate and Forecast (CF) Conventions](https://github.com/stac-extensions/cf) | Corresponds to the [CF `units`](https://cfconventions.org/cf-conventions/cf-conventions.html#units). |
| `copernicus:version` | string | [Processing](https://github.com/stac-extensions/processing) | The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions. |
| `copernicus:wkt2` | string or null | [Projection](https://github.com/stac-extensions/projection) | null |

### Collection and Catalog fields

Fields usable only on Collections and Catalogs (not in Item Properties).

| Field | Type | Source Extension(s) | Description |
|-------|------|----------------------|-------------|
| `copernicus:stats_catalogs` | object | [Stats](https://github.com/stac-extensions/stats) | A lookup of statistics for all child catalogs. |
| `copernicus:stats_collections` | object | [Stats](https://github.com/stac-extensions/stats) | A lookup of statistics for all child collections. |
| `copernicus:stats_items` | object | [Stats](https://github.com/stac-extensions/stats) | A lookup of statistics for all child items. |

### Nested object fields

Fields that appear inside object-valued `copernicus:` fields (e.g. each entry of the
`copernicus:renders` map, each class in `copernicus:classes`, each variable in
`copernicus:variables`).

| Field | Type | Applies To | Source Extension(s) | Description |
|-------|------|------------|---------------------|-------------|
| **Render Object** (`copernicus:renders`) | | | | |
| `copernicus:renders/asset_as_band` | boolean | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Treat assets in `expression` as single bands. Required when expression uses multiple assets |
| `copernicus:renders/assets` | array | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | **REQUIRED**. Array of asset keys [referencing the assets](#assets-reference) that are used to make the rendering |
| `copernicus:renders/bidx` | array | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Band(s) to select from each referenced asset, one entry per position in `assets` (an asset needing no sub-selection uses an empty array `[]`). Each selector is either a 1-based band index (matching the GDAL/rio-tiler/titiler convention) or a band name matching the `name` of a Band Object declared on that asset (via `eo:bands`, `raster:bands`, or the STAC [common `bands`](https://github.com/radiantearth/stac-spec/blob/v1.1.0/commons/common-metadata.md#bands) construct) — useful since `name` is not required on a Band Object. See [Band references](#band-references). |
| `copernicus:renders/color_formula` | string | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | [Color formula](https://developmentseed.org/titiler/user_guide/rendering/#color-formula) that must be applied for a raster band |
| `copernicus:renders/colormap` | object | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | [Color map JSON definition](https://developmentseed.org/titiler/user_guide/rendering/#custom-colormaps) that must be applied for a raster band |
| `copernicus:renders/colormap_name` | string | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Color map identifier that must be applied for a raster band |
| `copernicus:renders/expression` | string/object/array | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Band arithmetic formula to apply to the referenced assets. The format is defined by the rendering application, e.g. a [TiTiler](https://developmentseed.org/titiler/) band math string or a [MapLibre](https://maplibre.org/maplibre-style-spec/expressions/) style expression array. |
| `copernicus:renders/minmax_zoom` | array | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Zoom levels range applicable for the visualization |
| `copernicus:renders/nodata` | number/string | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Nodata value to use for this render, overriding any nodata value already defined on the referenced assets (e.g. via the [raster](https://github.com/stac-extensions/raster) extension). If not set, implementations SHOULD fall back to the asset's own nodata value. |
| `copernicus:renders/resampling` | string | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Resampling algorithm to apply to the referenced assets. See [GDAL resampling algorithm](https://gdal.org/programs/gdalwarp.html#cmdoption-gdalwarp-r) for some examples. |
| `copernicus:renders/rescale` | array | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | 2 dimensions array of delimited Min,Max range per band. If not provided, the data will not be rescaled. |
| `copernicus:renders/title` | string | `copernicus:renders` values | [Render](https://github.com/stac-extensions/render) | Optional title of the rendering |
| **Contact Object** (`copernicus:contacts`) | | | | |
| `copernicus:contacts/addresses` | array | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Physical location at which contact can be made. |
| `copernicus:contacts/contactInstructions` | string | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Supplemental instructions on how or when to contact the responsible party. |
| `copernicus:contacts/description` | string | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Detailed multi-line description to fully explain the STAC entity. [CommonMark 0.29](https://commonmark.org/) syntax MAY be used for rich text representation. |
| `copernicus:contacts/emails` | array | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Email address at which contact can be made. |
| `copernicus:contacts/identifier` | string | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | A value uniquely identifying a contact. |
| `copernicus:contacts/links` | array | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Links related to the contact. The link relation should be `about` and the media type must indicate the content type of the link (e.g. `text/html` for a company's web page versus `text/vcard` for a virtual contact file). |
| `copernicus:contacts/logo` | any | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Graphic identifying a contact. The link relation must be `icon` and the media type must be an image media type. |
| `copernicus:contacts/name` | string | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | **REQUIRED if `organization` is missing**. The name of the responsible person. |
| `copernicus:contacts/organization` | string | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | **REQUIRED if `name` is missing**. Organization/affiliation of the contact. |
| `copernicus:contacts/phones` | array | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | Telephone numbers at which contact can be made. |
| `copernicus:contacts/position` | string | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | The name of the role or position of the responsible person taken from the organization's formal organizational hierarchy or chart. |
| `copernicus:contacts/roles` | object | `copernicus:contacts` values | [Contacts](https://github.com/stac-extensions/contacts) | The set of named duties, job functions and/or permissions associated with this contact. See [Roles](#roles) for recommended values. |
| **Theme Object** (`copernicus:themes`) | | | | |
| `copernicus:themes/concepts` | array | `copernicus:themes` values | [Themes](https://github.com/stac-extensions/themes) | **REQUIRED**. One or more entity/concept identifers from this knowledge system. |
| `copernicus:themes/scheme` | string | `copernicus:themes` values | [Themes](https://github.com/stac-extensions/themes) | **REQUIRED**. An identifier for the knowledge organization system used. It is recommended that the identifier is a resolvable URI. |
| **Histogram Object** (`copernicus:histogram`) | | | | |
| `copernicus:histogram/buckets` | array | `copernicus:histogram` values | [Raster](https://github.com/stac-extensions/raster) | Array of integer indicating the number of pixels included in the bucket. |
| `copernicus:histogram/count` | number | `copernicus:histogram` values | [Raster](https://github.com/stac-extensions/raster) | number of buckets of the distribution. |
| `copernicus:histogram/max` | number | `copernicus:histogram` values | [Raster](https://github.com/stac-extensions/raster) | minimum value of the distribution. Also the mean value of the last bucket. |
| `copernicus:histogram/min` | number | `copernicus:histogram` values | [Raster](https://github.com/stac-extensions/raster) | minimum value of the distribution. Also the mean value of the first bucket. |
| **Processing Expression Object** (`copernicus:expression`) | | | | |
| `copernicus:expression/expression` | any | `copernicus:expression` values | [Processing](https://github.com/stac-extensions/processing) | Any data type, depending on the format chosen. |
| `copernicus:expression/format` | string | `copernicus:expression` values | [Processing](https://github.com/stac-extensions/processing) | **REQUIRED** The type of the expression that is specified in the `expression` property. |
| **Publication Object** (`copernicus:publications`) | | | | |
| `copernicus:publications/citation` | string | `copernicus:publications` values | [Scientific Citation](https://github.com/stac-extensions/scientific) | Citation of a publication referencing the data. |
| `copernicus:publications/doi` | string | `copernicus:publications` values | [Scientific Citation](https://github.com/stac-extensions/scientific) | The DOI of a publication referencing the data. This MUST NOT be a DOIs link. |
| **Column Object** (`copernicus:columns`) | | | | |
| `copernicus:columns/description` | string | `copernicus:columns` values | [Table](https://github.com/stac-extensions/table) | Detailed multi-line description to explain the dimension. CommonMark 0.29 syntax MAY be used for rich text representation. |
| `copernicus:columns/name` | string | `copernicus:columns` values | [Table](https://github.com/stac-extensions/table) | **REQUIRED**. The column name. |
| `copernicus:columns/type` | string | `copernicus:columns` values | [Table](https://github.com/stac-extensions/table) | Native data type of the column. If using a file format with a type system (like Parquet), we recommend you use those types. |

## Field mapping

The table below maps the original extension field names to their `copernicus:` equivalents.

| Original field | Copernicus field | Source |
|----------------|------------------|--------|
| `sat:absolute_orbit` | `copernicus:absolute_orbit` | Satellite |
| `sat:acquisition_station` | `copernicus:acquisition_station` | Satellite |
| `product:acquisition_type` | `copernicus:acquisition_type` | Product |
| `alternate:alternate` | `copernicus:alternate` | Alternate Assets |
| `alternate:alternate_name` | `copernicus:alternate_name` | Alternate Assets |
| `sat:anx_datetime` | `copernicus:anx_datetime` | Satellite |
| `auth:auth_refs` | `copernicus:auth_refs` | Authentication |
| `auth:auth_schemes` | `copernicus:auth_schemes` | Authentication |
| `view:azimuth` | `copernicus:azimuth` | View Geometry |
| `sar:bandwidth` | `copernicus:bandwidth` | Synthetic Aperture Radar |
| `proj:bbox` | `copernicus:bbox` | Projection |
| `sar:beam_ids` | `copernicus:beam_ids` | Synthetic Aperture Radar |
| `classification:bitfields` | `copernicus:bitfields` | Classification |
| `raster:bits_per_sample` | `copernicus:bits_per_sample` | Raster |
| `cf:cell_methods` | `copernicus:cell_methods` | Climate and Forecast (CF) Conventions |
| `sar:center_frequency` | `copernicus:center_frequency` | Synthetic Aperture Radar |
| `eo:center_wavelength` | `copernicus:center_wavelength` | Electro-Optical |
| `proj:centroid` | `copernicus:centroid` | Projection |
| `emb:chip_size` | `copernicus:chip_size` | Embeddings |
| `sci:citation` | `copernicus:citation` | Scientific Citation |
| `classification:classes` | `copernicus:classes` | Classification |
| `eo:cloud_cover` | `copernicus:cloud_cover` | Electro-Optical |
| `proj:code` | `copernicus:code` | Projection |
| `table:columns` | `copernicus:columns` | Table |
| `eo:common_name` | `copernicus:common_name` | Electro-Optical |
| `contacts:contacts` | `copernicus:contacts` | Contacts |
| `region:country` | `copernicus:country` | Region |
| `processing:datastrip_id` | `copernicus:datastrip_id` | Processing |
| `eopf:datastrip_id` | `copernicus:datastrip_id` | EOPF |
| `eopf:datatake_id` | `copernicus:datatake_id` | EOPF |
| `processing:datetime` | `copernicus:datetime` | Processing |
| `cf:description` | `copernicus:description` | Climate and Forecast (CF) Conventions |
| `cube:dimensions` | `copernicus:dimensions` | Data Cube |
| `sci:doi` | `copernicus:doi` | Scientific Citation |
| `emb:embedding_dimensions` | `copernicus:embedding_dimensions` | Embeddings |
| `emb:embedding_type` | `copernicus:embedding_type` | Embeddings |
| `expires` | `copernicus:expires` | Timestamps |
| `processing:expression` | `copernicus:expression` | Processing |
| `processing:facility` | `copernicus:facility` | Processing |
| `sar:frequency_band` | `copernicus:frequency_band` | Synthetic Aperture Radar |
| `eo:full_width_half_max` | `copernicus:full_width_half_max` | Electro-Optical |
| `proj:geometry` | `copernicus:geometry` | Projection |
| `vector:geometry_types` | `copernicus:geometry_types` | Vector |
| `grid:grid_code` | `copernicus:grid_code` | Grid |
| `emb:grid_id` | `copernicus:grid_id` | Embeddings |
| `raster:histogram` | `copernicus:histogram` | Raster |
| `view:incidence_angle` | `copernicus:incidence_angle` | View Geometry |
| `eopf:instrument_configuration_id` | `copernicus:instrument_configuration_id` | EOPF |
| `altm:instrument_mode` | `copernicus:instrument_mode` | Altimetry |
| `sar:instrument_mode` | `copernicus:instrument_mode` | Synthetic Aperture Radar |
| `eopf:instrument_mode` | `copernicus:instrument_mode` | EOPF |
| `altm:instrument_type` | `copernicus:instrument_type` | Altimetry |
| `processing:level` | `copernicus:level` | Processing |
| `processing:lineage` | `copernicus:lineage` | Processing |
| `sar:looks_azimuth` | `copernicus:looks_azimuth` | Synthetic Aperture Radar |
| `sar:looks_equivalent_number` | `copernicus:looks_equivalent_number` | Synthetic Aperture Radar |
| `sar:looks_range` | `copernicus:looks_range` | Synthetic Aperture Radar |
| `vector:mmu` | `copernicus:mmu` | Vector |
| `vector:mmw` | `copernicus:mmw` | Vector |
| `view:moon_azimuth` | `copernicus:moon_azimuth` | View Geometry |
| `view:moon_elevation` | `copernicus:moon_elevation` | View Geometry |
| `region:name` | `copernicus:name` | Region |
| `altm:nominal_track` | `copernicus:nominal_track` | Altimetry |
| `sar:observation_direction` | `copernicus:observation_direction` | Synthetic Aperture Radar |
| `view:off_nadir` | `copernicus:off_nadir` | View Geometry |
| `raster:offset` | `copernicus:offset` | Raster |
| `xarray:open_kwargs` | `copernicus:open_kwargs` | Xarray Assets |
| `sat:orbit_cycle` | `copernicus:orbit_cycle` | Satellite |
| `sat:orbit_state` | `copernicus:orbit_state` | Satellite |
| `sat:orbit_state_vectors` | `copernicus:orbit_state_vectors` | Satellite |
| `order:order_date` | `copernicus:order_date` | Order |
| `order:order_expiration_date` | `copernicus:order_expiration_date` | Order |
| `order:order_id` | `copernicus:order_id` | Order |
| `order:order_status` | `copernicus:order_status` | Order |
| `eopf:origin_datetime` | `copernicus:origin_datetime` | EOPF |
| `emb:original_data_type` | `copernicus:original_data_type` | Embeddings |
| `sar:pixel_spacing_azimuth` | `copernicus:pixel_spacing_azimuth` | Synthetic Aperture Radar |
| `sar:pixel_spacing_range` | `copernicus:pixel_spacing_range` | Synthetic Aperture Radar |
| `sat:platform_international_designator` | `copernicus:platform_international_designator` | Satellite |
| `sar:polarizations` | `copernicus:polarizations` | Synthetic Aperture Radar |
| `table:primary_datetime` | `copernicus:primary_datetime` | Table |
| `table:primary_geometry` | `copernicus:primary_geometry` | Table |
| `product:product_status` | `copernicus:product_status` | Product |
| `product:product_type` | `copernicus:product_type` | Product |
| `sar:product_type` | `copernicus:product_type` | Synthetic Aperture Radar |
| `proj:projjson` | `copernicus:projjson` | Projection |
| `sci:publications` | `copernicus:publications` | Scientific Citation |
| `published` | `copernicus:published` | Timestamps |
| `product:quality_status` | `copernicus:quality_status` | Product |
| `emb:quantization_method` | `copernicus:quantization_method` | Embeddings |
| `vector:reference_scale` | `copernicus:reference_scale` | Vector |
| `sar:relative_burst` | `copernicus:relative_burst` | Synthetic Aperture Radar |
| `sat:relative_orbit` | `copernicus:relative_orbit` | Satellite |
| `render:renders` | `copernicus:renders` | Render |
| `sar:resolution_azimuth` | `copernicus:resolution_azimuth` | Synthetic Aperture Radar |
| `sar:resolution_range` | `copernicus:resolution_range` | Synthetic Aperture Radar |
| `table:row_count` | `copernicus:row_count` | Table |
| `raster:sampling` | `copernicus:sampling` | Raster |
| `altm:sampling_rate` | `copernicus:sampling_rate` | Altimetry |
| `raster:scale` | `copernicus:scale` | Raster |
| `vpp:season` | `copernicus:season` | Vegetation Phenology and Productivity |
| `proj:shape` | `copernicus:shape` | Projection |
| `eo:snow_cover` | `copernicus:snow_cover` | Electro-Optical |
| `processing:software` | `copernicus:software` | Processing |
| `eo:solar_illumination` | `copernicus:solar_illumination` | Electro-Optical |
| `raster:spatial_resolution` | `copernicus:spatial_resolution` | Raster |
| `cf:standard_name` | `copernicus:standard_name` | Climate and Forecast (CF) Conventions |
| `stats:stats_catalogs` | `copernicus:stats_catalogs` | Stats |
| `stats:stats_collections` | `copernicus:stats_collections` | Stats |
| `stats:stats_items` | `copernicus:stats_items` | Stats |
| `table:storage_options` | `copernicus:storage_options` | Table |
| `xarray:storage_options` | `copernicus:storage_options` | Xarray Assets |
| `emb:stride` | `copernicus:stride` | Embeddings |
| `vpp:sub_parameter` | `copernicus:sub_parameter` | Vegetation Phenology and Productivity |
| `region:subdivision` | `copernicus:subdivision` | Region |
| `view:sun_azimuth` | `copernicus:sun_azimuth` | View Geometry |
| `view:sun_elevation` | `copernicus:sun_elevation` | View Geometry |
| `table:tables` | `copernicus:tables` | Table |
| `emb:temporal_period` | `copernicus:temporal_period` | Embeddings |
| `themes:themes` | `copernicus:themes` | Themes |
| `product:timeliness` | `copernicus:timeliness` | Product |
| `product:timeliness_category` | `copernicus:timeliness_category` | Product |
| `proj:transform` | `copernicus:transform` | Projection |
| `cf:unit` | `copernicus:unit` | Climate and Forecast (CF) Conventions |
| `unpublished` | `copernicus:unpublished` | Timestamps |
| `cube:variables` | `copernicus:variables` | Data Cube |
| `processing:version` | `copernicus:version` | Processing |
| `proj:wkt2` | `copernicus:wkt2` | Projection |

## Named object schemas

Nested object definitions carried over from the source extensions:

| Definition | Type | Description |
|------------|------|-------------|
| [auth_scheme](json-schema/schema.json) | object |  |
| [oauth2_flow](json-schema/schema.json) | object |  |
| [signed_url_flow](json-schema/schema.json) | object |  |
| [class_object](json-schema/schema.json) | object | Object for storing classes |
| [bit_field_object](json-schema/schema.json) | object | Object for storing bit fields |
| [link](json-schema/schema.json) | object |  |
| [roles](json-schema/schema.json) | object |  |
| [variable](json-schema/schema.json) | object |  |
| [vector_dimension](json-schema/schema.json) | object |  |
| [horizontal_spatial_dimension](json-schema/schema.json) | object |  |
| [vertical_spatial_dimension](json-schema/schema.json) | object |  |
| [temporal_dimension](json-schema/schema.json) | object |  |
| [additional_dimension](json-schema/schema.json) | object |  |
| [object_with_integer_properties](json-schema/schema.json) | object |  |
| [object_without_href](json-schema/schema.json) | object |  |
| [name](json-schema/schema.json) | object |  |

## Best practices

- Use `copernicus:` fields instead of mixing multiple upstream extension prefixes.
- When a field exists in multiple source extensions (e.g. `instrument_mode` in SAR, altimetry
  and EOPF), the merged definition is the most general one; the source columns in the tables
  above list all origins.
- Fields with source-specific semantics keep distinct names, e.g. `copernicus:order_status`
  (from `order:status`) vs `copernicus:product_status` (from `product:status`).

## Schema

- [JSON Schema (draft-07)](json-schema/schema.json)
- Storage platform schemas: [aws-s3](json-schema/platforms/aws-s3.json),
  [custom-s3](json-schema/platforms/custom-s3.json),
  [ms-azure](json-schema/platforms/ms-azure.json)

## Examples

- [Item example](examples/item.json): a Sentinel-3 OLCI item with EO, SAR, satellite,
  processing, product, projection, storage, alternate assets, web map links and more.
- [Collection example](examples/collection.json): a Sentinel-3 collection with contacts,
  themes, datacube, renders, and stats.

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).

## License

[Apache-2.0](LICENSE)
