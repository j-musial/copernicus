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

All `134` fields defined by this extension, sorted alphabetically.

<table>
<colgroup><col width="22%"><col width="8%"><col width="13%"><col width="15%"><col width="42%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Applies To</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>copernicus:absolute_orbit</code></td><td>integer</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The absolute orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the absolute orbit number at the start of the acquisition.</td></tr>
<tr><td><code>copernicus:acquisition_station</code></td><td>string</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The acquisition station (ground station) where the satellite data was downlinked. Equivalent to <code>eop:acquisition_station</code> in OGC 10-157r4 and OGC 17-003r2.</td></tr>
<tr><td><code>copernicus:acquisition_type</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The acquisition type of the product.</td></tr>
<tr><td><code>copernicus:alternate</code></td><td>object</td><td>Assets</td><td><a href="docs/sources/alternate-assets-v1.2.0.md">Alternate Assets</a></td><td>Alternate asset locations keyed by provider name, each an Asset Object without href.</td></tr>
<tr><td><code>copernicus:alternate_name</code></td><td>string</td><td>Assets</td><td><a href="docs/sources/alternate-assets-v1.2.0.md">Alternate Assets</a></td><td>A human readable name for the alternate asset.</td></tr>
<tr><td><code>copernicus:anx_datetime</code></td><td>string</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The <a href="https://en.wikipedia.org/wiki/Orbital_node">Ascending Node</a> Crossing (ANX) time, in UTC. It is formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>.</td></tr>
<tr><td><code>copernicus:auth_refs</code></td><td>array of string</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link.</td></tr>
<tr><td><code>copernicus:auth_schemes</code></td><td>map of auth_scheme</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>Dictionary of named authentication schemes that guard access to assets or links.</td></tr>
<tr><td><code>copernicus:azimuth</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Viewing azimuth angle. The angle measured from the sub-satellite point (point on the ground below the platform) between the scene center and true north. Measured clockwise from north in degrees (0-360).</td></tr>
<tr><td><code>copernicus:bandwidth</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation.</td></tr>
<tr><td><code>copernicus:bbox</code></td><td>array of number</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Bounding box of the Item in the asset CRS in 2 or 3 dimensions.</td></tr>
<tr><td><code>copernicus:beam_ids</code></td><td>array of string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Composition of the swath of the SAR acquision referencing the beam identifiers.</td></tr>
<tr><td><code>copernicus:bitfields</code></td><td><a href="#bit_field_object">bit_field_object</a></td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in bit fields in the raster</td></tr>
<tr><td><code>copernicus:bits_per_sample</code></td><td>integer</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the <code>datatype</code>, such as when a 1 bit TIFF is represented as byte.</td></tr>
<tr><td><code>copernicus:cell_methods</code></td><td>array of string/null</td><td>Collections, Item Properties, Assets, Bands, Data Cube Variables</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>null]</td></tr>
<tr><td><code>copernicus:center_frequency</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz).</td></tr>
<tr><td><code>copernicus:center_wavelength</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The center wavelength of the band, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:centroid</code></td><td>object</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Coordinates representing the centroid of the Item (in lat/long)</td></tr>
<tr><td><code>copernicus:chip_size</code></td><td>array of integer</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Chip size in pixels as <code>[height, width]</code>.</td></tr>
<tr><td><code>copernicus:citation</code></td><td>string</td><td>Item Properties, Collections, Catalogs</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>The recommended human-readable reference (citation) to be used by publications citing the data. No specific citation style is suggested, but the citation should contain all information required to find the publication distinctively.</td></tr>
<tr><td><code>copernicus:classes</code></td><td><a href="#class_object">class_object</a></td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in raster or bands</td></tr>
<tr><td><code>copernicus:cloud_cover</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of cloud cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:code</code></td><td>string or null</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:columns</code></td><td>array of object</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>A list of Column Objects describing each column.</td></tr>
<tr><td><code>copernicus:common_name</code></td><td>string (enum)</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The name commonly used to refer to the band to make it easier to search for bands across instruments. See the <a href="#common-band-names">list of accepted common names</a>.</td></tr>
<tr><td><code>copernicus:contacts</code></td><td>array of object</td><td>Catalogs, Collections, Item Properties</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td><strong>REQUIRED.</strong> A list of contacts qualified by their role.</td></tr>
<tr><td><code>copernicus:country</code></td><td>string</td><td>Collections, Item Properties</td><td><a href="docs/sources/region-v0.1.0.md">Region</a></td><td>ISO 3166-1 alpha-2 country code. Two-letter country code for the country that is primarily covered by the data.</td></tr>
<tr><td><code>copernicus:datastrip_id</code></td><td>string</td><td>Item Properties, Assets, Bands, Providers, Collections</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See <a href="#datastrip-id">Datastrip ID</a> for details.</td></tr>
<tr><td><code>copernicus:datatake_id</code></td><td>string</td><td>Item Properties, Collections</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a></td><td>Datatake identification. Examples: for S1, datatake_id = 12032; for S2, datatake_id = GS2A_20231215T103431_044292_N05.10</td></tr>
<tr><td><code>copernicus:datetime</code></td><td>string</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Processing date and time of the corresponding data formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>, in UTC.</td></tr>
<tr><td><code>copernicus:description</code></td><td>string</td><td>Collections, Item Properties, Assets, Bands, Data Cube Variables</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#long-name">CF <code>long_name</code></a>.</td></tr>
<tr><td><code>copernicus:dimensions</code></td><td>object</td><td>Collections, Item Properties</td><td><a href="docs/sources/datacube-v2.3.0.md">Data Cube</a></td><td><strong>REQUIRED.</strong> Uniquely named dimensions of the datacube.</td></tr>
<tr><td><code>copernicus:doi</code></td><td>string</td><td>Item Properties, Collections, Catalogs</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>The DOI of the data, e.g. <code>10.1000/xyz123</code>. This MUST NOT be a DOIs link. For all DOI names respective DOI links SHOULD be added to the links section (see chapter "Relation types").</td></tr>
<tr><td><code>copernicus:embedding_dimensions</code></td><td>array of integer</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding dimensions as an array of sizes, e.g. <code>[768]</code> for a single 768-dimensional vector.</td></tr>
<tr><td><code>copernicus:embedding_type</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding type: <code>pixel</code> or <code>chip</code>.</td></tr>
<tr><td><code>copernicus:expires</code></td><td>string</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) expires (is not valid any longer), in UTC.</td></tr>
<tr><td><code>copernicus:expression</code></td><td>object</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type <code>processing-expression</code> (see below).</td></tr>
<tr><td><code>copernicus:facility</code></td><td>string</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name of the facility that produced the data. For example, <code>Copernicus S1 Core Ground Segment - DPA</code> for product of Sentinel-1 satellites.</td></tr>
<tr><td><code>copernicus:frequency_band</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names.</td></tr>
<tr><td><code>copernicus:full_width_half_max</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:geometry</code></td><td>Geometry.json</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Defines the footprint of this Item.</td></tr>
<tr><td><code>copernicus:geometry_types</code></td><td>array of string</td><td>Collections, Item Properties, Assets, Table Columns</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>A list of the geometry types present in the dataset.</td></tr>
<tr><td><code>copernicus:grid_code</code></td><td>string</td><td>Item Properties</td><td><a href="docs/sources/grid-v1.1.0.md">Grid</a></td><td><strong>REQUIRED</strong>. The identifier for the grid element associated with the Item.</td></tr>
<tr><td><code>copernicus:grid_id</code></td><td>string</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Grid system the chips are aligned to. See <a href="#grid-ids">Grid IDs</a>.</td></tr>
<tr><td><code>copernicus:histogram</code></td><td>object</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Histogram distribution information of the pixels values in the band.</td></tr>
<tr><td><code>copernicus:incidence_angle</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>The incidence angle is the angle between the vertical (normal) to the intercepting surface and the line of sight back to the satellite at the scene center. Measured in degrees (0-90).</td></tr>
<tr><td><code>copernicus:instrument_configuration_id</code></td><td>integer</td><td>Item Properties, Collections</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a></td><td>The instrument configuration ID is specific to S1 SAR instrument and refers to the onboard configuration. Each version of it has a specific identifier called "Instrument Configuration ID" (ICID) corresponding to a specific number. For more information, cf. <a href="https://sar-mpc.eu/about/faq/">"What is the instrument configuration ID (ICID) ?"</a></td></tr>
<tr><td><code>copernicus:instrument_mode</code></td><td>string</td><td>Item Properties, Collections, Assets</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a>, <a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Mode of the altimetry instrument used to collect the data.</td></tr>
<tr><td><code>copernicus:instrument_type</code></td><td>string (enum)</td><td>Item Properties</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a></td><td>Type of altimetry instrument used to collect the data.</td></tr>
<tr><td><code>copernicus:level</code></td><td>string</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only <code>L</code>, not <code>Level</code>). See the <a href="#suggested-processing-levels">list of suggested processing levels</a>.</td></tr>
<tr><td><code>copernicus:lineage</code></td><td>string</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described <a href="https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information">NASA ISO</a>. For example, <code>GRD Post Processing</code> for "GRD" product of Sentinel-1 satellites. <a href="https://commonmark.org/">CommonMark 0.29</a> syntax MAY be used for rich text representation.</td></tr>
<tr><td><code>copernicus:looks_azimuth</code></td><td>integer</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path.</td></tr>
<tr><td><code>copernicus:looks_equivalent_number</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The equivalent number of looks (ENL).</td></tr>
<tr><td><code>copernicus:looks_range</code></td><td>integer</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path.</td></tr>
<tr><td><code>copernicus:mmu</code></td><td>number</td><td>Collections, Item Properties, Assets, Table Columns</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Minimum Mapping Unit - the smallest polygon area represented.</td></tr>
<tr><td><code>copernicus:mmw</code></td><td>number</td><td>Collections, Item Properties, Assets, Table Columns</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Minimal Mapping Width - the smallest real-world width represented as polygon.</td></tr>
<tr><td><code>copernicus:moon_azimuth</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Moon azimuth angle. From the scene center point on the ground, this is the angle between truth north and the moon. Measured clockwise in degrees (0-360).</td></tr>
<tr><td><code>copernicus:moon_elevation</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Moon elevation angle. The angle from the tangent of the scene center point to the moon. Measured from the horizon in degrees (<code>0</code>-<code>90</code>).</td></tr>
<tr><td><code>copernicus:name</code></td><td>string</td><td>Collections, Item Properties</td><td><a href="docs/sources/region-v0.1.0.md">Region</a></td><td>A human-readable name of the relevant region.</td></tr>
<tr><td><code>copernicus:nominal_track</code></td><td>coordinates</td><td>Item Properties</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a></td><td>An array of coordinates used to define the nominal track on the earths surface. This value is recommended ONLY if the item geometry is not representative of the acquisition track.</td></tr>
<tr><td><code>copernicus:observation_direction</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Antenna pointing direction relative to the flight trajectory of the satellite, either <code>left</code> or <code>right</code>.</td></tr>
<tr><td><code>copernicus:off_nadir</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>The angle from the sensor between nadir (straight down) and the scene center. Measured in degrees (0-90).</td></tr>
<tr><td><code>copernicus:offset</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:open_kwargs</code></td><td>object</td><td>Assets</td><td><a href="docs/sources/xarray-assets-v1.0.0.md">Xarray Assets</a></td><td>Keyword arguments to provide to the xarray opener</td></tr>
<tr><td><code>copernicus:orbit_cycle</code></td><td>integer</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The number of repeat cycle done by the satellite at the time of the acquisition. <a href="https://ltb.itc.utwente.nl/page/498/concept/81577">Repeat cycle</a> is the time between two successive identical orbits.</td></tr>
<tr><td><code>copernicus:orbit_state</code></td><td>string (enum)</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The state of the orbit. Either <code>ascending</code> or <code>descending</code> for polar orbiting satellites, <code>geostationary</code> for geosynchronous satellites, or <code>crossing</code> when the acquisition spans a polar crossing.</td></tr>
<tr><td><code>copernicus:orbit_state_vectors</code></td><td>map of array</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The state vectors of the satellite at the time of acquisition.</td></tr>
<tr><td><code>copernicus:order_date</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td>Indicates the order submission time, in UTC and formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>.</td></tr>
<tr><td><code>copernicus:order_expiration_date</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td><strong>DEPRECATED.</strong> Indicates the validity time of the order, in UTC and formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>. Use <a href="https://github.com/stac-extensions/timestamps/"><code>expires</code> from the timestamps extension</a> instead.</td></tr>
<tr><td><code>copernicus:order_id</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td>Identifier of the order.</td></tr>
<tr><td><code>copernicus:order_status</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td><strong>REQUIRED</strong>. Describe the status of the ordering. One of the value listed <a href="#orderstatus">here</a></td></tr>
<tr><td><code>copernicus:origin_datetime</code></td><td>string</td><td>Item Properties, Collections</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a></td><td>Date time of the input data considered to create the item. Example: for PRIP, time of the availability of all CADU data on the CADIP/XBIP</td></tr>
<tr><td><code>copernicus:original_data_type</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Data type before quantization. Uses the same <a href="https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types">data type values</a> as <code>data_type</code>.</td></tr>
<tr><td><code>copernicus:pixel_spacing_azimuth</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type <code>GRD</code>.</td></tr>
<tr><td><code>copernicus:pixel_spacing_range</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type <code>GRD</code>.</td></tr>
<tr><td><code>copernicus:platform_international_designator</code></td><td>string</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The International Designator, also known as COSPAR ID, and NSSDCA ID</td></tr>
<tr><td><code>copernicus:pmtiles_layers</code></td><td>array of string</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The PMTiles layers to display.</td></tr>
<tr><td><code>copernicus:polarizations</code></td><td>array of string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. Any combination of polarizations.</td></tr>
<tr><td><code>copernicus:primary_datetime</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The primary date/time column name.</td></tr>
<tr><td><code>copernicus:primary_geometry</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The primary geometry column name.</td></tr>
<tr><td><code>copernicus:product_status</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The lifecycle/status of the product.</td></tr>
<tr><td><code>copernicus:product_type</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/product-v1.1.0.md">Product</a>, <a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The product type.</td></tr>
<tr><td><code>copernicus:projjson</code></td><td>any</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:publications</code></td><td>array of object</td><td>Item Properties, Collections, Catalogs</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>List of relevant publications referencing and describing the data.</td></tr>
<tr><td><code>copernicus:published</code></td><td>string</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was published the first time, in UTC.</td></tr>
<tr><td><code>copernicus:quality_status</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The quality status of the product: <code>nominal</code> or <code>degraded</code>.</td></tr>
<tr><td><code>copernicus:quantization_method</code></td><td>string</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Quantization method (e.g. <code>linear</code>).</td></tr>
<tr><td><code>copernicus:reference_scale</code></td><td>integer</td><td>Collections, Item Properties, Assets, Table Columns</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Representative fraction denominator (e.g., 50000 for 1:50,000).</td></tr>
<tr><td><code>copernicus:relative_burst</code></td><td>integer</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Identification number that uniquely identifies a burst cycle within each repeat cycle.</td></tr>
<tr><td><code>copernicus:relative_orbit</code></td><td>integer</td><td>Item Properties, Collections</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The relative orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the relative orbit number at the start of the acquisition.</td></tr>
<tr><td><code>copernicus:renders</code></td><td>object</td><td>Collections, Item Properties</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Dictionary of rendering instructions that can be viewed, keyed by a unique render name.</td></tr>
<tr><td><code>copernicus:resolution_azimuth</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m).</td></tr>
<tr><td><code>copernicus:resolution_range</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m).</td></tr>
<tr><td><code>copernicus:row_count</code></td><td>number</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The number of rows in the dataset.</td></tr>
<tr><td><code>copernicus:sampling</code></td><td>string (enum)</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>One of <code>area</code> or <code>point</code>. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel.</td></tr>
<tr><td><code>copernicus:sampling_rate</code></td><td>number</td><td>Item Properties</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a></td><td>Sampling rate of the altimetry instrument in Hz.</td></tr>
<tr><td><code>copernicus:scale</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:season</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP season number. One of <code>S1</code> or <code>S2</code>. See below for details.</td></tr>
<tr><td><code>copernicus:servers</code></td><td>array of string</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The servers to substitute for the {s} variable in the link href.</td></tr>
<tr><td><code>copernicus:shape</code></td><td>array of integer</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Number of pixels in Y and X directions for the default grid</td></tr>
<tr><td><code>copernicus:snow_cover</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of snow and ice cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:software</code></td><td>map of string</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes.</td></tr>
<tr><td><code>copernicus:solar_illumination</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers.</td></tr>
<tr><td><code>copernicus:spatial_resolution</code></td><td>number</td><td>Item Properties, Assets, Bands</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Average spatial resolution (in meters) of the pixels in the band.</td></tr>
<tr><td><code>copernicus:standard_name</code></td><td>string</td><td>Collections, Item Properties, Assets, Bands, Data Cube Variables</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html">CF Standard Name</a>.</td></tr>
<tr><td><code>copernicus:stats_catalogs</code></td><td>object</td><td>Collections, Catalogs</td><td><a href="docs/sources/stats-v0.2.0.md">Stats</a></td><td>A lookup of statistics for all child catalogs.</td></tr>
<tr><td><code>copernicus:stats_collections</code></td><td>object</td><td>Collections, Catalogs</td><td><a href="docs/sources/stats-v0.2.0.md">Stats</a></td><td>A lookup of statistics for all child collections.</td></tr>
<tr><td><code>copernicus:stats_items</code></td><td>object</td><td>Collections, Catalogs</td><td><a href="docs/sources/stats-v0.2.0.md">Stats</a></td><td>A lookup of statistics for all child items.</td></tr>
<tr><td><code>copernicus:storage_options</code></td><td>object</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/table-v1.3.0.md">Table</a>, <a href="docs/sources/xarray-assets-v1.0.0.md">Xarray Assets</a></td><td><strong>DEPRECATED</strong> Additional keywords for opening the dataset.</td></tr>
<tr><td><code>copernicus:storage_refs</code></td><td>array of string</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that specifies which schemes in copernicus:storage_schemes may be used to access an Asset or Link. Each value must be one of the keys defined in copernicus:storage_schemes.</td></tr>
<tr><td><code>copernicus:storage_schemes</code></td><td>map of objects</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that contains all of the storage schemes used by Assets and Links in the STAC Item, Catalog or Collection.</td></tr>
<tr><td><code>copernicus:stride</code></td><td>array of integer</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Step between the origins of neighboring chips in pixels as <code>[row_stride, col_stride]</code>. When <code>stride &lt; chip_size</code>, chips overlap.</td></tr>
<tr><td><code>copernicus:sub_parameter</code></td><td>string (enum)</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP sub-parameter acronym. See below for the list of allowed values.</td></tr>
<tr><td><code>copernicus:subdivision</code></td><td>string</td><td>Collections, Item Properties</td><td><a href="docs/sources/region-v0.1.0.md">Region</a></td><td>ISO 3166-2 codes for identifying the principal subdivisions (e.g., provinces or states) of a country that is primarily covered by the data. Only provide the second part of the ISO 3166-2 code to reduce redundancy.</td></tr>
<tr><td><code>copernicus:sun_azimuth</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Sun azimuth angle. From the scene center point on the ground, this is the angle between truth north and the sun. Measured clockwise in degrees (0-360).</td></tr>
<tr><td><code>copernicus:sun_elevation</code></td><td>number</td><td>Item Properties, Assets</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Sun elevation angle. The angle from the tangent of the scene center point to the sun. Measured from the horizon in degrees (<code>-90</code>-<code>90</code>). Negative values indicate the sun is below the horizon, e.g. sun elevation of -10° means the data was captured during <a href="https://www.timeanddate.com/astronomy/different-types-twilight.html">nautical twilight</a>.</td></tr>
<tr><td><code>copernicus:tables</code></td><td>array of object</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td><strong>DEPRECATED</strong> A list of Table Objects (see below).</td></tr>
<tr><td><code>copernicus:temporal_period</code></td><td>string</td><td>Collections, Item Properties, Assets, Bands</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Temporal compositing period as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 duration</a> (e.g. <code>P1Y</code>, <code>P3M</code>).</td></tr>
<tr><td><code>copernicus:themes</code></td><td>array of object</td><td>Catalogs, Collections, Item Properties</td><td><a href="docs/sources/themes-v1.0.0.md">Themes</a></td><td><strong>REQUIRED.</strong> A knowledge organization system used to classify the STAC entity. Each element is a concept and their respective knowledge organization system / controlled vocabulary.</td></tr>
<tr><td><code>copernicus:timeliness</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The average expected timeliness of the product as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 Duration</a>.</td></tr>
<tr><td><code>copernicus:timeliness_category</code></td><td>string</td><td>Collections, Item Properties, Assets</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>A proprietary category identifier for the timeliness of the product.</td></tr>
<tr><td><code>copernicus:transform</code></td><td>array of number</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>The affine transformation coefficients for the default grid</td></tr>
<tr><td><code>copernicus:unit</code></td><td>string</td><td>Collections, Item Properties, Assets, Bands, Data Cube Variables</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#units">CF <code>units</code></a>.</td></tr>
<tr><td><code>copernicus:unpublished</code></td><td>string</td><td>Catalogs, Collections, Item Properties, Assets, Links</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was unpublished, in UTC.</td></tr>
<tr><td><code>copernicus:variables</code></td><td>object</td><td>Collections, Item Properties</td><td><a href="docs/sources/datacube-v2.3.0.md">Data Cube</a></td><td>Uniquely named variables of the datacube.</td></tr>
<tr><td><code>copernicus:version</code></td><td>string</td><td>Item Properties, Assets, Bands, Providers</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions.</td></tr>
<tr><td><code>copernicus:wkt2</code></td><td>string or null</td><td>Collections, Item Properties, Assets, Links, Bands</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:wms_dimensions</code></td><td>object</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>WMS dimensions and their values.</td></tr>
<tr><td><code>copernicus:wms_layers</code></td><td>array of string</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The WMS layers to display.</td></tr>
<tr><td><code>copernicus:wms_styles</code></td><td>array of string</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The WMS styles to apply.</td></tr>
<tr><td><code>copernicus:wms_transparent</code></td><td>boolean</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>Whether the WMS map background is transparent.</td></tr>
<tr><td><code>copernicus:wmts_dimensions</code></td><td>object</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>WMTS dimensions and their values.</td></tr>
<tr><td><code>copernicus:wmts_encoding</code></td><td>string (enum)</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The encoding to use for WMTS requests: <code>rest</code> or <code>kvp</code>.</td></tr>
<tr><td><code>copernicus:wmts_layer</code></td><td>string</td><td>Links</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The WMTS layer identifier.</td></tr>
</tbody>
</table>

