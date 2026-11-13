<!--
Harvested from https://github.com/stac-extensions/sat (v1.2.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Satellite (v1.2.0)

- **Source repository:** [stac-extensions/sat](https://github.com/stac-extensions/sat)
- **Upstream version:** v1.2.0
- **Upstream schema:** <https://stac-extensions.github.io/sat/v1.2.0/schema.json>
- **License:** Apache-2.0

The following is the specification text of the *Satellite* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

![Satellite Extension](https://github.com/stac-extensions/sat/blob/main/stac-sat-extension.png)

- **Title:** Satellite
- **Identifier:** <https://stac-extensions.github.io/sat/v1.2.0/schema.json>
- **Field Name Prefix:** sat
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Stable
- **Owner**: @emmanuelmathot
- **History**: [Prior to March 2, 2021](https://github.com/radiantearth/stac-spec/commits/v1.0.0-rc.1/extensions/sat)

This document explains the Satellite Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
It adds metadata related to a satellite that carries an instrument for collecting data.
It will often be combined with other extensions that describe the actual data, such as the [EO](https://github.com/radiantearth/stac-spec/tree/master/extensions/eo) or 
[SAR](https://github.com/stac-extensions/sar) extensions.

- Examples:
  - [example-landsat8.json](https://github.com/stac-extensions/sat/blob/main/examples/example-landsat8.json): Shows the basic usage of the extension in a STAC Item
  - [example-sentinel1.json](https://github.com/stac-extensions/sat/blob/main/examples/example-sentinel1.json): Shows the more advanced usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/sat/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/sat/blob/main/CHANGELOG.md)

### Item Properties

| Field Name                            | Type                   | Description                                                                                                                                                                                             |
| ------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| copernicus:platform_international_designator | string                 | The International Designator, also known as COSPAR ID, and NSSDCA ID                                                                                                                                    |
| copernicus:orbit_state                       | string                 | The state of the orbit. Either `ascending` or `descending` for polar orbiting satellites, `geostationary` for geosynchronous satellites, or `crossing` when the acquisition spans a polar crossing.     |
| copernicus:absolute_orbit                    | integer                | The absolute orbit number at the start of acquisition.                                                                                                                                                  |
| copernicus:relative_orbit                    | integer                | The relative orbit number at the start of acquisition.                                                                                                                                                  |
| copernicus:orbit_cycle                       | integer                | The number of repeat cycle done by the satellite at the time of the acquisition. [Repeat cycle](https://ltb.itc.utwente.nl/page/498/concept/81577) is the time between two successive identical orbits. |
| copernicus:orbit_state_vectors               | Map<string, \[number]> | The state vectors of the satellite at the time of acquisition.                                                                                                                                          |
| copernicus:anx_datetime                      | string                 | The [Ascending Node](https://en.wikipedia.org/wiki/Orbital_node) Crossing (ANX) time, in UTC. It is formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).    |
| copernicus:acquisition_station               | string                 | The acquisition station (ground station) where the satellite data was downlinked. Equivalent to `eop:acquisition_station` in OGC 10-157r4 and OGC 17-003r2.                                             |

*At least one of the fields must be specified.*

#### Additional Field Information

##### copernicus:platform_international_designator

The [International Designator](https://en.wikipedia.org/wiki/International_Designator), also known as COSPAR ID, and NSSDCA ID 
and is an international identifier assigned to artificial objects in space.

##### copernicus:orbit_state

Indicates the type and current state of orbit. Satellites are either geosynchronous in which case they have one state:
`geostationary`, or they are sun synchronous (i.e., polar orbiting satellites) in which case they are either `ascending` or
`descending`. For sun synchronous satellites it is daytime during one of these states, and nighttime during the other.
If the acquisition spans a polar crossing (i.e., the satellite transitions between ascending and descending during the
acquisition), the value `crossing` shall be used.

##### copernicus:absolute_orbit

A count of orbits from 1 to the number of orbits made in the total satellite lifecycle. In mission planning and tasking, the
absolute orbit may be used as a reference in the non systematic acquisition missions. The resulting Item can be tagged with the
absolute orbit and thus searchable as such. In the case of orbital changes during the mission modifying the ground track and
thus the repeat cycle and thus the number or relative orbits, the combination of cycle and relative orbit is not sufficient to
derive an absolute orbit.

When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), the convention is to use the
absolute orbit number at the start of the acquisition. This situation can occur, for example, in consolidated altimetry
products such as Sentinel-3.

##### copernicus:relative_orbit

A count of orbits from 1 to the number of orbits contained in a repeat cycle, where relative orbit 1 starts from a specific
reference location of the sub-satellite point (the point on the earth directly below the satellite). It resets to 1 when the
sub-satellite point revisits the reference location.

When the orbit changes during data acquisition (i.e., the acquisition spans multiple orbits), the convention is to use the
relative orbit number at the start of the acquisition. This situation can occur, for example, in consolidated altimetry
products such as Sentinel-3.

##### copernicus:anx_datetime

The UTC time when the satellite crosses the [Ascending Node](https://en.wikipedia.org/wiki/Orbital_node). For geocentric and 
heliocentric orbits, the ascending node (or north node) is where the orbiting object moves north through the plane of 
reference. Used to quickly compute orbital parameters without having to download the product. For instance to compute on the 
fly a baseline between 2 satellite acquisition, to find the best candidate in the archive from a post-disaster event (e.g 
earthquake) scene acquisition for a DInSAR processing.

##### copernicus:orbit_cycle

The repeat cycle of the satellite. The repeat cycle is the number of orbits required for the satellite to return to the same
position in its orbit. It is used to determine the relative orbit number. For instance, a satellite with a 16-day repeat cycle
will have 16 relative orbits.

##### copernicus:orbit_state_vectors

The state vectors of the satellite at the time of acquisition. The state vectors are a set of parameters that describe the
position and velocity of the satellite at a given time. The state vectors are used to compute the position of the satellite
at any time during the acquisition. 
The state vectors are usually provided in the [ECI](https://en.wikipedia.org/wiki/Earth-centered_inertial) frame.
The field is a map where the key is the time of the state vector and the value is an array of 6 elements (optional 9).
The first 3 elements are the position of the satellite in meters and the last 3 elements are the velocity of the satellite in meters per second.
The optional 3 additional elements are the acceleration of the satellite in meters per second squared.

Example:

```json
{
  "copernicus:orbit_state_vectors": {
    "2015-03-05T05:19:40.103Z": [
      5082939.4189831074,
      1595651.7369050409,
      4648033.5588545678,
      5173.8779329387489,
      -269.5432365485845,
      -5550.246440359806
    ],
    "2015-03-05T05:19:45.449Z": [
      5110519.0376543682,
      1594174.328112772,
      4618284.7202579351,
      5143.1200754073143,
      -283.12343661734587,
      -5578.2160610647188
    ],
    "2015-03-05T05:19:50.449Z": [
      5136162.3887853986,
      1592727.024757518,
      4590328.5904560406,
      5114.1961953273549,
      -295.79384304587683,
      -5604.2108611458289
    ]
  }
}
```

It is recommended that the state vectors are provided in a separate file and referenced as a link with relationship type `sat:osv`.
The file should correspond to the example above.

##### copernicus:acquisition_station

The ground station where the satellite data was downlinked. This information is crucial for data lineage and provenance tracking, 
as it identifies the first point of data reception on Earth. In the context of Earth Observation missions, this corresponds to the 
`eop:acquisitionStation` in OGC standards (10-157r4 and 17-003r2). This field can be used for filtering datasets based on the 
ground station used for downlinking, which can be relevant for certain processing workflows or quality assessments.

### Relation types

The following types should be used as applicable `rel` types in the
[Link Object](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#link-object).

| Type    | Description                                        |
| ------- | -------------------------------------------------- |
| sat:osv | Link to a file containing the orbit state vectors. |
