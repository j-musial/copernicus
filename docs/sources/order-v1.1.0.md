<!--
Harvested from https://github.com/stac-extensions/order (v1.1.0) on 2026-11-13 for the
Copernicus STAC Extension. Field names have been rewritten to their
copernicus: equivalents — see the field mapping table in the main README.
Upstream license: Apache-2.0.
-->

# Order (v1.1.0)

- **Source repository:** [stac-extensions/order](https://github.com/stac-extensions/order)
- **Upstream version:** v1.1.0
- **Upstream schema:** <https://stac-extensions.github.io/order/v1.1.0/schema.json#>
- **License:** Apache-2.0

The following is the specification text of the *Order* extension as merged into
the Copernicus STAC Extension. All field names below use the `copernicus:` prefix.

---

- **Title:** Order
- **Identifier:** <https://stac-extensions.github.io/order/v1.1.0/schema.json>
- **Field Name Prefix:** order
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @emmanuelmathot

This document explains the Order Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This extension allows assets ordering management within STAC specification.
In the context of this extension, the term "order" refers to a request for data to be
delivered, served, or otherwise made available (e.g., after a purchase).

- Examples:
  - [Item example](https://github.com/stac-extensions/order/blob/main/examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](https://github.com/stac-extensions/order/blob/main/examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](https://github.com/stac-extensions/order/blob/main/json-schema/schema.json)
- [Changelog](https://github.com/stac-extensions/order/blob/main/CHANGELOG.md)

### Ordering Scenarios

This extension can be used to enable several ordering scenarios. Some examples are described in the following sections

#### Activating Offline Assets

This scenario describes the "activation" of an *offline* product at the provider storage. 
It uses the [storage extension](https://github.com/stac-extensions/storage) to describe storage information necessary for the ordering status.
The following diagram describe the states transition of the asset in a STAC Item.

![Activating Offline Assets](https://github.com/stac-extensions/order/blob/main/images/diagrams/activate-offline/activate-offline.svg)

#### Data Ordering per user

This scenario describes the "ordering" of data product by a free or commercial provider.
This use case is based on a per-user exchange with the provider for an individual service.
The order information is not stored as a metadata of the Item but in the ordering information of the user request.

![Data Ordering per user](https://github.com/stac-extensions/order/blob/main/images/diagrams/ordering-paying/ordering-paying.svg)

### Fields

The fields in the table below can be used in these parts of STAC documents:
- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name            | Type     | Description                                                                                     |
| --------------------- | -------- | ----------------------------------------------------------------------------------------------- |
| copernicus:order_status          | string   | **REQUIRED**. Describe the status of the ordering. One of the value listed [here](#orderstatus) |
| copernicus:order_id              | string   | Identifier of the order.                                                                        |
| copernicus:order_date            | string   | Indicates the order submission time, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| copernicus:order_expiration_date | string   | **DEPRECATED.** Indicates the validity time of the order, in UTC and formatted according to [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Use [`expires` from the timestamps extension](https://github.com/stac-extensions/timestamps/) instead. |

These fields have different meaning depending on where they are used.
When used as an Item properties or top-level Collection field, they refer to an order of all data referenced in the Item or Collection, 
which may include the metadata itself.
When used in an Asset Object, the order refer to the particular data asset linked to in the Asset Object.

#### Additional Field Information

##### copernicus:order_status

The main field describing the order status

- `orderable`: The item or asset is orderable via the provider scenario.
- `ordered`: The item or asset is ordered and the provider is preparing to make it available.
- `pending`: The item or asset is ordered but wait for an activation before being able for shipping.
- `shipping`: The item or asset order are being processed by the provider to provide you with the asset(s).
- `succeeded`: The provider has delivered your order and asset(s) are available.
- `failed`: The provider is not able to deliver the order.
- `canceled`: The order has been canceled.

The State diagram below shows the item or asset `copernicus:order_status` lifecycle.

![Order Lifecycle](https://github.com/stac-extensions/order/blob/main/images/diagrams/order-lifecycle/order-lifecycle.svg)

##### Timestamps

The [timestamps extension](https://github.com/stac-extensions/timestamps/) and the fields
[`created` and `updated` from common metadata](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#date-and-time)
can be useful addition, usually used in the Item Properties and Collections, sometimes also in the Assets:

- Set `copernicus:order_date` once the status switches to `ordered` (i.e. when the user submits the order).
- Set `created` once the metadata files gets created, usually when the status is `ordered` or `shipping`.
- Set `published` once the order has `succeeded`.
- Set the `expires` field when the order has `succeeded` and your order is meant to expire.
- Update `updated` on each change of `copernicus:order_status` and/or whenever an additional asset has been added.

### Relation types

The following types should be used as applicable `rel` types in the
[Link Object](https://github.com/radiantearth/stac-spec/tree/master/item-spec/item-spec.md#link-object).

| Type  | Description                                                                                                   |
| ----- | ------------------------------------------------------------------------------------------------------------- |
| order | This link points to a document describing further the order (e.g. terms and conditions of the Item provider.) |