### Item Properties fields

Fields usable in Item Properties (and Collection Summaries).

<table>
<colgroup><col width="24%"><col width="10%"><col width="18%"><col width="48%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>copernicus:absolute_orbit</code></td><td>integer</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The absolute orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the absolute orbit number at the start of the acquisition.</td></tr>
<tr><td><code>copernicus:acquisition_station</code></td><td>string</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The acquisition station (ground station) where the satellite data was downlinked. Equivalent to <code>eop:acquisition_station</code> in OGC 10-157r4 and OGC 17-003r2.</td></tr>
<tr><td><code>copernicus:acquisition_type</code></td><td>string (enum)</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The acquisition type of the product.</td></tr>
<tr><td><code>copernicus:anx_datetime</code></td><td>string</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The <a href="https://en.wikipedia.org/wiki/Orbital_node">Ascending Node</a> Crossing (ANX) time, in UTC. It is formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>.</td></tr>
<tr><td><code>copernicus:auth_refs</code></td><td>array of string</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link.</td></tr>
<tr><td><code>copernicus:auth_schemes</code></td><td>map of auth_scheme</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>Dictionary of named authentication schemes that guard access to assets or links.</td></tr>
<tr><td><code>copernicus:azimuth</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Viewing azimuth angle. The angle measured from the sub-satellite point (point on the ground below the platform) between the scene center and true north. Measured clockwise from north in degrees (0-360).</td></tr>
<tr><td><code>copernicus:bandwidth</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation.</td></tr>
<tr><td><code>copernicus:bbox</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Bounding box of the Item in the asset CRS in 2 or 3 dimensions.</td></tr>
<tr><td><code>copernicus:beam_ids</code></td><td>array of string</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Composition of the swath of the SAR acquision referencing the beam identifiers.</td></tr>
<tr><td><code>copernicus:bitfields</code></td><td><a href="#bit_field_object">bit_field_object</a></td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in bit fields in the raster</td></tr>
<tr><td><code>copernicus:bits_per_sample</code></td><td>integer</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the <code>datatype</code>, such as when a 1 bit TIFF is represented as byte.</td></tr>
<tr><td><code>copernicus:cell_methods</code></td><td>array of string/null</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>null]</td></tr>
<tr><td><code>copernicus:center_frequency</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz).</td></tr>
<tr><td><code>copernicus:center_wavelength</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The center wavelength of the band, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:centroid</code></td><td>object</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Coordinates representing the centroid of the Item (in lat/long)</td></tr>
<tr><td><code>copernicus:chip_size</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Chip size in pixels as <code>[height, width]</code>.</td></tr>
<tr><td><code>copernicus:citation</code></td><td>string</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>The recommended human-readable reference (citation) to be used by publications citing the data. No specific citation style is suggested, but the citation should contain all information required to find the publication distinctively.</td></tr>
<tr><td><code>copernicus:classes</code></td><td><a href="#class_object">class_object</a></td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in raster or bands</td></tr>
<tr><td><code>copernicus:cloud_cover</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of cloud cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:code</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:columns</code></td><td>array of object</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>A list of Column Objects describing each column.</td></tr>
<tr><td><code>copernicus:common_name</code></td><td>string (enum)</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The name commonly used to refer to the band to make it easier to search for bands across instruments. See the <a href="#common-band-names">list of accepted common names</a>.</td></tr>
<tr><td><code>copernicus:contacts</code></td><td>array of object</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td><strong>REQUIRED.</strong> A list of contacts qualified by their role.</td></tr>
<tr><td><code>copernicus:country</code></td><td>string</td><td><a href="docs/sources/region-v0.1.0.md">Region</a></td><td>ISO 3166-1 alpha-2 country code. Two-letter country code for the country that is primarily covered by the data.</td></tr>
<tr><td><code>copernicus:datastrip_id</code></td><td>string</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See <a href="#datastrip-id">Datastrip ID</a> for details.</td></tr>
<tr><td><code>copernicus:datatake_id</code></td><td>string</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a></td><td>Datatake identification. Examples: for S1, datatake_id = 12032; for S2, datatake_id = GS2A_20231215T103431_044292_N05.10</td></tr>
<tr><td><code>copernicus:datetime</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Processing date and time of the corresponding data formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>, in UTC.</td></tr>
<tr><td><code>copernicus:description</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#long-name">CF <code>long_name</code></a>.</td></tr>
<tr><td><code>copernicus:dimensions</code></td><td>object</td><td><a href="docs/sources/datacube-v2.3.0.md">Data Cube</a></td><td><strong>REQUIRED.</strong> Uniquely named dimensions of the datacube.</td></tr>
<tr><td><code>copernicus:doi</code></td><td>string</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>The DOI of the data, e.g. <code>10.1000/xyz123</code>. This MUST NOT be a DOIs link. For all DOI names respective DOI links SHOULD be added to the links section (see chapter "Relation types").</td></tr>
<tr><td><code>copernicus:embedding_dimensions</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding dimensions as an array of sizes, e.g. <code>[768]</code> for a single 768-dimensional vector.</td></tr>
<tr><td><code>copernicus:embedding_type</code></td><td>string (enum)</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding type: <code>pixel</code> or <code>chip</code>.</td></tr>
<tr><td><code>copernicus:expires</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) expires (is not valid any longer), in UTC.</td></tr>
<tr><td><code>copernicus:expression</code></td><td>object</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type <code>processing-expression</code> (see below).</td></tr>
<tr><td><code>copernicus:facility</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name of the facility that produced the data. For example, <code>Copernicus S1 Core Ground Segment - DPA</code> for product of Sentinel-1 satellites.</td></tr>
<tr><td><code>copernicus:frequency_band</code></td><td>string (enum)</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names.</td></tr>
<tr><td><code>copernicus:full_width_half_max</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:geometry</code></td><td>Geometry.json</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Defines the footprint of this Item.</td></tr>
<tr><td><code>copernicus:geometry_types</code></td><td>array of string</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>A list of the geometry types present in the dataset.</td></tr>
<tr><td><code>copernicus:grid_code</code></td><td>string</td><td><a href="docs/sources/grid-v1.1.0.md">Grid</a></td><td><strong>REQUIRED</strong>. The identifier for the grid element associated with the Item.</td></tr>
<tr><td><code>copernicus:grid_id</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Grid system the chips are aligned to. See <a href="#grid-ids">Grid IDs</a>.</td></tr>
<tr><td><code>copernicus:histogram</code></td><td>object</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Histogram distribution information of the pixels values in the band.</td></tr>
<tr><td><code>copernicus:incidence_angle</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>The incidence angle is the angle between the vertical (normal) to the intercepting surface and the line of sight back to the satellite at the scene center. Measured in degrees (0-90).</td></tr>
<tr><td><code>copernicus:instrument_configuration_id</code></td><td>integer</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a></td><td>The instrument configuration ID is specific to S1 SAR instrument and refers to the onboard configuration. Each version of it has a specific identifier called "Instrument Configuration ID" (ICID) corresponding to a specific number. For more information, cf. <a href="https://sar-mpc.eu/about/faq/">"What is the instrument configuration ID (ICID) ?"</a></td></tr>
<tr><td><code>copernicus:instrument_mode</code></td><td>string</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a>, <a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Mode of the altimetry instrument used to collect the data.</td></tr>
<tr><td><code>copernicus:instrument_type</code></td><td>string (enum)</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a></td><td>Type of altimetry instrument used to collect the data.</td></tr>
<tr><td><code>copernicus:level</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only <code>L</code>, not <code>Level</code>). See the <a href="#suggested-processing-levels">list of suggested processing levels</a>.</td></tr>
<tr><td><code>copernicus:lineage</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described <a href="https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information">NASA ISO</a>. For example, <code>GRD Post Processing</code> for "GRD" product of Sentinel-1 satellites. <a href="https://commonmark.org/">CommonMark 0.29</a> syntax MAY be used for rich text representation.</td></tr>
<tr><td><code>copernicus:looks_azimuth</code></td><td>integer</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path.</td></tr>
<tr><td><code>copernicus:looks_equivalent_number</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The equivalent number of looks (ENL).</td></tr>
<tr><td><code>copernicus:looks_range</code></td><td>integer</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path.</td></tr>
<tr><td><code>copernicus:mmu</code></td><td>number</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Minimum Mapping Unit - the smallest polygon area represented.</td></tr>
<tr><td><code>copernicus:mmw</code></td><td>number</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Minimal Mapping Width - the smallest real-world width represented as polygon.</td></tr>
<tr><td><code>copernicus:moon_azimuth</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Moon azimuth angle. From the scene center point on the ground, this is the angle between truth north and the moon. Measured clockwise in degrees (0-360).</td></tr>
<tr><td><code>copernicus:moon_elevation</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Moon elevation angle. The angle from the tangent of the scene center point to the moon. Measured from the horizon in degrees (<code>0</code>-<code>90</code>).</td></tr>
<tr><td><code>copernicus:name</code></td><td>string</td><td><a href="docs/sources/region-v0.1.0.md">Region</a></td><td>A human-readable name of the relevant region.</td></tr>
<tr><td><code>copernicus:nominal_track</code></td><td>coordinates</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a></td><td>An array of coordinates used to define the nominal track on the earths surface. This value is recommended ONLY if the item geometry is not representative of the acquisition track.</td></tr>
<tr><td><code>copernicus:observation_direction</code></td><td>string (enum)</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Antenna pointing direction relative to the flight trajectory of the satellite, either <code>left</code> or <code>right</code>.</td></tr>
<tr><td><code>copernicus:off_nadir</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>The angle from the sensor between nadir (straight down) and the scene center. Measured in degrees (0-90).</td></tr>
<tr><td><code>copernicus:offset</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:orbit_cycle</code></td><td>integer</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The number of repeat cycle done by the satellite at the time of the acquisition. <a href="https://ltb.itc.utwente.nl/page/498/concept/81577">Repeat cycle</a> is the time between two successive identical orbits.</td></tr>
<tr><td><code>copernicus:orbit_state</code></td><td>string (enum)</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The state of the orbit. Either <code>ascending</code> or <code>descending</code> for polar orbiting satellites, <code>geostationary</code> for geosynchronous satellites, or <code>crossing</code> when the acquisition spans a polar crossing.</td></tr>
<tr><td><code>copernicus:orbit_state_vectors</code></td><td>map of array</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The state vectors of the satellite at the time of acquisition.</td></tr>
<tr><td><code>copernicus:order_date</code></td><td>string</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td>Indicates the order submission time, in UTC and formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>.</td></tr>
<tr><td><code>copernicus:order_expiration_date</code></td><td>string</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td><strong>DEPRECATED.</strong> Indicates the validity time of the order, in UTC and formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>. Use <a href="https://github.com/stac-extensions/timestamps/"><code>expires</code> from the timestamps extension</a> instead.</td></tr>
<tr><td><code>copernicus:order_id</code></td><td>string</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td>Identifier of the order.</td></tr>
<tr><td><code>copernicus:order_status</code></td><td>string (enum)</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td><strong>REQUIRED</strong>. Describe the status of the ordering. One of the value listed <a href="#orderstatus">here</a></td></tr>
<tr><td><code>copernicus:origin_datetime</code></td><td>string</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a></td><td>Date time of the input data considered to create the item. Example: for PRIP, time of the availability of all CADU data on the CADIP/XBIP</td></tr>
<tr><td><code>copernicus:original_data_type</code></td><td>string (enum)</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Data type before quantization. Uses the same <a href="https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types">data type values</a> as <code>data_type</code>.</td></tr>
<tr><td><code>copernicus:pixel_spacing_azimuth</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type <code>GRD</code>.</td></tr>
<tr><td><code>copernicus:pixel_spacing_range</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type <code>GRD</code>.</td></tr>
<tr><td><code>copernicus:platform_international_designator</code></td><td>string</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The International Designator, also known as COSPAR ID, and NSSDCA ID</td></tr>
<tr><td><code>copernicus:polarizations</code></td><td>array of string</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. Any combination of polarizations.</td></tr>
<tr><td><code>copernicus:primary_datetime</code></td><td>string</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The primary date/time column name.</td></tr>
<tr><td><code>copernicus:primary_geometry</code></td><td>string</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The primary geometry column name.</td></tr>
<tr><td><code>copernicus:product_status</code></td><td>string (enum)</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The lifecycle/status of the product.</td></tr>
<tr><td><code>copernicus:product_type</code></td><td>string</td><td><a href="docs/sources/product-v1.1.0.md">Product</a>, <a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The product type.</td></tr>
<tr><td><code>copernicus:projjson</code></td><td>any</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:publications</code></td><td>array of object</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>List of relevant publications referencing and describing the data.</td></tr>
<tr><td><code>copernicus:published</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was published the first time, in UTC.</td></tr>
<tr><td><code>copernicus:quality_status</code></td><td>string (enum)</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The quality status of the product: <code>nominal</code> or <code>degraded</code>.</td></tr>
<tr><td><code>copernicus:quantization_method</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Quantization method (e.g. <code>linear</code>).</td></tr>
<tr><td><code>copernicus:reference_scale</code></td><td>integer</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Representative fraction denominator (e.g., 50000 for 1:50,000).</td></tr>
<tr><td><code>copernicus:relative_burst</code></td><td>integer</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Identification number that uniquely identifies a burst cycle within each repeat cycle.</td></tr>
<tr><td><code>copernicus:relative_orbit</code></td><td>integer</td><td><a href="docs/sources/sat-v1.2.0.md">Satellite</a></td><td>The relative orbit number at the start of acquisition. When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), use the relative orbit number at the start of the acquisition.</td></tr>
<tr><td><code>copernicus:renders</code></td><td>object</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Dictionary of rendering instructions that can be viewed, keyed by a unique render name.</td></tr>
<tr><td><code>copernicus:resolution_azimuth</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m).</td></tr>
<tr><td><code>copernicus:resolution_range</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m).</td></tr>
<tr><td><code>copernicus:row_count</code></td><td>number</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The number of rows in the dataset.</td></tr>
<tr><td><code>copernicus:sampling</code></td><td>string (enum)</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>One of <code>area</code> or <code>point</code>. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel.</td></tr>
<tr><td><code>copernicus:sampling_rate</code></td><td>number</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a></td><td>Sampling rate of the altimetry instrument in Hz.</td></tr>
<tr><td><code>copernicus:scale</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:season</code></td><td>string (enum)</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP season number. One of <code>S1</code> or <code>S2</code>. See below for details.</td></tr>
<tr><td><code>copernicus:shape</code></td><td>array of integer</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Number of pixels in Y and X directions for the default grid</td></tr>
<tr><td><code>copernicus:snow_cover</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of snow and ice cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:software</code></td><td>map of string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes.</td></tr>
<tr><td><code>copernicus:solar_illumination</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers.</td></tr>
<tr><td><code>copernicus:spatial_resolution</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Average spatial resolution (in meters) of the pixels in the band.</td></tr>
<tr><td><code>copernicus:standard_name</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html">CF Standard Name</a>.</td></tr>
<tr><td><code>copernicus:storage_options</code></td><td>object</td><td><a href="docs/sources/table-v1.3.0.md">Table</a>, <a href="docs/sources/xarray-assets-v1.0.0.md">Xarray Assets</a></td><td><strong>DEPRECATED</strong> Additional keywords for opening the dataset.</td></tr>
<tr><td><code>copernicus:storage_refs</code></td><td>array of string</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that specifies which schemes in copernicus:storage_schemes may be used to access an Asset or Link. Each value must be one of the keys defined in copernicus:storage_schemes.</td></tr>
<tr><td><code>copernicus:storage_schemes</code></td><td>map of objects</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that contains all of the storage schemes used by Assets and Links in the STAC Item, Catalog or Collection.</td></tr>
<tr><td><code>copernicus:stride</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Step between the origins of neighboring chips in pixels as <code>[row_stride, col_stride]</code>. When <code>stride &lt; chip_size</code>, chips overlap.</td></tr>
<tr><td><code>copernicus:sub_parameter</code></td><td>string (enum)</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP sub-parameter acronym. See below for the list of allowed values.</td></tr>
<tr><td><code>copernicus:subdivision</code></td><td>string</td><td><a href="docs/sources/region-v0.1.0.md">Region</a></td><td>ISO 3166-2 codes for identifying the principal subdivisions (e.g., provinces or states) of a country that is primarily covered by the data. Only provide the second part of the ISO 3166-2 code to reduce redundancy.</td></tr>
<tr><td><code>copernicus:sun_azimuth</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Sun azimuth angle. From the scene center point on the ground, this is the angle between truth north and the sun. Measured clockwise in degrees (0-360).</td></tr>
<tr><td><code>copernicus:sun_elevation</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Sun elevation angle. The angle from the tangent of the scene center point to the sun. Measured from the horizon in degrees (<code>-90</code>-<code>90</code>). Negative values indicate the sun is below the horizon, e.g. sun elevation of -10° means the data was captured during <a href="https://www.timeanddate.com/astronomy/different-types-twilight.html">nautical twilight</a>.</td></tr>
<tr><td><code>copernicus:tables</code></td><td>array of object</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td><strong>DEPRECATED</strong> A list of Table Objects (see below).</td></tr>
<tr><td><code>copernicus:temporal_period</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Temporal compositing period as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 duration</a> (e.g. <code>P1Y</code>, <code>P3M</code>).</td></tr>
<tr><td><code>copernicus:themes</code></td><td>array of object</td><td><a href="docs/sources/themes-v1.0.0.md">Themes</a></td><td><strong>REQUIRED.</strong> A knowledge organization system used to classify the STAC entity. Each element is a concept and their respective knowledge organization system / controlled vocabulary.</td></tr>
<tr><td><code>copernicus:timeliness</code></td><td>string</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The average expected timeliness of the product as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 Duration</a>.</td></tr>
<tr><td><code>copernicus:timeliness_category</code></td><td>string</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>A proprietary category identifier for the timeliness of the product.</td></tr>
<tr><td><code>copernicus:transform</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>The affine transformation coefficients for the default grid</td></tr>
<tr><td><code>copernicus:unit</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#units">CF <code>units</code></a>.</td></tr>
<tr><td><code>copernicus:unpublished</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was unpublished, in UTC.</td></tr>
<tr><td><code>copernicus:variables</code></td><td>object</td><td><a href="docs/sources/datacube-v2.3.0.md">Data Cube</a></td><td>Uniquely named variables of the datacube.</td></tr>
<tr><td><code>copernicus:version</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions.</td></tr>
<tr><td><code>copernicus:wkt2</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
</tbody>
</table>

