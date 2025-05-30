---
title: Chinese vouchers
description: Learn about Chinese vouchers and how they are used in Microsoft Dynamics 365 Finance, including an outline on voucher creation methods.
author: AdamTrukawka
ms.author: atrukawk
ms.topic: article
ms.custom: 
  - bap-template
ms.date: 07/10/2024
ms.reviewer: johnmichalak
ms.search.region: China (PRC)
ms.search.validFrom: 2016-11-30
ms.search.form: LedgerVoucherType_CN, VoucherTypeWizard_CN
ms.dyn365.ops.version: Version 1611
---

# Chinese vouchers

[!include [banner](../../includes/banner.md)]

This article describes Chinese vouchers and how they are used.

You must create a voucher document for every posted journal. You can print a paper voucher and a posted journal. Based on your requirements, you can use the Voucher type setup wizard to set up the **Get**, **Pay** and **Transfer** voucher types that are often used, or you can create new voucher types on the **Voucher type setup** page. You can use booking vouchers to enter and group transactions into the Receipt voucher, Payment voucher, or Transfer voucher. 

A continuous number sequence that begins from the first day of every monthly period should be assigned to each voucher type. On the **Voucher type setup** page, you can define validation rules for posting voucher transactions to the specified accounts. During voucher posting, validation is run, based on the rules that are specified on the **Voucher type setup** page. You receive a message if the voucher type that is selected for the document is incorrect. 

For example, you select a ledger account of the **Credit** type for the **Get** voucher type. However, the validation rule that you defined for the **Get** voucher type specifies that the ledger account must be a debit account. In this case, you receive a message that states that the Chinese voucher type isn't valid. You can then make the appropriate changes and post the voucher again. 

For more information, see [Set up Chinese vouchers](set-up-chinese-vouchers.md).

## Voucher creation methods
You can create voucher transactions on the **General journal** page by using the **Simple** or **Advanced** method. If you create journal vouchers of a single voucher type by using the **Simple** method, the voucher type that is selected on all the journal lines should be the same. The **Advanced** method lets you create multiple journal lines of different voucher types. 

## Check for continuity in voucher numbers
The Chinese voucher number should be sequential, and there should be no gaps in the fiscal period. You can run a batch process to determine whether there are gaps in the Chinese voucher numbers. The batch process verifies the transaction dates and then renumbers the vouchers for continuity. For tracking purposes, you can generate the **Chinese voucher continuity check** report. This report shows the history of renumbered Chinese vouchers. For more information, see [Chinese voucher continuity check](chinese-voucher-continuity-check.md).

## Printing a Chinese voucher
You can print a Chinese voucher either before or after you post the voucher. The printed voucher shows information such as the history of renumbered Chinese vouchers, and tax information before or after the voucher was posted. You can review the printed information to verify that the information is the same before and after posting, and that the information is correct. For example, if you select sales tax in a journal voucher, the final voucher information includes the sales tax. However, the sales tax might differ from the sales tax that was part of the journal. The printed result must be accurate, and it must be the same as the result that is generated after the final posting. Therefore, you can print a Chinese voucher that has the correct information from both the journal voucher and the voucher transactions. You can also print Chinese vouchers in a batch after you filter the information by Chinese voucher type and fiscal period.

## Additional resources
- [Post vouchers from the general journal](post-vouchers-general-journal.md)
- [Post vouchers from other modules, like sales invoices](post-vouchers-other-modules-like-sales-invoices.md)





[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
