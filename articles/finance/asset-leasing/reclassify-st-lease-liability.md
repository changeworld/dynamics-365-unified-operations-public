---
title: Reclassify the short-term portion of a lease liability
description: Learn about how to create a monthly journal entry to reclassify a portion of the lease liability, with steps for posting a short-term liability journal entries.
author: moaamer
ms.author: moaamer
ms.topic: how-to
ms.date: 04/12/2021
ms.reviewer: kfend
audience: Application User
ms.search.region: Global
ms.search.validFrom: 2020-10-28
ms.search.form: Dialog
ms.dyn365.ops.version: 10.0.14
ms.assetid: 5f89daf1-acc2-4959-b48d-91542fb6bacb
---

# Reclassify the short-term portion of lease liability

[!include [banner](../includes/banner.md)]

This article explains how to create a monthly journal entry to reclassify a portion of the lease liability as short-term. When the schedule that is selected in the batch process is **Short-term lease liability reclass**, a journal entry is created. This entry is used to post the current portion of the lease liability on the last day of the month. At the same time, a reversal entry is posted as of the first day of the next month.

The short-term portion of the lease liability is shown on the liability amortization schedule. When the journal entry is posted, the **Liability reclass journal created** column becomes available, and the journal ID is also filled in on the schedule.

To create and post the short-term liability reclassification journal entry, follow these steps.

1. Go to **Asset leasing \> Periodic \> Batch journal creation**.
2. In the **Batch journal creation** dialog box, in the **Select schedule** field, select **Short-term lease liability reclass**.
3. In the **Lease group** field, select a lease group. Alternatively, in the **Book ID** field, select the book ID.
4. Turn on the **Post** parameter. Alternatively, if the entry should be created but not posted, leave this parameter turned off.
5. Select **OK**.


[!INCLUDE[footer-include](../../includes/footer-banner.md)]