### Asset fields

Fields usable in Assets and Item Asset Definitions.

<table>
<colgroup><col width="24%"><col width="10%"><col width="18%"><col width="48%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>copernicus:acquisition_type</code></td><td>string (enum)</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The acquisition type of the product.</td></tr>
<tr><td><code>copernicus:alternate</code></td><td>object</td><td><a href="docs/sources/alternate-assets-v1.2.0.md">Alternate Assets</a></td><td>Alternate asset locations keyed by provider name, each an Asset Object without href.</td></tr>
<tr><td><code>copernicus:alternate_name</code></td><td>string</td><td><a href="docs/sources/alternate-assets-v1.2.0.md">Alternate Assets</a></td><td>A human readable name for the alternate asset.</td></tr>
<tr><td><code>copernicus:auth_refs</code></td><td>array of string</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link.</td></tr>
<tr><td><code>copernicus:auth_schemes</code></td><td>map of auth_scheme</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>Dictionary of named authentication schemes that guard access to assets or links.</td></tr>
<tr><td><code>copernicus:azimuth</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Viewing azimuth angle. The angle measured from the sub-satellite point (point on the ground below the platform) between the scene center and true north. Measured clockwise from north in degrees (0-360).</td></tr>
<tr><td><code>copernicus:bandwidth</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range bandwidth of the SAR instrument, in gigahertz (GHz), representing the full bandwidth used in range compression and image formation.</td></tr>
<tr><td><code>copernicus:bbox</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Bounding box of the Item in the asset CRS in 2 or 3 dimensions.</td></tr>
<tr><td><code>copernicus:beam_ids</code></td><td>array of string</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Composition of the swath of the SAR acquision referencing the beam identifiers.</td></tr>
<tr><td><code>copernicus:bitfields</code></td><td><a href="#bit_field_object">bit_field_object</a></td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in bit fields in the raster</td></tr>
<tr><td><code>copernicus:bits_per_sample</code></td><td>integer</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the <code>datatype</code>, such as when a 1 bit TIFF is represented as byte.</td></tr>
<tr><td><code>copernicus:cell_methods</code></td><td>array of string/null</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>null]</td></tr>
<tr><td><code>copernicus:center_frequency</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. The center frequency of the radar signal transmitted by the instrument, in gigahertz (GHz).</td></tr>
<tr><td><code>copernicus:center_wavelength</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The center wavelength of the band, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:centroid</code></td><td>object</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Coordinates representing the centroid of the Item (in lat/long)</td></tr>
<tr><td><code>copernicus:chip_size</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Chip size in pixels as <code>[height, width]</code>.</td></tr>
<tr><td><code>copernicus:classes</code></td><td><a href="#class_object">class_object</a></td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in raster or bands</td></tr>
<tr><td><code>copernicus:cloud_cover</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of cloud cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:code</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:columns</code></td><td>array of object</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>A list of Column Objects describing each column.</td></tr>
<tr><td><code>copernicus:common_name</code></td><td>string (enum)</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The name commonly used to refer to the band to make it easier to search for bands across instruments. See the <a href="#common-band-names">list of accepted common names</a>.</td></tr>
<tr><td><code>copernicus:datastrip_id</code></td><td>string</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See <a href="#datastrip-id">Datastrip ID</a> for details.</td></tr>
<tr><td><code>copernicus:datetime</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Processing date and time of the corresponding data formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>, in UTC.</td></tr>
<tr><td><code>copernicus:description</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#long-name">CF <code>long_name</code></a>.</td></tr>
<tr><td><code>copernicus:embedding_dimensions</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding dimensions as an array of sizes, e.g. <code>[768]</code> for a single 768-dimensional vector.</td></tr>
<tr><td><code>copernicus:embedding_type</code></td><td>string (enum)</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding type: <code>pixel</code> or <code>chip</code>.</td></tr>
<tr><td><code>copernicus:expires</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) expires (is not valid any longer), in UTC.</td></tr>
<tr><td><code>copernicus:expression</code></td><td>object</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type <code>processing-expression</code> (see below).</td></tr>
<tr><td><code>copernicus:facility</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name of the facility that produced the data. For example, <code>Copernicus S1 Core Ground Segment - DPA</code> for product of Sentinel-1 satellites.</td></tr>
<tr><td><code>copernicus:frequency_band</code></td><td>string (enum)</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. The common name for the frequency band to make it easier to search for bands across instruments. See section "Common Frequency Band Names" for a list of accepted names.</td></tr>
<tr><td><code>copernicus:full_width_half_max</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:geometry</code></td><td>Geometry.json</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Defines the footprint of this Item.</td></tr>
<tr><td><code>copernicus:geometry_types</code></td><td>array of string</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>A list of the geometry types present in the dataset.</td></tr>
<tr><td><code>copernicus:grid_id</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Grid system the chips are aligned to. See <a href="#grid-ids">Grid IDs</a>.</td></tr>
<tr><td><code>copernicus:histogram</code></td><td>object</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Histogram distribution information of the pixels values in the band.</td></tr>
<tr><td><code>copernicus:incidence_angle</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>The incidence angle is the angle between the vertical (normal) to the intercepting surface and the line of sight back to the satellite at the scene center. Measured in degrees (0-90).</td></tr>
<tr><td><code>copernicus:instrument_mode</code></td><td>string</td><td><a href="docs/sources/altimetry-v0.1.0.md">Altimetry</a>, <a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Mode of the altimetry instrument used to collect the data.</td></tr>
<tr><td><code>copernicus:level</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only <code>L</code>, not <code>Level</code>). See the <a href="#suggested-processing-levels">list of suggested processing levels</a>.</td></tr>
<tr><td><code>copernicus:lineage</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described <a href="https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information">NASA ISO</a>. For example, <code>GRD Post Processing</code> for "GRD" product of Sentinel-1 satellites. <a href="https://commonmark.org/">CommonMark 0.29</a> syntax MAY be used for rich text representation.</td></tr>
<tr><td><code>copernicus:looks_azimuth</code></td><td>integer</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Number of azimuth looks, which is the number of groups of signal samples (looks) parallel to the flight path.</td></tr>
<tr><td><code>copernicus:looks_equivalent_number</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The equivalent number of looks (ENL).</td></tr>
<tr><td><code>copernicus:looks_range</code></td><td>integer</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Number of range looks, which is the number of groups of signal samples (looks) perpendicular to the flight path.</td></tr>
<tr><td><code>copernicus:mmu</code></td><td>number</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Minimum Mapping Unit - the smallest polygon area represented.</td></tr>
<tr><td><code>copernicus:mmw</code></td><td>number</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Minimal Mapping Width - the smallest real-world width represented as polygon.</td></tr>
<tr><td><code>copernicus:moon_azimuth</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Moon azimuth angle. From the scene center point on the ground, this is the angle between truth north and the moon. Measured clockwise in degrees (0-360).</td></tr>
<tr><td><code>copernicus:moon_elevation</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Moon elevation angle. The angle from the tangent of the scene center point to the moon. Measured from the horizon in degrees (<code>0</code>-<code>90</code>).</td></tr>
<tr><td><code>copernicus:observation_direction</code></td><td>string (enum)</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Antenna pointing direction relative to the flight trajectory of the satellite, either <code>left</code> or <code>right</code>.</td></tr>
<tr><td><code>copernicus:off_nadir</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>The angle from the sensor between nadir (straight down) and the scene center. Measured in degrees (0-90).</td></tr>
<tr><td><code>copernicus:offset</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:open_kwargs</code></td><td>object</td><td><a href="docs/sources/xarray-assets-v1.0.0.md">Xarray Assets</a></td><td>Keyword arguments to provide to the xarray opener</td></tr>
<tr><td><code>copernicus:order_date</code></td><td>string</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td>Indicates the order submission time, in UTC and formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>.</td></tr>
<tr><td><code>copernicus:order_expiration_date</code></td><td>string</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td><strong>DEPRECATED.</strong> Indicates the validity time of the order, in UTC and formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>. Use <a href="https://github.com/stac-extensions/timestamps/"><code>expires</code> from the timestamps extension</a> instead.</td></tr>
<tr><td><code>copernicus:order_id</code></td><td>string</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td>Identifier of the order.</td></tr>
<tr><td><code>copernicus:order_status</code></td><td>string (enum)</td><td><a href="docs/sources/order-v1.1.0.md">Order</a></td><td><strong>REQUIRED</strong>. Describe the status of the ordering. One of the value listed <a href="#orderstatus">here</a></td></tr>
<tr><td><code>copernicus:original_data_type</code></td><td>string (enum)</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Data type before quantization. Uses the same <a href="https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types">data type values</a> as <code>data_type</code>.</td></tr>
<tr><td><code>copernicus:pixel_spacing_azimuth</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The azimuth pixel spacing, which is the distance between adjacent pixels parallel to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type <code>GRD</code>.</td></tr>
<tr><td><code>copernicus:pixel_spacing_range</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range pixel spacing, which is the distance between adjacent pixels perpendicular to the flight path, in meters (m). Strongly RECOMMENDED to be specified for products of type <code>GRD</code>.</td></tr>
<tr><td><code>copernicus:polarizations</code></td><td>array of string</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>RECOMMENDED. Any combination of polarizations.</td></tr>
<tr><td><code>copernicus:primary_datetime</code></td><td>string</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The primary date/time column name.</td></tr>
<tr><td><code>copernicus:primary_geometry</code></td><td>string</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The primary geometry column name.</td></tr>
<tr><td><code>copernicus:product_status</code></td><td>string (enum)</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The lifecycle/status of the product.</td></tr>
<tr><td><code>copernicus:product_type</code></td><td>string</td><td><a href="docs/sources/product-v1.1.0.md">Product</a>, <a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The product type.</td></tr>
<tr><td><code>copernicus:projjson</code></td><td>any</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:published</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was published the first time, in UTC.</td></tr>
<tr><td><code>copernicus:quality_status</code></td><td>string (enum)</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The quality status of the product: <code>nominal</code> or <code>degraded</code>.</td></tr>
<tr><td><code>copernicus:quantization_method</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Quantization method (e.g. <code>linear</code>).</td></tr>
<tr><td><code>copernicus:reference_scale</code></td><td>integer</td><td><a href="docs/sources/vector-v0.1.0.md">Vector</a></td><td>Representative fraction denominator (e.g., 50000 for 1:50,000).</td></tr>
<tr><td><code>copernicus:relative_burst</code></td><td>integer</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>Identification number that uniquely identifies a burst cycle within each repeat cycle.</td></tr>
<tr><td><code>copernicus:resolution_azimuth</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The azimuth resolution, which is the maximum ability to distinguish two adjacent targets parallel to the flight path, in meters (m).</td></tr>
<tr><td><code>copernicus:resolution_range</code></td><td>number</td><td><a href="docs/sources/sar-v1.3.2.md">Synthetic Aperture Radar</a></td><td>The range resolution, which is the maximum ability to distinguish two adjacent targets perpendicular to the flight path, in meters (m).</td></tr>
<tr><td><code>copernicus:row_count</code></td><td>number</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>The number of rows in the dataset.</td></tr>
<tr><td><code>copernicus:sampling</code></td><td>string (enum)</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>One of <code>area</code> or <code>point</code>. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel.</td></tr>
<tr><td><code>copernicus:scale</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:season</code></td><td>string (enum)</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP season number. One of <code>S1</code> or <code>S2</code>. See below for details.</td></tr>
<tr><td><code>copernicus:shape</code></td><td>array of integer</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Number of pixels in Y and X directions for the default grid</td></tr>
<tr><td><code>copernicus:snow_cover</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of snow and ice cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:software</code></td><td>map of string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes.</td></tr>
<tr><td><code>copernicus:solar_illumination</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers.</td></tr>
<tr><td><code>copernicus:spatial_resolution</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Average spatial resolution (in meters) of the pixels in the band.</td></tr>
<tr><td><code>copernicus:standard_name</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html">CF Standard Name</a>.</td></tr>
<tr><td><code>copernicus:storage_options</code></td><td>object</td><td><a href="docs/sources/table-v1.3.0.md">Table</a>, <a href="docs/sources/xarray-assets-v1.0.0.md">Xarray Assets</a></td><td><strong>DEPRECATED</strong> Additional keywords for opening the dataset.</td></tr>
<tr><td><code>copernicus:storage_refs</code></td><td>array of string</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that specifies which schemes in copernicus:storage_schemes may be used to access an Asset or Link. Each value must be one of the keys defined in copernicus:storage_schemes.</td></tr>
<tr><td><code>copernicus:storage_schemes</code></td><td>map of objects</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that contains all of the storage schemes used by Assets and Links in the STAC Item, Catalog or Collection.</td></tr>
<tr><td><code>copernicus:stride</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Step between the origins of neighboring chips in pixels as <code>[row_stride, col_stride]</code>. When <code>stride &lt; chip_size</code>, chips overlap.</td></tr>
<tr><td><code>copernicus:sub_parameter</code></td><td>string (enum)</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP sub-parameter acronym. See below for the list of allowed values.</td></tr>
<tr><td><code>copernicus:sun_azimuth</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Sun azimuth angle. From the scene center point on the ground, this is the angle between truth north and the sun. Measured clockwise in degrees (0-360).</td></tr>
<tr><td><code>copernicus:sun_elevation</code></td><td>number</td><td><a href="docs/sources/view-v1.1.0.md">View Geometry</a></td><td>Sun elevation angle. The angle from the tangent of the scene center point to the sun. Measured from the horizon in degrees (<code>-90</code>-<code>90</code>). Negative values indicate the sun is below the horizon, e.g. sun elevation of -10° means the data was captured during <a href="https://www.timeanddate.com/astronomy/different-types-twilight.html">nautical twilight</a>.</td></tr>
<tr><td><code>copernicus:tables</code></td><td>array of object</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td><strong>DEPRECATED</strong> A list of Table Objects (see below).</td></tr>
<tr><td><code>copernicus:temporal_period</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Temporal compositing period as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 duration</a> (e.g. <code>P1Y</code>, <code>P3M</code>).</td></tr>
<tr><td><code>copernicus:timeliness</code></td><td>string</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>The average expected timeliness of the product as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 Duration</a>.</td></tr>
<tr><td><code>copernicus:timeliness_category</code></td><td>string</td><td><a href="docs/sources/product-v1.1.0.md">Product</a></td><td>A proprietary category identifier for the timeliness of the product.</td></tr>
<tr><td><code>copernicus:transform</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>The affine transformation coefficients for the default grid</td></tr>
<tr><td><code>copernicus:unit</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#units">CF <code>units</code></a>.</td></tr>
<tr><td><code>copernicus:unpublished</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was unpublished, in UTC.</td></tr>
<tr><td><code>copernicus:version</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions.</td></tr>
<tr><td><code>copernicus:wkt2</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
</tbody>
</table>

