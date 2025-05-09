---
title: Cost calculation level
description: Learn about the bill of materials (BOM) level that is named Cost calculation level. This BOM level excludes production and batch orders from its calculations.
author: prasungoel
ms.author: prasungoel
ms.reviewer: kamaybac
ms.search.form:
ms.topic: how-to
ms.date: 03/17/2025
ms.custom: 
  - bap-template
---

# Cost calculation level

[!include [banner](../includes/banner.md)]

The bill of materials (BOM) level that is named **Cost calculation level** excludes production orders and batch orders from its calculations. The system uses this level when it runs cost calculations in costing versions. In processes such as recalculation and inventory close, the system uses the **Costing level** BOM level instead.

## Turn the Cost calculation level feature on or off

To use this feature, it must be turned on for your system. As of Supply Chain Management version 10.0.29, it's turned on by default. As of Supply Chain Management version 10.0.36, the feature is mandatory and can't be turned off. If you're running a version older than 10.0.36, then admins can turn this functionality on or off by searching for the *Cost calculation level* feature in the [Feature management](../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md) workspace.

## Example scenario

The following simple scenario shows the differences between the **Cost calculation level** BOM level and the **Costing level** BOM level.

You have three products: A, B, and C. Product C is the component of product B, and product B is the component of product A.

- **Costing level** assigns the following BOM levels:

    - **Product A:** 0
    - **Product B:** 1
    - **Product C:** 2

- **Cost calculation level** assigns the following BOM levels:

    - **Product A:** 0
    - **Product B:** 1
    - **Product C:** 2

A production order for product C is then created, and product A is added to the production order BOM. After the order is estimated, BOM levels are updated in the following way:

- **Costing level** assigns the following BOM levels:

    - **Product B:** 1
    - **Product C:** 2
    - **Product A:** 3

- **Cost calculation level** assigns the following BOM levels:

    - **Product A:** 0
    - **Product B:** 1
    - **Product C:** 2

This behavior ensures that changes to production order BOMs don't affect subsequent cost calculations.

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
