---
title: Costing versions overview
description: Learn about costing versions, how to maintain them, and the types of data that you can include in them, with an outline on standard or planned costs.
author: prasungoel
ms.author: prasungoel
ms.reviewer: kamaybac
ms.search.form: BOMCalcDialog, BOMCalcTable, CostingVersion
ms.topic: overview
ms.date: 01/30/2025
ms.custom: 
  - bap-template
---

# Costing versions overview

[!include [banner](../includes/banner.md)]

This article provides information about costing versions, how to maintain them, and the types of data that you can include in them.

A costing version can serve one or more purposes, depending on the data that the costing version contains. The primary purpose of a costing version is to contain cost records about items, cost categories, and calculation formulas for indirect costs. A costing version can contain a set of standard cost records or a set of planned cost records that are based on the costing type that is assigned to the costing version.

## Costing versions for standard or planned costs

### Standard costs

A costing version can support a standard cost inventory model for items, where the costing version contains a set of standard cost records about items and manufacturing processes. Cost data about manufacturing processes is expressed in terms of the cost categories for routing operations and the calculation formulas for manufacturing overheads.

### Planned costs

A costing version can contain a set of planned cost records about items and manufacturing processes. A costing version that contains planned costs is often used to support cost calculation simulations, such as simulations of the effect that cost changes to purchased materials or manufacturing processes have on the calculated costs of manufactured items. The item cost records for planned costs can also be used to support an actual cost inventory model by providing the initial values for item costs. These values include the calculation of planned costs for manufactured items.

## Entering costs

Data maintenance for cost records in a costing version involves entering costs for purchased items and for items that are transferred between sites. Additional data maintenance for manufacturers involves entering costs for cost categories that are associated with routing operations, entering calculation formulas for the indirect costs that reflect manufacturing overhead, and calculating costs for manufactured items.

The item cost data in a costing version consists of one or more cost records for each item. When an item cost record is first entered, it has *Pending* status and an intended effective date. When you activate the item cost record, the status is updated to *Active*, and the effective date is updated to the activation date. Different item cost records can reflect different sites, effective dates, or statuses. When you calculate costs for manufactured items for a future date, the bill of materials (BOM) calculation uses cost records that have the relevant effective date, regardless of whether the status is *Pending* or *Active*. An item's current active cost record is used to estimate production order costs and to value inventory transactions under a standard costing inventory model. The maintenance of cost records for cost categories and indirect cost calculation formulas resembles the maintenance of item cost records.

Two blocking policies for a costing version determine whether pending costs can be maintained and whether the pending cost can be activated. Use the blocking policies to permit data maintenance, and then use them to prevent data maintenance for cost records in a costing version. The following blocking policies can prevent pending costs from being updated or modified until they are finalized:

- *Block* – Prevents pending costs from being edited in or added to a cost version.
- *Block activation* – Prevents pending costs from being activated.

A costing version can also contain data about item sales prices or purchase prices for BOM calculation purposes.

## Item sales prices for BOM calculations

The main reason for including data about sales prices is to retain a manufactured item’s calculated sales price. The calculated sales price can then be analyzed to determine how components, routing operations, and overhead contribute to the cost and sales price.

A secondary reason for including data about sales prices is to define the sales price records for component items. These records can then be used to calculate the sales price of manufactured items. You first define the sales price model that is embedded in a BOM calculation group, and assign the BOM calculation group to purchased items. Then, when you perform BOM calculations that use planned costs, you select the cost price model of the BOM calculation group.

Otherwise, the sales price records for items are used only as reference information, regardless of whether the records are manually entered or calculated. By activating an item’s sales price record, you can update the item’s base sales price. However, the base sales price isn't site-specific and can be manually overridden. The item’s base sales price is used as a default sales price on sales orders and sales quotations.

## Item purchase prices for BOM calculations

The main reason for enabling purchase price data is to define purchase price records for component items, so that these records can be used to calculate the costs of manufactured items. The item purchase price records must be manually entered.

To enable purchase price content, you first define a BOM calculation group that contains a cost price model for the item’s purchase price, and assign the BOM calculation group to purchased items. You then use a cost price model for the BOM calculation group when you perform BOM calculations that use planned costs to calculate the sales price of manufactured items.

The purchase price records for items are also used as reference information. By changing the status of an item’s purchase price record from *Pending* to *Active*, you can update the item’s base purchase price. However, the base purchase price isn't site-specific and can be manually overridden. The item's base purchase price is used as a default purchase price on purchase orders.

## Related information

- [Glossary of terms in Dynamics 365 business processes](/dynamics365/guidance/business-processes/glossary#costing-methodology)
- [Define service costing overview and relation to other business processes](/dynamics365/guidance/business-processes/concept-to-market-define-service-costing-overview)
- [Business process for product costing and how it relates to other processes with Dynamics 365](/dynamics365/guidance/business-processes/design-to-retire-define-product-costing-overview)

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
