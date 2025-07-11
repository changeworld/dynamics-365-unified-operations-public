---
title: Product data entities 
description: Learn about the different entities that can be used to import and export product data, including an outline on product-related data entities. 
author: sgmsft
ms.author: shwgarg
ms.topic: article
ms.date: 06/23/2025
ms.custom: bap-template
ms.reviewer: kamaybac
ms.search.form:
---

# Product data entities

[!include [banner](../includes/banner.md)]

To import and export product data, you must use data entities. Learn more at [Configuration data and data migration in Dynamics 365 implementation projects](/dynamics365/guidance/implementation-guide/data-management-configuration-data-migration).

## Product-related data entities

The following table provides details about the product-related data entities and describes the purpose of each. Learn more in [Built-in entities](/dynamics365/fin-ops-core/dev-itpro/data-entities/data-entities#built-in-entities).

| Entity | Application Object Tree (AOT) name (type) | Notes |
|--------|-------------------------------------------|-------|
| Products V2 | `EcoResProductV2Entity` | This entity is used to import and export shared products-distinct products and product masters. It allows for updates. It doesn't support set-based SQL operations. It's enabled for Open Data Protocol (OData). |
| Released products V2 | `EcoResReleasedProductV2Entity` | This entity is used to import and export released products-distinct products and product masters. It allows for updates. It requires that the shared product is already created. When a new released product is imported, a release of the shared product occurs. There are also separate entities that can be used to import and export released product masters and released distinct variants. This entity doesn't support set-based SQL operations or delete operations. It's enabled for OData. |
| Released product creation V2 | `EcoResReleasedProductCreationV2Entity` | This entity is used to import shared products and released products in one step. Although it supports exports, we don't recommend using it for exports because the purpose of the entity is product creation. It doesn't support updates. It supports a limited set of fields (fields that are available in the product creation dialog box). It doesn't support set-based SQL operations. It isn't exposed through OData. |
| Product variants | `EcoResProductVariantV2Entity` | This entity is used to import and export shared product variants. It allows for updates. It requires that dimension values are already created. The integration key is the product master plus product dimensions. This entity doesn't support set-based SQL operations. It's enabled for OData. It supports delete operations. It can't be extended through the addition of new product dimensions. |
| Product variants by product number identification | `EcoResProductNumberIdentifiedProductVariantEntity` | This entity is used to import and export shared product variants. It allows for updates. It requires that dimension values are already created. The integration key is the product number (whereas the integration key for the **Product variants** entity is the product master plus product dimensions). |
| Released product variants | `EcoResReleasedProductVariantV2Entity` | This entity is used to import and export released product variants. It allows for updates. It requires that shared product variants already be created. When a new released product variant is imported, a release of the shared product variant occurs. This entity doesn't support set-based SQL operations. It's enabled for OData. Although it supports delete operations, doing so currently causes data corruption because of a bug in the current platform. This entity can't be extended through the addition of new product dimensions. This entity doesn't support deletion of global products and variants. |
| Released product variants by product number identification | `EcoResProductNumberIdentifiedReleasedProductVariantEntity` | This entity resembles the **Released product variants** entity, but the integration key is the product number instead of the product master plus product dimensions. It can be extended through the addition of new product dimensions. |
| Sellable released products | `EcoResSellableReleasedProductEntity` | This entity is used to export only sellable products. Sellable products are products that have the information that they require in order to be used in a sales order. The same rules apply when a product is validated by using the **Validate** function on the **Released products** page. |
| Released Distinct products V2 | `EcoResDistinctProductEntity` | This entity is used for distinct products. Those distinct products can be products, subtype products, and product variants. This entity is enabled for OData but not for data management. |
| Released products masters V2 | `EcoResProductMasterV2Entity` | This entity is used for product masters. It's enabled for OData but not for data management. |
|  Item - barcodes V3 | `EcoResProductBarcodeV3Entity` | This entity is used to export products and bar codes. This entity doesn't allow change tracking, updates, or deletes. To use change tracking, updates, or deletes on bar codes, use the **Item - barcode association** entity. |
| Item - barcode association | `EcoResProductBarcodeAssociationEntity` | This entity is used to export products and bar codes. It allows change tracking, updates, and deletes. Its entity key is `AssociationID`, which creates the association between the bar code and the product. To add support for this key, the table `InventitemBarcodeAssociation` is populated for existing item bar code data when you turn on the feature. The table is populated using a batch job and if your bar code table has a large number of records, it could take significant time to run the batch job. Therefore, we recommend that you plan to enable the feature (and therefore run the batch job) at a time that fits your business schedule. |
| Product lifecycle states | `EcoResProductLifecycleStateEntity` | This entity is used to import and export the different product lifecycle states that can be assigned to a product. |

> [!NOTE]
> You can use the **Released Products V2** data entity to import products into the system only if the shared product has already been created. Otherwise, to import products into the system, you must use the **Product creation** data entity.

## Next steps

- [Data management overview](../../fin-ops-core/dev-itpro/data-entities/data-entities-data-packages.md)

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
