<!--
Harvested from https://github.com/CS-SI/eopf-stac-extension (v1.2.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# EOPF (v1.2.0)

- **Source repository:** [CS-SI/eopf-stac-extension](https://github.com/CS-SI/eopf-stac-extension)
- **Upstream version:** v1.2.0
- **Upstream schema:** <https://cs-si.github.io/eopf-stac-extension/v1.2.0/schema.json>
- **License:** Apache-2.0

The following is the specification text of the *EOPF* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Earth Observation Processing Framework
- **Identifier:** <https://cs-si.github.io/eopf-stac-extension/v1.2.0/schema.json>
- **Field Name Prefix:** eopf
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: CS Group France
- **History:** Proposal in preparation

This document explains the fields of the EOPF extension to the
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

EOPF is the framework of Copernicus Sentinel data processors under development by ESA.
See [EOPF site](https://eopf.copernicus.eu/) for context.

It is strongly recommended to use the other STAC extensions eo, view, processing, sat and sci with the eopf extension.

### Item Properties or Asset Fields

| Field Name               | Type                                                   | Description                      |
| ------------------------ | ------------------------------------------------------ | -------------------------------- |
| copernicus:datastrip_id       | string                                                  | Datastrip identification (specific to Sentinel-2). Example: S2A_OPER_MSI_L2A_DS_2APS_20240308T143352_S20240308T101546_N05.10 |
| copernicus:datatake_id        | string                                                  | Datatake identification. Examples: for S1, datatake_id = 12032; for S2, datatake_id = GS2A_20231215T103431_044292_N05.10     |
| copernicus:instrument_configuration_id    | integer                                     | The instrument configuration ID is specific to S1 SAR instrument and refers to the onboard configuration. Each version of it has a specific identifier called "Instrument Configuration ID" (ICID) corresponding to a specific number. For more information, cf. ["What is the instrument configuration ID (ICID) ?"](https://sar-mpc.eu/about/faq/) |
| copernicus:instrument_mode     | string                                                 | Instrument_mode (specific to Sentinel-2). Supports all datatake_type values: INS-NOBS, INS-EOBS, INS-DASC, INS-ABSR, INS-VIC, INS-RAW, INS-TST, INS-NOBD, INS-ABSD, INS-DASD, INS-VICD |
| copernicus:origin_datetime     | datetime                                               | Date time of the input data considered to create the item. Example: for PRIP, time of the availability of all CADU data on the CADIP/XBIP                             |
