<!--
Harvested from https://github.com/stac-extensions/contacts (v1.0.1) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Contacts (v1.0.1)

- **Source repository:** [stac-extensions/contacts](https://github.com/stac-extensions/contacts)
- **Upstream version:** v1.0.1
- **Upstream schema:** <https://stac-extensions.github.io/contacts/v1.0.1/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Contacts* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Contacts
- **Identifier:** <https://stac-extensions.github.io/copernicus:contacts/v1.0.1/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Contacts Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
It allows to add extensive information about persons and organizations related to the (meta)data.
The extension is based on [OGC API - Records](https://ogcapi.ogc.org/records/),
which itself is inspired by [ISO 19115](https://www.iso.org/standard/53798.html).

- Examples:
  - [Collection example](https://github.com/stac-extensions/copernicus:contacts/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/copernicus:contacts/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/copernicus:contacts/blob/main/CHANGELOG.md)

### Fields

The fields in the table below can be used in these parts of STAC documents:

- [x] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name | Type                                 | Description |
| ---------- | ------------------------------------ | ----------- |
| copernicus:contacts   | \[[Contact Object](#contact-object)] | **REQUIRED.** A list of copernicus:contacts qualified by their role. |

#### Contact Object

The Contact Object aimed at the identification of, and means of communication with, a person responsible for the resource.
Either the field `name` or the field `organization` must be provided (or both).

| Field Name          | Type                                 | Description |
| ------------------- | ------------------------------------ | ----------- |
| name                | string                               | **REQUIRED if `organization` is missing**. The name of the responsible person. |
| organization        | string                               | **REQUIRED if `name` is missing**. Organization/affiliation of the contact. |
| identifier          | string                               | A value uniquely identifying a contact. |
| position            | string                               | The name of the role or position of the responsible person taken from the organization's formal organizational hierarchy or chart. |
| description         | string                               | Detailed multi-line description to fully explain the STAC entity. [CommonMark 0.29](https://commonmark.org/) syntax MAY be used for rich text representation. |
| logo                | [Link Object](#link-object)          | Graphic identifying a contact. The link relation must be `icon` and the media type must be an image media type. |
| phones              | \[[Info Object](#info-object)]       | Telephone numbers at which contact can be made. |
| emails              | \[[Info Object](#info-object)]       | Email address at which contact can be made. |
| addresses           | \[[Address Object](#address-object)] | Physical location at which contact can be made. |
| links               | \[[Link Object](#link-object)\]      | Links related to the contact. The link relation should be `about` and the media type must indicate the content type of the link (e.g. `text/html` for a company's web page versus `text/vcard` for a virtual contact file). |
| contactInstructions | string                               | Supplemental instructions on how or when to contact the responsible party. |
| roles               | \[string]                            | The set of named duties, job functions and/or permissions associated with this contact. See [Roles](#roles) for recommended values. |

OGC API - Records also defines an additional property `hoursOfService` which is omitted from this extension
for simplicity. If you need to add the hours of service to your contact object, it is recommended to follow
[the schema that OGC API - Records defines](https://github.com/opengeospatial/ogcapi-records/blob/master/core/openapi/schemas/contact.yaml).

##### Roles

The roles of a contact describe the duties, job functions and/or permissions of the contact in relation to the resource.
The roles are not restricted to a fixed list of values, so data providers can use any role that fits their use case,
for example `developer`, `administrator` or `support`.

To improve interoperability, it is recommended to use the following role codes from
[ISO 19115-1](https://www.iso.org/standard/53798.html) (`CI_RoleCode`) where applicable:

| Role                  | Description |
| --------------------- | ----------- |
| resourceProvider      | Party that supplies the resource. |
| custodian             | Party that accepts accountability and responsibility for the resource and ensures appropriate care and maintenance of the resource. |
| owner                 | Party that owns the resource. |
| user                  | Party who uses the resource. |
| distributor           | Party who distributes the resource. |
| originator            | Party who created the resource. |
| pointOfContact        | Party who can be contacted for acquiring knowledge about or acquisition of the resource. |
| principalInvestigator | Key party responsible for gathering information and conducting research. |
| processor             | Party who has processed the data in a manner such that the resource has been modified. |
| publisher             | Party who published the resource. |
| author                | Party who authored the resource. |
| sponsor               | Party who speaks for the resource. |
| coAuthor              | Party who jointly authors the resource. |
| collaborator          | Party who assists with the generation of the resource other than the principal investigator. |
| editor                | Party who reviewed or modified the resource to improve the content. |
| mediator              | A class of entity that mediates access to the resource and for whom the resource is intended or useful. |
| rightsHolder          | Party owning or managing rights over the resource. |
| contributor           | Party contributing to the resource. |
| funder                | Party providing monetary support for the resource. |
| stakeholder           | Party who has an interest in the resource or the use of the resource. |

The roles defined for the [Provider Object](https://github.com/radiantearth/stac-spec/blob/master/commons/common-metadata.md#roles)
in STAC (`licensor`, `producer`, `processor` and `host`) can also be used.

#### Info Object

Gives contact information for and their "roles".

Currently, this object can be used in two place:

1. Phone numbers
   - Pattern for the value: `^+[1-9]{1}[0-9]{3,14}$`.
   - Potential roles could be `home`, `work`, `fax`, etc.
2. Email addresses
   - Must be a valid email address according to
     [RFC 5321, section 4.1.2](https://datatracker.ietf.org/doc/html/rfc5321#section-4.1.2).
   - Potential roles could be `home`, `work`, etc.

| Field Name | Type      | Description |
| ---------- | --------- | ----------- |
| value      | string    | **REQUIRED**. The actual contact information, depending on the context for example the actual phone number or the email address. |
| roles      | \[string] | The type(s) of this contact information, e.g. whether it's at work or at home. |

#### Address Object

Physical location at which contact can be made.

| Field Name         | Type      | Description |
| ------------------ | --------- | ----------- |
| deliveryPoint      | \[string] | Address lines for the location, for example a street name and a house number. |
| city               | string    | City for the location. |
| administrativeArea | string    | State or province of the location. |
| postalCode         | string    | ZIP or other postal code. |
| country            | string    | Country of the physical address. Could be a free-form country name or an [ISO 3166-1 alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements). |
| roles              | \[string] | The type(s) of this address, e.g. `office`, `home`, etc. |

#### Link Object

This object describes a relationship with another entity.

| Field Name | Type   | Description |
| ---------- | ------ | ----------- |
| href       | string | **REQUIRED.** The actual link in the format of an URL. Relative and absolute links are both allowed. |
| rel        | string | **REQUIRED.** Relationship between the current document and the linked document. |
| type       | string | Media type of the referenced entity. |
| title      | string | A human readable title to be used in rendered displays of the link. |
