---
title: Access Business performance analytics
description: Learn about how to access Business performance analytics, including an outline on how to share performance analytics with users.
author: jkhaira7
ms.author: jkhaira
ms.topic: how-to
ms.custom:
ms.date: 10/30/2024
ms.reviewer: twheeloc 
audience: Application User
---

# Access Business performance analytics

[!include [banner](../includes/banner.md)]

This article explains how to access Business performance analytics.

## Access Business performance analytics as an administrator

After Business performance analytics is installed, there are several ways to access the app:

- In [Power Platform admin center](https://admin.powerplatform.microsoft.com/), go to the environment where you installed the app, and find the environment URL.
- In the Power Platform maker portal, go to **Apps**, and find and select **Business performance analytics**.

### Access Business performance analytics from finance and operations apps

A shortcut to access Business performance analytics in Dynamics 365 finance and operations apps is visible to users with one of the following duties assigned:

- View manage bank accounts workspace
- Maintain budget plans
- View cash flow all companies workspace
- View cash flow current company workspace
- View vendor invoice entry workspace
- Maintain purchase orders
- VendPaymentWorkspaceInquire
- View vendor invoice entry workspace
- View vendor profile
- Maintain vendor requests for quotations replies
- BudgetTrackingWorkspaceMaintain
- Maintain vendor collaboration invoices
- GeneralJournalEntryWorkspaceInquire
- CustomerInvoiceWorkspaceView
- CustPaymentWorkspaceView
- Customer credit and collections
- Configure Electronic reporting configuration
- View CFO overview workspace
- View financial insights current company
- View financial period close processes
- Inquire into fixed assets

To open Business performance analytics directly from Dynamics 365 finance and operations apps, confirm the following prerequisites are met:

1. Go to <https://admin.powerplatform.microsoft.com/>.
2. Select **Environments** on the left menu.
2. Select the environment where business performance analytics is installed.
3. Go to **Settings** > **Users**.
4. For Business performance analytics users, confirm that the **Basic user** security role is assigned.

If these prerequisites aren't met, a user who selects the Business performance analytics icon in the **Apps** section is redirected to a public document that explains the functionality. After the prerequisites are met, a user who selects the Business performance analytics icon is redirected to the Business performance analytics app. Administrators can control who the Business performance analytics icon is visible to by granting or removing the associated privileges from users' duties, or by using Feature management to hide the **Apps** section. Administrators can also use security roles and privileges to grant additional users and roles in finance and operations apps access to the Business performance analytics icon.

After these prerequisites are met, the administrator can use security roles and privileges to assign access to the **Business performance analytics** tile in finance and operations apps.

### Share Business performance analytics with users

To share the Business performance analytics app with users, first confirm that those users are set up as Business performance analytics users in the app, and that their security is set up.

1. In Business performance analytics, select **Business performance analytics (preview)**.
2. The dialog box that appears includes a **Published apps** list. Find **Business performance analytics (preview)** in the list, select the three dots, and then select **Manage roles**.
3. Expand **App URL suffix**, and enter a name to use in the custom URL that you share with Business performance analytics users.
4. Copy the URL that's generated, and share it with app users.