### Link fields

Fields usable in Links and Link Templates.

<table>
<colgroup><col width="24%"><col width="10%"><col width="18%"><col width="48%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>copernicus:auth_refs</code></td><td>array of string</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>The names of authentication schemes (keys of copernicus:auth_schemes) that apply to an asset or link.</td></tr>
<tr><td><code>copernicus:auth_schemes</code></td><td>map of auth_scheme</td><td><a href="docs/sources/authentication-v1.2.0.md">Authentication</a></td><td>Dictionary of named authentication schemes that guard access to assets or links.</td></tr>
<tr><td><code>copernicus:bbox</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Bounding box of the Item in the asset CRS in 2 or 3 dimensions.</td></tr>
<tr><td><code>copernicus:centroid</code></td><td>object</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Coordinates representing the centroid of the Item (in lat/long)</td></tr>
<tr><td><code>copernicus:code</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:expires</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) expires (is not valid any longer), in UTC.</td></tr>
<tr><td><code>copernicus:geometry</code></td><td>Geometry.json</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Defines the footprint of this Item.</td></tr>
<tr><td><code>copernicus:pmtiles_layers</code></td><td>array of string</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The PMTiles layers to display.</td></tr>
<tr><td><code>copernicus:projjson</code></td><td>any</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:published</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was published the first time, in UTC.</td></tr>
<tr><td><code>copernicus:servers</code></td><td>array of string</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The servers to substitute for the {s} variable in the link href.</td></tr>
<tr><td><code>copernicus:shape</code></td><td>array of integer</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Number of pixels in Y and X directions for the default grid</td></tr>
<tr><td><code>copernicus:storage_refs</code></td><td>array of string</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that specifies which schemes in copernicus:storage_schemes may be used to access an Asset or Link. Each value must be one of the keys defined in copernicus:storage_schemes.</td></tr>
<tr><td><code>copernicus:storage_schemes</code></td><td>map of objects</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>A property that contains all of the storage schemes used by Assets and Links in the STAC Item, Catalog or Collection.</td></tr>
<tr><td><code>copernicus:transform</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>The affine transformation coefficients for the default grid</td></tr>
<tr><td><code>copernicus:unpublished</code></td><td>string</td><td><a href="docs/sources/timestamps-v1.1.0.md">Timestamps</a></td><td>Date and time the corresponding data (see below) was unpublished, in UTC.</td></tr>
<tr><td><code>copernicus:wkt2</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:wms_dimensions</code></td><td>object</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>WMS dimensions and their values.</td></tr>
<tr><td><code>copernicus:wms_layers</code></td><td>array of string</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The WMS layers to display.</td></tr>
<tr><td><code>copernicus:wms_styles</code></td><td>array of string</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The WMS styles to apply.</td></tr>
<tr><td><code>copernicus:wms_transparent</code></td><td>boolean</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>Whether the WMS map background is transparent.</td></tr>
<tr><td><code>copernicus:wmts_dimensions</code></td><td>object</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>WMTS dimensions and their values.</td></tr>
<tr><td><code>copernicus:wmts_encoding</code></td><td>string (enum)</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The encoding to use for WMTS requests: <code>rest</code> or <code>kvp</code>.</td></tr>
<tr><td><code>copernicus:wmts_layer</code></td><td>string</td><td><a href="docs/sources/web-map-links-v1.3.0.md">Web Map Links</a></td><td>The WMTS layer identifier.</td></tr>
</tbody>
</table>

