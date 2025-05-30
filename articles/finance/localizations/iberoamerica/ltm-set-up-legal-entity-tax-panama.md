---
title: Set up a legal entity and tax information for Panama
description: Learn how to set up a legal entity and tax information for a company in Panama, including a step-by-step process on creating a legal entity.
author: Cpicon85
ms.author: v-cpicon
ms.topic: how-to
ms.date: 04/29/2025
ms.custom: bap-template
ms.reviewer: johnmichalak
---

# Set up a legal entity and tax information for Panama

[!include [banner](../../includes/banner.md)]

This article explains how to set up a legal entity and tax information for a company that's located in Panama and is using the Latin American (LATAM) features that are available in Microsoft Dynamics 365 Finance. A legal entity represents the company, and it contains the tax and legal attributes that are required for the rest of the LATAM configuration.

Before you begin, open the **Feature management** workspace, and verify that the **LATAM globalization expansion – Panama** feature is enabled. If it isn't enabled, enable it. After you're sure that the feature is enabled, complete the following procedures.

## Create a legal entity

1. Go to **Organization administration** \> **Organizations** \> **Legal entities**, and select **New** to create a legal entity. Some functionality is enabled only for Panama. Examples include specific tax reports or electronic invoices.
2. In the address setup, set up the address format for Panama by using **State** as **Province**, **County** as **District**, and **City** as **Corregimiento**.
3. Go to **Organization administration** \> **Setup** \> **LATAM** \> **LATAM parameters**.
4. On the **Concept and notes** tab, in the **Legal entity** section set a field as **Activity**.

## Set up tax information

1. [Create a document class letter](ltm-core-document-class-letter.md) without a prefix. This document class letter will be used in taxpayer and document class configurations.
2. Go to **Organization administration** \> **Setup** \> **LATAM** \> **Tax ID type**.
3. Select **New**, and then, in the **Overview** section, in the **Tax ID type** field, enter **RUC** (Unique Taxpayer Registry), which is one of the tax ID types for Panama.
4. Set the method validation to **None**. Learn more in [Tax ID types for Latin America](ltm-core-tax-id-type.md).
5. Go to **Organization administration** \> **Global address book** \> **Addresses**, select the country/region where the company is set, and then select **LATAM** to add the **RUC** tax ID type. For more information, see [Address setup for Latin America](ltm-core-address-setup.md).
6. Go to **Organization administration** \> **Setup** \> **LATAM** \> **Taxpayer type**, and select **New** to create a record that represents organizations.
7. In the **Type** field, select **persona juridica**. Then add the tax ID type and the document class letter that you created. For more information, see [Taxpayer types for Latin America](ltm-core-taxpayer-type.md).
8. Go to **Organization administration** \> **Organizations** \> **Legal entities**, and then, in the **LATAM** section, configure the following entity tax and legal information:

    - In the **Taxpayer type** field, select **persona juridica** to represent an organization.
    - In the **Based in country/region** field, select **Panama**.
    - In the **Country document type** field, select **RUC**.
    - Complete the **Country document number** field, including the tax ID number of the company. Note that you must add the last two characters with the verification digit, with no character separation from the RUC number.
    - In the **Concept and notes** section, in the first field, enter the company activity.

[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
