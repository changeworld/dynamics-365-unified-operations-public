---
title: SAF Bank statement file - JPK_WB
description: This article explains how users in legal entities in Poland can generate a SAF Bank statement file - JPK_WB in XML format.
author: liza-golub
ms.author: egolub
ms.topic: reference
ms.custom: 
  - bap-template
ms.date: 11/27/2024
ms.reviewer: johnmichalak
ms.search.region: Poland
ms.search.validFrom: 2016-11-30
ms.search.form: LedgerParameters, TaxAuthority, TaxReportCollection, TaxTable
ms.dyn365.ops.version: Version 1611
ms.assetid: b85c4019-f682-45bf-9a0d-c7549a2f1274
---

# SAF Bank statement file - JPK_WB

[!include [banner](../../includes/banner.md)]

This article explains how to set up Microsoft Dynamics 365 Finance to configure and generate a SAF Bank statement file - JPK_WB in legal entities that have a primary address in Poland.

SAF Bank statement file (JPK_WB) is a standardized electronic format that enables businesses to submit detailed bank account statements directly to Polish tax authorities in a structured and consistent manner.

A SAF Bank statement file - JPK_WB must be submitted whenever Polish tax authorities request one. It must be submitted electronically through the Polish tax authority's portal.

## Setup

Before you can generate a SAF Bank statement file - JPK_WB, you must complete the following setup.

1. [Import Electronic reporting (ER) configurations](#er-import).
1. [Set up the ER format in General ledger parameters](#er-format-setup).

### <a id="er-import"></a>Import ER configurations

In Finance, import the following ER configurations from Dataverse. Learn more about how to import ER configurations in [Import Electronic reporting (ER) configurations from Dataverse](../../localizations/global/workspace/gsw-import-er-config-dataverse.md).

| ER configuration name | Type | Description |
|---|---|---|
| Standard Audit File (SAF-T) | Model | The common data model for different audit reports. |
| Standard Audit File model mapping | Model mapping | The model mapping that provides general source mapping for several electronic reports for Poland. |
| SAF Poland | Format | The XML format that represents a parent format for several JPK formats for Poland. |
| Bank Statement (PL) | Format | The XML format that represents Bank Statement (WB) SAF-T for Poland. |

Import the most recent versions of the configurations. The version description usually includes the number of the Knowledge Base (KB) article that explains the changes that were introduced in the configuration version.

> [!IMPORTANT]
> After all the ER configurations from the previous table are imported, set the **Default for model mapping** option to **Yes** for the **Standard Audit File model mapping** configuration.

### <a id="er-format-setup"></a>Set up the ER format in General ledger parameters

To set up the ER format in General ledger parameters, follow these steps.

1. Go to **General ledger** \> **Ledger setup** \> **General ledger parameters**.
1. On the **Standard Audit File for Tax (SAT-T)** tab, in the **SAF Bank statements** field, select the **VAT Invoices (PL)** ER format.

## <a id="jpk-wb"></a>Generate a SAF Bank statement file - JPK_WB

To generate a SAF Bank statement file - JPK_WB, go to **General ledger** \> **Inquiries and reports** \> **Standard Audit File for Tax (SAF-T)** \> **SAF Bank statement**, set the following parameters, and then select **OK**.

| Parameter | Description |
|---|---|
| From date | Specify the first date to export reporting data for. |
| To date | Specify the last date to export reporting data for. |
| Authority identification | In the list, select the identifier of the tax authority to use in the export file. |
| Bank account | Specify the bank account to export transactions for. |

The SAF Bank statement file includes information about transactions that were posted during the specified period for the selected bank account. The name of the counterparty that is reported in the **NazwaPodmiotu** element is collected from the **Customers** master data (**Accounts receivable** \> **Customers** \> **All customers**) and the **Vendors** master data (**Accounts payable** \> **Vendors** \> **All vendors**) of the system that is registered in the legal entity, as it's related to the posted bank transaction. The operation description that is reported in the **OpisOperacji** element is collected from the **Description** field of the bank transaction.

## Using a batch job to generate a SAF Bank statement file - JPK_WB

A SAF Bank statement file - JPK_WB for a long period, such as a month or a quarter, can include a large amount of data and take a long time to be generated. Therefore, we recommend that you use a batch job. The dialog box for every SAF report includes a **Run in the background** tab where you can set up report generation in batch mode. Set the **Batch processing** option to **Yes**. Learn more about batch processing in [Batch processing overview](../../../fin-ops-core/dev-itpro/sysadmin/batch-processing-overview.md).

To review batch jobs or find a generated file, follow these steps.

1. Go to **Organization administration** \> **Electronic reporting** \> **Electronic reporting jobs**.
1. Find a line that is related to your job, and then select **Show log**. If nothing is shown, no messages were produced when the file was generated.
1. To view a file, select **Show files**, find the file that you need, and then select **Open**.

When an electronic report is generated in batch mode, you can find related batch information and the generated output file as an attachment by going to **Organization administration** \> **Electronic reporting** \> **Electronic reporting jobs**.

Learn more about how to configure a destination for each ER format configuration and its output component in [Electronic reporting (ER) destinations](../../../fin-ops-core/dev-itpro/analytics/electronic-reporting-destinations.md).
