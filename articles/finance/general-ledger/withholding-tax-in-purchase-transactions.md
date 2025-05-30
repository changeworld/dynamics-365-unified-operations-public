---
title: Withholding tax in purchase transactions
description: For vendors who are liable to withholding tax, you can assign the default withholding tax group on the all vendors page.
author: kailiang
ms.author: kailiang
ms.topic: how-to
ms.date: 01/12/2021
ms.reviewer: kfend
audience: Application User
ms.search.region: Global
ms.search.validFrom: 2020-01-12
ms.search.form: 
ms.dyn365.ops.version: AX 10.0.16
ms.assetid: b4b406fa-b772-44ec-8dd8-8eb818a921ef
---

# Withholding tax in purchase transactions

For vendors who are liable to withholding tax, you can assign the default **Withholding tax group** on the **All vendors** page.

1. Go to **Navigation pane > Modules > Accounts payable > Vendors > All vendors**.

2. Click the respective Vendor account, click **Edit**.

3. In **Invoice and delivery** tab, set the **Calculate withholding tax** field to **Yes**.

   > [!NOTE] 
   > Withholding tax will not be calculated if **Calculate withholding tax** is not switched on for this vendor in the data.

4. Select a withholding tax group in **Withholding tax group**.

5. Click **Save**.

For items and services that are liable to withholding tax, you can assign the default **Item withholding tax group** in **Released Products**.

1. Go to **Navigation pane > Modules > Product information management > Products > Released products**.

2. Click the respective Item number, click **Edit**.

3. In **Purchase** tab, click **Calculate withholding tax**.

   > [!NOTE] 
   > Withholding tax will not be calculated if **Calculate withholding tax** isn't set to **Yes** for this Item in the **Purchase** tab on the **Released product** page.

4. Select an item withholding tax group in **Item withholding tax group** list.

5. Click **Save**.

Withholding tax groups and Item withholding tax groups can be assigned in pages: 

- **Purchase order**
- **Vendor invoice**
- **Invoice journal**

The default Withholding tax group and Item withholding tax group are carried into the lines when creating **Purchase orders** and/or **Pending Vendor invoices**. For **Vendor invoice journal**, you can switch on **Calculate withholding tax** and select **Item withholding tax group** in the **General** tab in the journal.

The temporary amount of withholding tax is available in the field **Adjusted withholding tax** of the **Totals** tab on the **Purchase order** page.

![Withholding tax is included on the purchase order.](media/withholding-tax-adjusted.png)

   > [!NOTE] 
   > Starting in version 10.0.33, a new option **Estimate withholding tax amount on invoice** is available on the **Withholding tax** tab of the **General ledger parameters** page. When you enable this option, a **Withholding tax** button is available on purchase orders and vendor invoices to estimate the withholding tax amount.


Withholding tax is calculated on **Vendor payment journal**. You can manually adjust the applicable withholding tax codes and the actual withholding tax amounts in the **Withholding tax** tab on the **Settle transactions** page.

![Withholding can be manually adjusted on the Settle transactions page.](media/withholding-tax-vendor-payment-tab.png)

The derived withholding tax amount is deducted from the vendor payment and posted to the **Withholding tax account** in a related voucher.

![Withholding tax account showing a related voucher.](media/withholding-tax-adjusted.png)


[!INCLUDE[footer-include](../../includes/footer-banner.md)]
