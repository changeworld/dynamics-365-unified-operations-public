---
title: Master planning and multisite functionality overview
description: Learn about master planning and multisite functionality, which take the settings of the site and warehouse inventory dimensions into account. 
author: Henrikan
ms.author: henrikan
ms.topic: overview
ms.date: 07/25/2019
ms.custom:
ms.reviewer: kamaybac
ms.collection: get-started
ms.search.form: InventLocation, InventSite
ms.assetid: 7f05c031-a446-4168-8cce-03a6305f5c4d
---

# Master planning and multisite functionality overview

[!include [banner](../includes/banner.md)]

Master planning takes the settings of the site and warehouse inventory dimensions into account. 

The site dimension is mandatory, and you can set the warehouse dimension to be mandatory.

When a dimension is mandatory, a dimension value must be entered on all inventory transactions. Therefore, during master planning, the site and the warehouse for the initial demand are known. The site dimension is also consistent so that during the explosion of lower-level demand, the site value does not change.

When the warehouse is not set to mandatory, it may not be known from the initial demand. The planning engine must determine which warehouse to use based on the settings that are defined for the item, individual warehouses, and the details of the order line.

The following articles describe how the planning engine works, when different settings are defined, to determine the warehouse to use.

[Master planning for site and warehouse coverage, warehouse mandatory](master-plan-site-warehouse-coverage-warehouse-mandatory.md)

[Master planning for site coverage, mandatory warehouse](master-plan-site-coverage-warehouse-mandatory.md)

[Master planning for site and warehouse coverage, warehouse not mandatory](master-plan-site-warehouse-coverage-warehouse-not-mandatory.md)

[Master planning for site coverage, warehouse not mandatory](master-plan-site-coverage-warehouse-not-mandatory.md)

[Determine the BOM version](master-plan-bom-version-determined.md)





[!INCLUDE[footer-include](../../includes/footer-banner.md)]