### Band fields

Fields usable in Band Objects (`bands` arrays on assets or item properties).

<table>
<colgroup><col width="24%"><col width="10%"><col width="18%"><col width="48%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>copernicus:bbox</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Bounding box of the Item in the asset CRS in 2 or 3 dimensions.</td></tr>
<tr><td><code>copernicus:bitfields</code></td><td><a href="#bit_field_object">bit_field_object</a></td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in bit fields in the raster</td></tr>
<tr><td><code>copernicus:bits_per_sample</code></td><td>integer</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>The actual number of bits used for this band. Normally only present when the number of bits is non-standard for the <code>datatype</code>, such as when a 1 bit TIFF is represented as byte.</td></tr>
<tr><td><code>copernicus:cell_methods</code></td><td>array of string/null</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>null]</td></tr>
<tr><td><code>copernicus:center_wavelength</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The center wavelength of the band, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:centroid</code></td><td>object</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Coordinates representing the centroid of the Item (in lat/long)</td></tr>
<tr><td><code>copernicus:chip_size</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Chip size in pixels as <code>[height, width]</code>.</td></tr>
<tr><td><code>copernicus:classes</code></td><td><a href="#class_object">class_object</a></td><td><a href="docs/sources/classification-v2.0.0.md">Classification</a></td><td>Classes stored in raster or bands</td></tr>
<tr><td><code>copernicus:cloud_cover</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of cloud cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:code</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:common_name</code></td><td>string (enum)</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The name commonly used to refer to the band to make it easier to search for bands across instruments. See the <a href="#common-band-names">list of accepted common names</a>.</td></tr>
<tr><td><code>copernicus:datastrip_id</code></td><td>string</td><td><a href="docs/sources/eopf-v1.2.0.md">EOPF</a>, <a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The identifier of the datastrip, i.e. the part of a datatake that the ground segment processed as one unit. See <a href="#datastrip-id">Datastrip ID</a> for details.</td></tr>
<tr><td><code>copernicus:datetime</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Processing date and time of the corresponding data formatted according to <a href="https://tools.ietf.org/html/rfc3339#section-5.6">RFC 3339, section 5.6</a>, in UTC.</td></tr>
<tr><td><code>copernicus:description</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#long-name">CF <code>long_name</code></a>.</td></tr>
<tr><td><code>copernicus:embedding_dimensions</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding dimensions as an array of sizes, e.g. <code>[768]</code> for a single 768-dimensional vector.</td></tr>
<tr><td><code>copernicus:embedding_type</code></td><td>string (enum)</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td><strong>REQUIRED</strong>. Embedding type: <code>pixel</code> or <code>chip</code>.</td></tr>
<tr><td><code>copernicus:expression</code></td><td>object</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>An expression or processing chain that describes how the data has been processed. Alternatively, you can also link to a processing chain with the relation type <code>processing-expression</code> (see below).</td></tr>
<tr><td><code>copernicus:facility</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name of the facility that produced the data. For example, <code>Copernicus S1 Core Ground Segment - DPA</code> for product of Sentinel-1 satellites.</td></tr>
<tr><td><code>copernicus:full_width_half_max</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Full width at half maximum (FWHM). The width of the band, as measured at half the maximum transmission, in micrometers (μm).</td></tr>
<tr><td><code>copernicus:geometry</code></td><td>Geometry.json</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Defines the footprint of this Item.</td></tr>
<tr><td><code>copernicus:grid_id</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Grid system the chips are aligned to. See <a href="#grid-ids">Grid IDs</a>.</td></tr>
<tr><td><code>copernicus:histogram</code></td><td>object</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Histogram distribution information of the pixels values in the band.</td></tr>
<tr><td><code>copernicus:level</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The name commonly used to refer to the processing level to make it easier to search for product level across collections or items. The short name must be used (only <code>L</code>, not <code>Level</code>). See the <a href="#suggested-processing-levels">list of suggested processing levels</a>.</td></tr>
<tr><td><code>copernicus:lineage</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Lineage Information provided as free text information about the how observations were processed or models that were used to create the resource being described <a href="https://wiki.earthdata.nasa.gov/display/NASAISO/Lineage+Information">NASA ISO</a>. For example, <code>GRD Post Processing</code> for "GRD" product of Sentinel-1 satellites. <a href="https://commonmark.org/">CommonMark 0.29</a> syntax MAY be used for rich text representation.</td></tr>
<tr><td><code>copernicus:offset</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Number to be added to the pixel value (after scaling) to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:original_data_type</code></td><td>string (enum)</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Data type before quantization. Uses the same <a href="https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#data-types">data type values</a> as <code>data_type</code>.</td></tr>
<tr><td><code>copernicus:projjson</code></td><td>any</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
<tr><td><code>copernicus:quantization_method</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Quantization method (e.g. <code>linear</code>).</td></tr>
<tr><td><code>copernicus:sampling</code></td><td>string (enum)</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>One of <code>area</code> or <code>point</code>. Indicates whether a pixel value should be assumed to represent a sampling over the region of the pixel or a point sample at the center of the pixel.</td></tr>
<tr><td><code>copernicus:scale</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Multiplicator factor of the pixel value to transform into the value (i.e. translate digital number to reflectance).</td></tr>
<tr><td><code>copernicus:season</code></td><td>string (enum)</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP season number. One of <code>S1</code> or <code>S2</code>. See below for details.</td></tr>
<tr><td><code>copernicus:shape</code></td><td>array of integer</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>Number of pixels in Y and X directions for the default grid</td></tr>
<tr><td><code>copernicus:snow_cover</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>Estimate of snow and ice cover as a percentage (0-100).</td></tr>
<tr><td><code>copernicus:software</code></td><td>map of string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>A dictionary with name/version for key/value describing one or more applications or libraries that were involved during the production of the data for provenance purposes.</td></tr>
<tr><td><code>copernicus:solar_illumination</code></td><td>number</td><td><a href="docs/sources/eo-v2.0.0.md">Electro-Optical</a></td><td>The solar illumination of the band, as measured at half the maximum transmission, in W/m2/micrometers.</td></tr>
<tr><td><code>copernicus:spatial_resolution</code></td><td>number</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Average spatial resolution (in meters) of the pixels in the band.</td></tr>
<tr><td><code>copernicus:standard_name</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html">CF Standard Name</a>.</td></tr>
<tr><td><code>copernicus:stride</code></td><td>array of integer</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Step between the origins of neighboring chips in pixels as <code>[row_stride, col_stride]</code>. When <code>stride &lt; chip_size</code>, chips overlap.</td></tr>
<tr><td><code>copernicus:sub_parameter</code></td><td>string (enum)</td><td><a href="docs/sources/vpp-v0.1.0.md">Vegetation Phenology and Productivity</a></td><td>The VPP sub-parameter acronym. See below for the list of allowed values.</td></tr>
<tr><td><code>copernicus:temporal_period</code></td><td>string</td><td><a href="docs/sources/embeddings-v1.0.0.md">Embeddings</a></td><td>Temporal compositing period as an <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601 duration</a> (e.g. <code>P1Y</code>, <code>P3M</code>).</td></tr>
<tr><td><code>copernicus:transform</code></td><td>array of number</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>The affine transformation coefficients for the default grid</td></tr>
<tr><td><code>copernicus:unit</code></td><td>string</td><td><a href="docs/sources/cf-v1.0.0.md">Climate and Forecast (CF) Conventions</a></td><td>Corresponds to the <a href="https://cfconventions.org/cf-conventions/cf-conventions.html#units">CF <code>units</code></a>.</td></tr>
<tr><td><code>copernicus:version</code></td><td>string</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>The version of the primary processing software or processing chain that produced the data. For example, this could be the processing baseline for the Sentinel missions.</td></tr>
<tr><td><code>copernicus:wkt2</code></td><td>string or null</td><td><a href="docs/sources/projection-v2.1.0.md">Projection</a></td><td>null</td></tr>
</tbody>
</table>

