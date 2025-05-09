﻿---
title: Customer specific certificate of analysis (COA) (preview)
description: Learn how to customize the content of a COA to meet specific customer requirements and automatically print the COA when generating a sales order packing slip
author: johanhoffmann
ms.author: johanho
ms.reviewer: kamaybac
ms.search.form: QMSInventTestCertOfAnalysisCustGroup, InventTestGroup, InventQualityOrderTable
ms.topic: how-to
ms.date: 04/25/2025
ms.custom: 
  - bap-template
---

# Customer specific certificate of analysis (COA) (preview)

[!include [banner](../../includes/banner.md)]
[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]
<!-- KFM: Preview until further notice -->

Supply Chain Management provides the ability to create a basic certificate of analysis (COA) from the quality order or from the menu directly after selecting a quality order. Learn more about how to use the basic COA in [Quality orders](quality-orders.md). This article explains how to customize the content of a COA to meet specific customer requirements and automatically print the COA when generating a sales order packing slip.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

To use the features described in this article, your system must meet the following requirements:

- You must be running Microsoft Dynamics 365 Supply Chain Management version 10.0.44 or later.
- The feature that is named *(Preview) Advanced quality management* must be turned on in [feature management](../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md).

## Set up a COA customer group

To manage COA for different customers, you can group customers by assigning them to COA customer groups. To create and add customers to a COA customer group, follow these steps.

1. Go to: **Inventory management** \> **Setup** \> **Certificate of analysis** \> **Certificate of analysis customer groups**.
1. Use buttons in the action pane to add, edit, or delete a COA customer group.
1. Make the following selections for your new or selected COA customer group.
    - **COA customer group** - Identification of the COA customer group.
    - **Description** - Description of the COA customer group.

## Set up and maintaining customer COA requirements on test groups

To set up customer-specific COA requirements on test groups follow these steps:

1. Go to **Inventory management** \> **Setup** \> **Quality control** \> **Test groups**
1. In the lower section of the page, select a test.
1. In the tool bar, select customer COA requirements to open the customer COA requirements page.
1. Use the buttons in the action pane to add, edit, or delete a customer COA requirement.
1. When making a new customer COA requirement the fields test and test group will be automatically filled our. The **Attribute** field is filled out if the test is associated a Batch attribute.
1. Fill out the fields in the grid to complete the creation of the requirement.
    - **Customer code** - Choose *All* to make the requirement applicable for all customers, *Group* for a group of customers, and *Table* for a specific customer.
    - **Customer relation** - Dependent on your selection in **Customer code** select a *COA customer group* or a specific *Customer account*.
    - **Exclude** - Indicates if the test should appear on customer-specific COA. All tests are assumed to be included except those specifically marked as excluded.
    - **Use customer specific ranges** - Indicates whether the customer specific batch attribute range should be used for the customer-specific COA. If no customer specific batch attribute range if found, then the standard range will print.
    - **Suppress Min/Max values** - Indicates if the minimum and maximum values of the Test should be suppressed on the customer-specific COA. For example, for a given test, let's assume that the minimum is 1 and the Maximum is 10 and the Result is 1. For certain customers, it might be desirable that the range doesn't display at all, not to draw attention to the fact that the result just passed the quality test.
    - **Replace pass results** - When populated, the verbiage will replace the test results on the customer-specific COA if the test is passed. Some businesses would prefer to not show the actual test results but instead just show standard verbiage such as *Within specifications* for a pass.
    - **Replace fail results** - When populated, the verbiage will replace the test results on the customer's COA if the test is failed. Some businesses would prefer to not show the actual test results but instead just show standard verbiage such as *Outside acceptable range* for a failure.

## Set up and maintain customer COA requirements from a quality order

To set up and maintain customer COA requirements from a quality order, follow these steps.

1. Go to **Inventory management** \> **Periodic** \> **Quality management** \> **Quality orders**
1. Select a quality order
1. Select a line on the selected quality order
1. From the action pane, select customer COA requirements
1. Follow the same steps for adding, deleting, or editing customer COA requirements as described in previous section about test groups.

## Include product- and customer-specific batch attributes in COA

You can mark product and customer specific batch attributes to be included into the COA, even if they aren't included in testing through a quality order.

1. Go to **Product information management** \> **Products** \> **Released products**.
1. In the **All released products** list page, find and select or open the batch-enabled product you want to set up.
1. On the Action Pane, open the **Manage inventory** tab and, from the **Batch attributes** group, select either **Product specific** or **Customer specific**.
1. Select an existing attribute from the list pane or create a new one.
1. To include your new or selected attribute in COA, set **Include in COA independent of quality order** to *Yes*.
1. Repeat the previous steps for each attribute you want to include in the COA.

Once the customer COA requirements are set for a test group, they'll automatically apply to all quality orders using that test group. However, these requirements can be adjusted directly on the quality order if needed.

## Access customer-specific COAs

Customer-specific COAs can be accessed from the menu paths listed in the following table.

| Access Method | Navigation Path | Details |
|--|--|--|
| From the menu directly | **Inventory management** \> **Inquiries** \> **Quality management** \> **Certificate of analysis** | You can print both the standard COA and customer-specific COA (triggered by selecting a specific customer account). You must select a quality order in both cases. |
| From a quality order | **Inventory management** \> **Periodic** \> **Quality management** \> **Quality order** \> **Ribbon: Inquiries** \> **Certificate of analysis** | You can print both the standard COA and customer-specific COA (triggered by selecting a specific customer account). Since access is from a quality order, the Quality order is assumed in both cases. |
| From an inventory batch | **Inventory management** \> **Inquiries** \> **Dimensions** \> **Batches** \> **Ribbon: Inquiries** \> **Certificate of analysis** | You can print both the standard COA and the customer-specific COA (triggered by selecting a specific customer account). Since access is from an inventory batch, the Certificate of analysis Quality order (found on the General tab) on the Inventory Batch is used in both cases to generate the COA. If the Certificate of analysis quality order needs to be updated, the ribbon action **Reset COA Quality order** can be used to change the quality order that drives the details of the COA. |
| As part of processing the Sales order packing slip | **Sales and marketing** \> **Common** \> **Sales orders** \> **All sales orders** \> **Ribbon: Pick and pack** \> **Generate** \> **Packing slip** or **Sales and marketing** \> **Periodic** \> **Sales update** \> **Packing slip** | Only customer-specific COAs are printed from this process. Based on the customer placing the order, the system prints a customer-specific COA for every item/batch combination on the order that has a Certificate of analysis Quality order specified on the Batch. No COA is printed for items not batch-controlled or for items where the batch doesn't have a Quality order specified. |

> [!NOTE]
> The option to print customer-specific COA is initially defaulted from the Accounts Receivable parameters from the Updates tab. This parameter defaults to new customers. The checkbox on the Packing slip process form defaults from the customer if processing for a single order. If processing for multiple orders, you must select this checkbox to print customer-specific COAs.
