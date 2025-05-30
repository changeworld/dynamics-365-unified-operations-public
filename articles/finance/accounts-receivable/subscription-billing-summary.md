---
title: Subscription billing overview
description: Learn about subscription billing in Microsoft Dynamics 365 Finance, including overviews of various types of billing modules.
author: JodiChristiansen
ms.author: jchrist
ms.topic: article
ms.date: 05/12/2025
ms.reviewer: twheeloc
audience: Application User
ms.search.region: Global
ms.search.validFrom: 2022-02-09
ms.search.form: CustPosting, CustVendExternalItem
ms.dyn365.ops.version: 10.0.25
ms.assetid: cb82245e-8c02-429c-b36e-8db0e3e6f7e5
---

# Subscription billing overview

[!include [banner](../includes/banner.md)]

Subscription billing enables organizations to manage subscription revenue opportunities and recurring billing through billing schedules. Complex pricing and billing models and revenue allocation are easily managed, and are billed and recognized at the line level. Multi-element revenue allocation enables allocation of revenue to comply with International Accounting Standards (International Financial Reporting Standard 15 \[IFRS 15\]) and Generally Accepted Accounting Principles (US GAAP) standards (Accounting Standards Codification Topic 606 \[ASC 606\]).

The solution has three modules that can be used independently. Alternatively, all three modules can be used together.

- **Recurring contract billing** – This module enables recurring billing and price management to provide control over pricing and billing parameters, contract renewal, and consolidated invoicing.
- **Revenue and expense deferrals** – This module eliminates manual processes and dependency on external systems by managing revenue and enabling real-time insight into monthly recurring revenue.
- **Multiple element revenue allocation** – This module helps with revenue compliance by handling pricing and revenue allocation across multiple items.

For more information about subscription billing, see [Subscription billing Power BI content](sub-bill-power-bi.md).

>[!NOTE]
> Subscription billing is enabled through **Feature management**. However, it can't be used with the **Revenue recognition** feature. You must disable that feature before you enable subscription billing.

1. In the **Feature management** workspace, on the **All** tab, enter **Revenue recognition** in the filter, and then select the feature name as the filter.
2. Select the **Revenue recognition** feature, and then select **Disable**.
3. In **Feature name** filter, enter **Subscription billing**, and then select the module filter.
4. Select the **Subscription billing** feature, and then select **Enable**.
5. Select one of the three modules from the previous list, and then select **Enable**. Repeat this step for each of the other two modules.

    > [!IMPORTANT]
    > The **Subscription billing** feature must be enabled before you can enable any of the three modules.