### Collection and Catalog fields

Fields usable only on Collections and Catalogs (not in Item Properties).

<table>
<colgroup><col width="24%"><col width="10%"><col width="18%"><col width="48%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>copernicus:stats_catalogs</code></td><td>object</td><td><a href="docs/sources/stats-v0.2.0.md">Stats</a></td><td>A lookup of statistics for all child catalogs.</td></tr>
<tr><td><code>copernicus:stats_collections</code></td><td>object</td><td><a href="docs/sources/stats-v0.2.0.md">Stats</a></td><td>A lookup of statistics for all child collections.</td></tr>
<tr><td><code>copernicus:stats_items</code></td><td>object</td><td><a href="docs/sources/stats-v0.2.0.md">Stats</a></td><td>A lookup of statistics for all child items.</td></tr>
</tbody>
</table>

### Nested object fields

Fields that appear inside object-valued `copernicus:` fields (e.g. each entry of the
`copernicus:renders` map, each class in `copernicus:classes`, each variable in
`copernicus:variables`).

<table>
<colgroup><col width="22%"><col width="8%"><col width="13%"><col width="15%"><col width="42%"></colgroup>
<thead>
<tr><th>Field</th><th>Type</th><th>Applies To</th><th>Source Extension(s)</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><strong>Render Object</strong> (<code>copernicus:renders</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:renders/asset_as_band</code></td><td>boolean</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Treat assets in <code>expression</code> as single bands. Required when expression uses multiple assets</td></tr>
<tr><td><code>copernicus:renders/assets</code></td><td>array</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td><strong>REQUIRED</strong>. Array of asset keys <a href="#assets-reference">referencing the assets</a> that are used to make the rendering</td></tr>
<tr><td><code>copernicus:renders/bidx</code></td><td>array</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Band(s) to select from each referenced asset, one entry per position in <code>assets</code> (an asset needing no sub-selection uses an empty array <code>[]</code>). Each selector is either a 1-based band index (matching the GDAL/rio-tiler/titiler convention) or a band name matching the <code>name</code> of a Band Object declared on that asset (via <code>eo:bands</code>, <code>raster:bands</code>, or the STAC <a href="https://github.com/radiantearth/stac-spec/blob/v1.1.0/commons/common-metadata.md#bands">common <code>bands</code></a> construct) — useful since <code>name</code> is not required on a Band Object. See <a href="#band-references">Band references</a>.</td></tr>
<tr><td><code>copernicus:renders/color_formula</code></td><td>string</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td><a href="https://developmentseed.org/titiler/user_guide/rendering/#color-formula">Color formula</a> that must be applied for a raster band</td></tr>
<tr><td><code>copernicus:renders/colormap</code></td><td>object</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td><a href="https://developmentseed.org/titiler/user_guide/rendering/#custom-colormaps">Color map JSON definition</a> that must be applied for a raster band</td></tr>
<tr><td><code>copernicus:renders/colormap_name</code></td><td>string</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Color map identifier that must be applied for a raster band</td></tr>
<tr><td><code>copernicus:renders/expression</code></td><td>string/object/array</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Band arithmetic formula to apply to the referenced assets. The format is defined by the rendering application, e.g. a <a href="https://developmentseed.org/titiler/">TiTiler</a> band math string or a <a href="https://maplibre.org/maplibre-style-spec/expressions/">MapLibre</a> style expression array.</td></tr>
<tr><td><code>copernicus:renders/minmax_zoom</code></td><td>array</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Zoom levels range applicable for the visualization</td></tr>
<tr><td><code>copernicus:renders/nodata</code></td><td>number/string</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Nodata value to use for this render, overriding any nodata value already defined on the referenced assets (e.g. via the <a href="https://github.com/stac-extensions/raster">raster</a> extension). If not set, implementations SHOULD fall back to the asset's own nodata value.</td></tr>
<tr><td><code>copernicus:renders/resampling</code></td><td>string</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Resampling algorithm to apply to the referenced assets. See <a href="https://gdal.org/programs/gdalwarp.html#cmdoption-gdalwarp-r">GDAL resampling algorithm</a> for some examples.</td></tr>
<tr><td><code>copernicus:renders/rescale</code></td><td>array</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>2 dimensions array of delimited Min,Max range per band. If not provided, the data will not be rescaled.</td></tr>
<tr><td><code>copernicus:renders/title</code></td><td>string</td><td><code>copernicus:renders</code> values</td><td><a href="docs/sources/render-v2.1.0.md">Render</a></td><td>Optional title of the rendering</td></tr>
<tr><td><strong>Contact Object</strong> (<code>copernicus:contacts</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:contacts/addresses</code></td><td>array</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Physical location at which contact can be made.</td></tr>
<tr><td><code>copernicus:contacts/contactInstructions</code></td><td>string</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Supplemental instructions on how or when to contact the responsible party.</td></tr>
<tr><td><code>copernicus:contacts/description</code></td><td>string</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Detailed multi-line description to fully explain the STAC entity. <a href="https://commonmark.org/">CommonMark 0.29</a> syntax MAY be used for rich text representation.</td></tr>
<tr><td><code>copernicus:contacts/emails</code></td><td>array</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Email address at which contact can be made.</td></tr>
<tr><td><code>copernicus:contacts/identifier</code></td><td>string</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>A value uniquely identifying a contact.</td></tr>
<tr><td><code>copernicus:contacts/links</code></td><td>array</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Links related to the contact. The link relation should be <code>about</code> and the media type must indicate the content type of the link (e.g. <code>text/html</code> for a company's web page versus <code>text/vcard</code> for a virtual contact file).</td></tr>
<tr><td><code>copernicus:contacts/logo</code></td><td>any</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Graphic identifying a contact. The link relation must be <code>icon</code> and the media type must be an image media type.</td></tr>
<tr><td><code>copernicus:contacts/name</code></td><td>string</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td><strong>REQUIRED if <code>organization</code> is missing</strong>. The name of the responsible person.</td></tr>
<tr><td><code>copernicus:contacts/organization</code></td><td>string</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td><strong>REQUIRED if <code>name</code> is missing</strong>. Organization/affiliation of the contact.</td></tr>
<tr><td><code>copernicus:contacts/phones</code></td><td>array</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>Telephone numbers at which contact can be made.</td></tr>
<tr><td><code>copernicus:contacts/position</code></td><td>string</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>The name of the role or position of the responsible person taken from the organization's formal organizational hierarchy or chart.</td></tr>
<tr><td><code>copernicus:contacts/roles</code></td><td>object</td><td><code>copernicus:contacts</code> values</td><td><a href="docs/sources/contacts-v1.0.1.md">Contacts</a></td><td>The set of named duties, job functions and/or permissions associated with this contact. See <a href="#roles">Roles</a> for recommended values.</td></tr>
<tr><td><strong>Theme Object</strong> (<code>copernicus:themes</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:themes/concepts</code></td><td>array</td><td><code>copernicus:themes</code> values</td><td><a href="docs/sources/themes-v1.0.0.md">Themes</a></td><td><strong>REQUIRED</strong>. One or more entity/concept identifers from this knowledge system.</td></tr>
<tr><td><code>copernicus:themes/scheme</code></td><td>string</td><td><code>copernicus:themes</code> values</td><td><a href="docs/sources/themes-v1.0.0.md">Themes</a></td><td><strong>REQUIRED</strong>. An identifier for the knowledge organization system used. It is recommended that the identifier is a resolvable URI.</td></tr>
<tr><td><strong>Storage Scheme Object</strong> (<code>copernicus:storage_schemes</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:storage_schemes/platform</code></td><td>string</td><td><code>copernicus:storage_schemes</code> values</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td><strong>REQUIRED.</strong> The cloud provider where data is stored as URI or URI template to the API.</td></tr>
<tr><td><code>copernicus:storage_schemes/region</code></td><td>string</td><td><code>copernicus:storage_schemes</code> values</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>The region where the data is stored. Relevant to speed of access and inter region egress costs (as defined by PaaS provider).</td></tr>
<tr><td><code>copernicus:storage_schemes/requester_pays</code></td><td>boolean</td><td><code>copernicus:storage_schemes</code> values</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td>Is the data "requester pays" (<code>true</code>) or is it "data manager/cloud provider pays" (<code>false</code>). Defaults to <code>false</code>.</td></tr>
<tr><td><code>copernicus:storage_schemes/type</code></td><td>string</td><td><code>copernicus:storage_schemes</code> values</td><td><a href="docs/sources/storage-v2.0.0.md">Storage</a></td><td><strong>REQUIRED.</strong> Type identifier for the platform, see below.</td></tr>
<tr><td><strong>Histogram Object</strong> (<code>copernicus:histogram</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:histogram/buckets</code></td><td>array</td><td><code>copernicus:histogram</code> values</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>Array of integer indicating the number of pixels included in the bucket.</td></tr>
<tr><td><code>copernicus:histogram/count</code></td><td>number</td><td><code>copernicus:histogram</code> values</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>number of buckets of the distribution.</td></tr>
<tr><td><code>copernicus:histogram/max</code></td><td>number</td><td><code>copernicus:histogram</code> values</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>minimum value of the distribution. Also the mean value of the last bucket.</td></tr>
<tr><td><code>copernicus:histogram/min</code></td><td>number</td><td><code>copernicus:histogram</code> values</td><td><a href="docs/sources/raster-v2.0.0.md">Raster</a></td><td>minimum value of the distribution. Also the mean value of the first bucket.</td></tr>
<tr><td><strong>Processing Expression Object</strong> (<code>copernicus:expression</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:expression/expression</code></td><td>any</td><td><code>copernicus:expression</code> values</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td>Any data type, depending on the format chosen.</td></tr>
<tr><td><code>copernicus:expression/format</code></td><td>string</td><td><code>copernicus:expression</code> values</td><td><a href="docs/sources/processing-v1.3.0.md">Processing</a></td><td><strong>REQUIRED</strong> The type of the expression that is specified in the <code>expression</code> property.</td></tr>
<tr><td><strong>Publication Object</strong> (<code>copernicus:publications</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:publications/citation</code></td><td>string</td><td><code>copernicus:publications</code> values</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>Citation of a publication referencing the data.</td></tr>
<tr><td><code>copernicus:publications/doi</code></td><td>string</td><td><code>copernicus:publications</code> values</td><td><a href="docs/sources/scientific-v1.0.0.md">Scientific Citation</a></td><td>The DOI of a publication referencing the data. This MUST NOT be a DOIs link.</td></tr>
<tr><td><strong>Column Object</strong> (<code>copernicus:columns</code>)</td><td></td><td></td><td></td><td></td></tr>
<tr><td><code>copernicus:columns/description</code></td><td>string</td><td><code>copernicus:columns</code> values</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>Detailed multi-line description to explain the dimension. CommonMark 0.29 syntax MAY be used for rich text representation.</td></tr>
<tr><td><code>copernicus:columns/name</code></td><td>string</td><td><code>copernicus:columns</code> values</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td><strong>REQUIRED</strong>. The column name.</td></tr>
<tr><td><code>copernicus:columns/type</code></td><td>string</td><td><code>copernicus:columns</code> values</td><td><a href="docs/sources/table-v1.3.0.md">Table</a></td><td>Native data type of the column. If using a file format with a type system (like Parquet), we recommend you use those types.</td></tr>
</tbody>
</table>

## Field mapping

The table below maps the original extension field names to their `copernicus:` equivalents.

<table>
<colgroup><col width="38%"><col width="38%"><col width="24%"></colgroup>
<thead>
<tr><th>Original field</th><th>Copernicus field</th><th>Source</th></tr>
</thead>
<tbody>
<tr><td><code>sat:absolute_orbit</code></td><td><code>copernicus:absolute_orbit</code></td><td>Satellite</td></tr>
<tr><td><code>sat:acquisition_station</code></td><td><code>copernicus:acquisition_station</code></td><td>Satellite</td></tr>
<tr><td><code>product:acquisition_type</code></td><td><code>copernicus:acquisition_type</code></td><td>Product</td></tr>
<tr><td><code>alternate:alternate</code></td><td><code>copernicus:alternate</code></td><td>Alternate Assets</td></tr>
<tr><td><code>alternate:alternate_name</code></td><td><code>copernicus:alternate_name</code></td><td>Alternate Assets</td></tr>
<tr><td><code>sat:anx_datetime</code></td><td><code>copernicus:anx_datetime</code></td><td>Satellite</td></tr>
<tr><td><code>auth:auth_refs</code></td><td><code>copernicus:auth_refs</code></td><td>Authentication</td></tr>
<tr><td><code>auth:auth_schemes</code></td><td><code>copernicus:auth_schemes</code></td><td>Authentication</td></tr>
<tr><td><code>view:azimuth</code></td><td><code>copernicus:azimuth</code></td><td>View Geometry</td></tr>
<tr><td><code>sar:bandwidth</code></td><td><code>copernicus:bandwidth</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>proj:bbox</code></td><td><code>copernicus:bbox</code></td><td>Projection</td></tr>
<tr><td><code>sar:beam_ids</code></td><td><code>copernicus:beam_ids</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>classification:bitfields</code></td><td><code>copernicus:bitfields</code></td><td>Classification</td></tr>
<tr><td><code>raster:bits_per_sample</code></td><td><code>copernicus:bits_per_sample</code></td><td>Raster</td></tr>
<tr><td><code>cf:cell_methods</code></td><td><code>copernicus:cell_methods</code></td><td>Climate and Forecast (CF) Conventions</td></tr>
<tr><td><code>sar:center_frequency</code></td><td><code>copernicus:center_frequency</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>eo:center_wavelength</code></td><td><code>copernicus:center_wavelength</code></td><td>Electro-Optical</td></tr>
<tr><td><code>proj:centroid</code></td><td><code>copernicus:centroid</code></td><td>Projection</td></tr>
<tr><td><code>emb:chip_size</code></td><td><code>copernicus:chip_size</code></td><td>Embeddings</td></tr>
<tr><td><code>sci:citation</code></td><td><code>copernicus:citation</code></td><td>Scientific Citation</td></tr>
<tr><td><code>classification:classes</code></td><td><code>copernicus:classes</code></td><td>Classification</td></tr>
<tr><td><code>eo:cloud_cover</code></td><td><code>copernicus:cloud_cover</code></td><td>Electro-Optical</td></tr>
<tr><td><code>proj:code</code></td><td><code>copernicus:code</code></td><td>Projection</td></tr>
<tr><td><code>table:columns</code></td><td><code>copernicus:columns</code></td><td>Table</td></tr>
<tr><td><code>eo:common_name</code></td><td><code>copernicus:common_name</code></td><td>Electro-Optical</td></tr>
<tr><td><code>contacts:contacts</code></td><td><code>copernicus:contacts</code></td><td>Contacts</td></tr>
<tr><td><code>region:country</code></td><td><code>copernicus:country</code></td><td>Region</td></tr>
<tr><td><code>processing:datastrip_id</code></td><td><code>copernicus:datastrip_id</code></td><td>Processing</td></tr>
<tr><td><code>eopf:datastrip_id</code></td><td><code>copernicus:datastrip_id</code></td><td>EOPF</td></tr>
<tr><td><code>eopf:datatake_id</code></td><td><code>copernicus:datatake_id</code></td><td>EOPF</td></tr>
<tr><td><code>processing:datetime</code></td><td><code>copernicus:datetime</code></td><td>Processing</td></tr>
<tr><td><code>cf:description</code></td><td><code>copernicus:description</code></td><td>Climate and Forecast (CF) Conventions</td></tr>
<tr><td><code>cube:dimensions</code></td><td><code>copernicus:dimensions</code></td><td>Data Cube</td></tr>
<tr><td><code>sci:doi</code></td><td><code>copernicus:doi</code></td><td>Scientific Citation</td></tr>
<tr><td><code>emb:embedding_dimensions</code></td><td><code>copernicus:embedding_dimensions</code></td><td>Embeddings</td></tr>
<tr><td><code>emb:embedding_type</code></td><td><code>copernicus:embedding_type</code></td><td>Embeddings</td></tr>
<tr><td><code>expires</code></td><td><code>copernicus:expires</code></td><td>Timestamps</td></tr>
<tr><td><code>processing:expression</code></td><td><code>copernicus:expression</code></td><td>Processing</td></tr>
<tr><td><code>processing:facility</code></td><td><code>copernicus:facility</code></td><td>Processing</td></tr>
<tr><td><code>sar:frequency_band</code></td><td><code>copernicus:frequency_band</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>eo:full_width_half_max</code></td><td><code>copernicus:full_width_half_max</code></td><td>Electro-Optical</td></tr>
<tr><td><code>proj:geometry</code></td><td><code>copernicus:geometry</code></td><td>Projection</td></tr>
<tr><td><code>vector:geometry_types</code></td><td><code>copernicus:geometry_types</code></td><td>Vector</td></tr>
<tr><td><code>grid:grid_code</code></td><td><code>copernicus:grid_code</code></td><td>Grid</td></tr>
<tr><td><code>emb:grid_id</code></td><td><code>copernicus:grid_id</code></td><td>Embeddings</td></tr>
<tr><td><code>raster:histogram</code></td><td><code>copernicus:histogram</code></td><td>Raster</td></tr>
<tr><td><code>view:incidence_angle</code></td><td><code>copernicus:incidence_angle</code></td><td>View Geometry</td></tr>
<tr><td><code>eopf:instrument_configuration_id</code></td><td><code>copernicus:instrument_configuration_id</code></td><td>EOPF</td></tr>
<tr><td><code>altm:instrument_mode</code></td><td><code>copernicus:instrument_mode</code></td><td>Altimetry</td></tr>
<tr><td><code>sar:instrument_mode</code></td><td><code>copernicus:instrument_mode</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>eopf:instrument_mode</code></td><td><code>copernicus:instrument_mode</code></td><td>EOPF</td></tr>
<tr><td><code>altm:instrument_type</code></td><td><code>copernicus:instrument_type</code></td><td>Altimetry</td></tr>
<tr><td><code>processing:level</code></td><td><code>copernicus:level</code></td><td>Processing</td></tr>
<tr><td><code>processing:lineage</code></td><td><code>copernicus:lineage</code></td><td>Processing</td></tr>
<tr><td><code>sar:looks_azimuth</code></td><td><code>copernicus:looks_azimuth</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>sar:looks_equivalent_number</code></td><td><code>copernicus:looks_equivalent_number</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>sar:looks_range</code></td><td><code>copernicus:looks_range</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>vector:mmu</code></td><td><code>copernicus:mmu</code></td><td>Vector</td></tr>
<tr><td><code>vector:mmw</code></td><td><code>copernicus:mmw</code></td><td>Vector</td></tr>
<tr><td><code>view:moon_azimuth</code></td><td><code>copernicus:moon_azimuth</code></td><td>View Geometry</td></tr>
<tr><td><code>view:moon_elevation</code></td><td><code>copernicus:moon_elevation</code></td><td>View Geometry</td></tr>
<tr><td><code>region:name</code></td><td><code>copernicus:name</code></td><td>Region</td></tr>
<tr><td><code>altm:nominal_track</code></td><td><code>copernicus:nominal_track</code></td><td>Altimetry</td></tr>
<tr><td><code>sar:observation_direction</code></td><td><code>copernicus:observation_direction</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>view:off_nadir</code></td><td><code>copernicus:off_nadir</code></td><td>View Geometry</td></tr>
<tr><td><code>raster:offset</code></td><td><code>copernicus:offset</code></td><td>Raster</td></tr>
<tr><td><code>xarray:open_kwargs</code></td><td><code>copernicus:open_kwargs</code></td><td>Xarray Assets</td></tr>
<tr><td><code>sat:orbit_cycle</code></td><td><code>copernicus:orbit_cycle</code></td><td>Satellite</td></tr>
<tr><td><code>sat:orbit_state</code></td><td><code>copernicus:orbit_state</code></td><td>Satellite</td></tr>
<tr><td><code>sat:orbit_state_vectors</code></td><td><code>copernicus:orbit_state_vectors</code></td><td>Satellite</td></tr>
<tr><td><code>order:order_date</code></td><td><code>copernicus:order_date</code></td><td>Order</td></tr>
<tr><td><code>order:order_expiration_date</code></td><td><code>copernicus:order_expiration_date</code></td><td>Order</td></tr>
<tr><td><code>order:order_id</code></td><td><code>copernicus:order_id</code></td><td>Order</td></tr>
<tr><td><code>order:order_status</code></td><td><code>copernicus:order_status</code></td><td>Order</td></tr>
<tr><td><code>eopf:origin_datetime</code></td><td><code>copernicus:origin_datetime</code></td><td>EOPF</td></tr>
<tr><td><code>emb:original_data_type</code></td><td><code>copernicus:original_data_type</code></td><td>Embeddings</td></tr>
<tr><td><code>sar:pixel_spacing_azimuth</code></td><td><code>copernicus:pixel_spacing_azimuth</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>sar:pixel_spacing_range</code></td><td><code>copernicus:pixel_spacing_range</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>sat:platform_international_designator</code></td><td><code>copernicus:platform_international_designator</code></td><td>Satellite</td></tr>
<tr><td><code>sar:polarizations</code></td><td><code>copernicus:polarizations</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>table:primary_datetime</code></td><td><code>copernicus:primary_datetime</code></td><td>Table</td></tr>
<tr><td><code>table:primary_geometry</code></td><td><code>copernicus:primary_geometry</code></td><td>Table</td></tr>
<tr><td><code>product:product_status</code></td><td><code>copernicus:product_status</code></td><td>Product</td></tr>
<tr><td><code>product:product_type</code></td><td><code>copernicus:product_type</code></td><td>Product</td></tr>
<tr><td><code>sar:product_type</code></td><td><code>copernicus:product_type</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>proj:projjson</code></td><td><code>copernicus:projjson</code></td><td>Projection</td></tr>
<tr><td><code>sci:publications</code></td><td><code>copernicus:publications</code></td><td>Scientific Citation</td></tr>
<tr><td><code>published</code></td><td><code>copernicus:published</code></td><td>Timestamps</td></tr>
<tr><td><code>product:quality_status</code></td><td><code>copernicus:quality_status</code></td><td>Product</td></tr>
<tr><td><code>emb:quantization_method</code></td><td><code>copernicus:quantization_method</code></td><td>Embeddings</td></tr>
<tr><td><code>vector:reference_scale</code></td><td><code>copernicus:reference_scale</code></td><td>Vector</td></tr>
<tr><td><code>sar:relative_burst</code></td><td><code>copernicus:relative_burst</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>sat:relative_orbit</code></td><td><code>copernicus:relative_orbit</code></td><td>Satellite</td></tr>
<tr><td><code>render:renders</code></td><td><code>copernicus:renders</code></td><td>Render</td></tr>
<tr><td><code>sar:resolution_azimuth</code></td><td><code>copernicus:resolution_azimuth</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>sar:resolution_range</code></td><td><code>copernicus:resolution_range</code></td><td>Synthetic Aperture Radar</td></tr>
<tr><td><code>table:row_count</code></td><td><code>copernicus:row_count</code></td><td>Table</td></tr>
<tr><td><code>raster:sampling</code></td><td><code>copernicus:sampling</code></td><td>Raster</td></tr>
<tr><td><code>altm:sampling_rate</code></td><td><code>copernicus:sampling_rate</code></td><td>Altimetry</td></tr>
<tr><td><code>raster:scale</code></td><td><code>copernicus:scale</code></td><td>Raster</td></tr>
<tr><td><code>vpp:season</code></td><td><code>copernicus:season</code></td><td>Vegetation Phenology and Productivity</td></tr>
<tr><td><code>proj:shape</code></td><td><code>copernicus:shape</code></td><td>Projection</td></tr>
<tr><td><code>eo:snow_cover</code></td><td><code>copernicus:snow_cover</code></td><td>Electro-Optical</td></tr>
<tr><td><code>processing:software</code></td><td><code>copernicus:software</code></td><td>Processing</td></tr>
<tr><td><code>eo:solar_illumination</code></td><td><code>copernicus:solar_illumination</code></td><td>Electro-Optical</td></tr>
<tr><td><code>raster:spatial_resolution</code></td><td><code>copernicus:spatial_resolution</code></td><td>Raster</td></tr>
<tr><td><code>cf:standard_name</code></td><td><code>copernicus:standard_name</code></td><td>Climate and Forecast (CF) Conventions</td></tr>
<tr><td><code>stats:stats_catalogs</code></td><td><code>copernicus:stats_catalogs</code></td><td>Stats</td></tr>
<tr><td><code>stats:stats_collections</code></td><td><code>copernicus:stats_collections</code></td><td>Stats</td></tr>
<tr><td><code>stats:stats_items</code></td><td><code>copernicus:stats_items</code></td><td>Stats</td></tr>
<tr><td><code>table:storage_options</code></td><td><code>copernicus:storage_options</code></td><td>Table</td></tr>
<tr><td><code>xarray:storage_options</code></td><td><code>copernicus:storage_options</code></td><td>Xarray Assets</td></tr>
<tr><td><code>storage:storage_refs</code></td><td><code>copernicus:storage_refs</code></td><td>Storage</td></tr>
<tr><td><code>storage:storage_schemes</code></td><td><code>copernicus:storage_schemes</code></td><td>Storage</td></tr>
<tr><td><code>emb:stride</code></td><td><code>copernicus:stride</code></td><td>Embeddings</td></tr>
<tr><td><code>vpp:sub_parameter</code></td><td><code>copernicus:sub_parameter</code></td><td>Vegetation Phenology and Productivity</td></tr>
<tr><td><code>region:subdivision</code></td><td><code>copernicus:subdivision</code></td><td>Region</td></tr>
<tr><td><code>view:sun_azimuth</code></td><td><code>copernicus:sun_azimuth</code></td><td>View Geometry</td></tr>
<tr><td><code>view:sun_elevation</code></td><td><code>copernicus:sun_elevation</code></td><td>View Geometry</td></tr>
<tr><td><code>table:tables</code></td><td><code>copernicus:tables</code></td><td>Table</td></tr>
<tr><td><code>emb:temporal_period</code></td><td><code>copernicus:temporal_period</code></td><td>Embeddings</td></tr>
<tr><td><code>themes:themes</code></td><td><code>copernicus:themes</code></td><td>Themes</td></tr>
<tr><td><code>product:timeliness</code></td><td><code>copernicus:timeliness</code></td><td>Product</td></tr>
<tr><td><code>product:timeliness_category</code></td><td><code>copernicus:timeliness_category</code></td><td>Product</td></tr>
<tr><td><code>proj:transform</code></td><td><code>copernicus:transform</code></td><td>Projection</td></tr>
<tr><td><code>cf:unit</code></td><td><code>copernicus:unit</code></td><td>Climate and Forecast (CF) Conventions</td></tr>
<tr><td><code>unpublished</code></td><td><code>copernicus:unpublished</code></td><td>Timestamps</td></tr>
<tr><td><code>cube:variables</code></td><td><code>copernicus:variables</code></td><td>Data Cube</td></tr>
<tr><td><code>processing:version</code></td><td><code>copernicus:version</code></td><td>Processing</td></tr>
<tr><td><code>proj:wkt2</code></td><td><code>copernicus:wkt2</code></td><td>Projection</td></tr>
</tbody>
</table>

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
