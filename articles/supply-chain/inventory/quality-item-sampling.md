---
title: Quality management item sampling
description: Learn how to set up item sampling and how it's used as part of a quality association, including an outline and step-by-step process for setting up item sampling.
author: johanhoffmann
ms.author: johanho
ms.reviewer: kamaybac
ms.search.form: InventItemSampling
ms.topic: how-to
ms.date: 06/17/2025
ms.custom: 
  - bap-template
---

# Quality management item sampling

[!include [banner](../includes/banner.md)]

Item sampling is used as part of a quality association. It defines the amount of current physical inventory that must be inspected. Sampling can be based on fixed quantities, a percentage, or a full license plate.

## Set up item sampling

Follow these steps to set up item sampling.

1. Go to **Inventory management \> Setup \> Quality control \> Item sampling**.
1. Select **New**.
1. In the **Item sampling** field, enter a value.
1. In the **Description** field, enter a value.
1. In the **Value** field, enter a number. This value is related to the quantity specification value that is selected in the adjacent field.
1. On the **Process** FastTab, set **Full blocking** to *Yes* if the whole lot or order line quantity should be blocked if a test is failed. Set this option to *No* if only the items in the quality order should be blocked if a test is failed.
1. On the **Process** FastTab, enable each dimension (such as **License plate** or **Batch number**) that should be populated automatically on the **Inventory dimensions** tab of a quality order.
1. Select **Save**.
1. Close the page.

> [!NOTE]
> The *Quality management for warehouse processes* feature provides additional item sampling capabilities. It adds the concept of *item sampling scope* and lets you define a full license plate as the quantity specification. If you've turned on this feature, see [Quality management for warehouse processes](quality-management-for-warehouses-processes.md).

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
