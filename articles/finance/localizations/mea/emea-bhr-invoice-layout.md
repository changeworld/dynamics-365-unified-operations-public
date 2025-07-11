---
title: Configure invoice layout for Bahrain
description: Learn how to configure the invoice layout for Bahrain, including prerequisites and outlines on turning on features and importing configurations.
author: mrolecki
ms.author: mrolecki
ms.topic: how-to
ms.date: 06/05/2025
ms.reviewer: johnmichalak
ms.search.region: Bahrain
ms.search.validFrom: 2020-06-03
ms.custom: 
  - bap-template
  - evergreen
---

# Configure invoice layout for Bahrain (BH-00003)

[!include [banner](../../includes/banner.md)]

This article explains how to configure printable invoice layouts to ensure compliance with Bahraini legal requirements. Bahrain-specific invoice layouts are implemented by using the concept of *configurable business documents*. For more information about configurable business documents, see the [Business document management overview](../../../fin-ops-core/dev-itpro/analytics/er-business-document-management.md). 

## Prerequisites

The primary address of the legal entity must be in Bahrain.

## <a id="features"></a>Turn on features

In the **Feature management** workspace, turn on the following features:

- (Bahrain) Credit invoicing layout for sales and project invoice reports
- Convert Electronic reporting outbound documents from Microsoft Office formats to PDF

For more information about how to turn on features, see [Feature management overview](../../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md).

## <a id="ERConfigs"></a>Import Electronic reporting configurations

In the **Electronic reporting** workspace, import the following Electronic reporting (ER) formats from the repository:

- Sales invoice (Excel) (BH)
- Free text invoice (Excel) (BH)
- Project invoice (Excel) (BH)
- Project contract line items (Excel) (BH)
- Project manage invoice (Excel) (BH)

> [!NOTE]
> These formats are derived from related standard formats, based on the invoice model, and they use the invoice model mapping. All required additional configurations will be automatically imported.

For more information about how to import ER configurations, see [Download Electronic reporting configurations from Lifecycle Services](../../../fin-ops-core/dev-itpro/analytics/download-electronic-reporting-configuration-lcs.md).

## Configure conversion to PDF

By default, invoices are generated as Microsoft Excel files. To enable their conversion to PDF format, follow these steps.

1. In the **Electronic reporting** workspace, in the **Related links** section, select **Electronic reporting destination**.
1. On the **Electronic reporting destination** page, create destinations for the following related formats:

    - Sales invoice (Excel) (BH)
    - Free text invoice (Excel) (BH)
    - Project invoice (Excel) (BH)
    - Project contract line items (Excel) (BH)
    - Project manage invoice (Excel) (BH)
 
1. For each format, follow these steps:

    1. Select the **Convert to PDF** checkbox.
    1. In the **Page orientation** field, select **Portrait**.
    1. Select **Settings**, and then, on the **Destination settings** page, on the **Screen** tab, set the **Enabled** option to **Yes** to enable printing to the screen.

![Enabling conversion to PDF.](../media/emea-bhr-pdf.jpg)

## Configure default model mapping for project invoices

In the **Electronic reporting** workspace, select the **Project invoice model mapping (RDP)** configuration. Turn on **Default model mapping** parameter for the selected configuration.

![Project invoice model mapping configuration.](../media/invoice-model-tree.png)

## Configure parameters

### Configure print management

To configure print management, follow these steps.

1. In Dynamics 365 Finance, go to **Accounts receivable** \> **Setup** \> **Forms** \> **Forms setup**.
1. On the **Form setup** page, on the **General** tab, select **Print management**.
1. On the **Print management setup** page, define the references to the imported formats for the following documents:

    - **Customer invoice:** In the **Report format** field, select **Sales invoice (Excel) (BH)**.
    - **Free text invoice:** In the **Report format** field, select **Free text invoice (Excel) (BH)**.

    ![Configuring Print management.](../media/emea-bhr-print_management.jpg)

1. Go to **Project management and accounting** \> **Setup** \> **Forms** \> **Forms setup**.
1. On the **Form setup** page, on the **General** tab, select **Print management**.
1. On the **Print management** page, define the references to the imported formats for the following documents:

    - **Project invoice without billing rules:** In the **Report format** field, select **Project invoice (Excel) (BH)**.
    - **Project invoice with billing rules:** In the **Report format** field, select **Project contract line items (Excel) (BH)**.
    - **User defined project invoice:** In the **Report format** field, select **Project manage invoice (Excel) (BH)**.

### Configure sales tax specification

To configure sales tax specification, follow these steps.

1. In Dynamics 365 Finance, go to **Accounts receivable** \> **Setup** \> **Forms** \> **Forms setup**.
1. On the **Form setup** page, on the **General** tab, in the **Sales tax specification** field, select **Registration and company currency**.

    ![Configuring sales tax specification.](../media/emea-bhr-tax-spec.jpg)

1. Go to **Project management and accounting** \> **Setup** \> **Forms** \> **Forms setup**.
1. On the **Form setup** page, on the **General** tab, in the **Sales tax specification** field, select **Registration and company currency**.

### Configure packing slip specification

To configure packing slip specification, follow these steps.

1. In Dynamics 365 Finance, go to **Accounts receivable** \> **Setup** \> **Forms** \> **Forms setup**.
1. On the **Form setup** page, on the **Invoice** tab, select the **Print packing slip specifications** checkbox.

    ![Configuring packing slip specification.](../media/emea-bhr-packing-spec.jpg)

1. Go to **Project management and accounting** \> **Setup** \> **Forms** \> **Forms setup**.
1. On the **Form setup** page, on the **Invoice** tab, select the **Print packing slip specifications** checkbox.

### Activate credit invoicing

To activate credit invoicing, follow these steps.

1. In Dynamics 365 Finance, go to **Accounts receivable** \> **Setup** \> **Accounts receivable parameters**.
1. On the **Accounts receivable parameters** page, on the **Updates** tab, on the **Invoice** FastTab, set the **Apply the credit invoicing layout into sales and project invoice reports** option to **Yes**.

![Activating credit invoicing.](../media/emea-bhr-credit.jpg)

## Generate invoices

After you've completed all the previous procedures in this article, you can print invoices that are based on sales orders and free text invoices, in accordance with Bahraini legal requirements.


[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
