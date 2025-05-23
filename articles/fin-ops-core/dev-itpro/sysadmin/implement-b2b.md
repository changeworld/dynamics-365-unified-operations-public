---
title: Export business-to-business (B2B) users to Microsoft Entra ID
description: Learn about implementing the business-to-business transaction functionality, including an overview on setting up invitation service applications.
author: paulliew
ms.author: paulliew
ms.topic: how-to
ms.date: 04/09/2019
ms.custom:
ms.reviewer: johnmichalak
audience: developer, IT Pro
ms.search.region: Global
ms.search.validFrom: 2017-10-31
ms.search.form: B2BInvitationConfiguration
ms.dyn365.ops.version: Platform update 12
---

# Export business-to-business (B2B) users to Microsoft Entra ID

[!include [banner](../includes/banner.md)]

You can automatically export business-to-business (B2B) users to Microsoft Entra ID. 

In the past, B2B users were exported manually to a .csv file. Then the Microsoft Entra tenant administrator had to use this file to manually add the users to Microsoft Entra using the Azure portal. 

To enable the automatic export feature, a one-time setup and configuration process must be completed. When the process is completed, you can use the **Provision Microsoft Entra B2B user** workflow task to automatically export B2B users to Microsoft Entra ID.

The one-time set up and configuration means that you'll need to: 
1. Set up a B2B invitation service application in Microsoft Entra ID.
2. Configure the B2B invitation service settings in finance and operations.

### Set up a B2B invitation service application in Microsoft Entra ID
The tenant administrator of your Microsoft Entra tenant will need to complete the following steps.

1. Log on to the [Azure portal](https://portal.azure.com) as the tenant administrator. 

2. Click **Microsoft Entra ID** > **Properties**.

3. Copy the **Directory ID** (this is the tenant ID) and save it. You will need this later.

4. Click **App registrations** > **New application registration**.

5. Enter the following information, and then click **Create**.
    1. In the **Name** field, enter the name of the application. For example: **B2B admin application**.
    2. In the **Application type** field, select **Web app /API**.
    3. In the **Sign-on URL** field, enter the URL for finance and operations.
  
6. Click the **App registrations** tab, click the newly created application, copy the **Application ID**, and save it. You will need this later.

7. Click **All settings** > **Required permissions** > **Add**.

8. In the **Add API access** pane, do the following:
    1. Click the **Select an API** tab. Click **Microsoft Graph**, and then click **Select**.
    
    2. In the **Select permissions** tab, select the following **application permissions** and set them to **Yes**:
         - **Invite guest users to the organization**
         - **Read and write directory data**
         - **Read and write all users' full profiles**
    
    3. Select the following **delegated permissions** and set them to **Yes**:
         - **Invite guest users to the organization**
         - **Read and write directory data**
         - **Read and write all users' full profiles**
         - **Sign in and read user profile**
     
    4. Click **Select** and **Done**.
    
9. In the **Required permissions** blade, click **Grant Permissions**, and then click **Yes** to assign the permissions.

10. Click **All settings** > **Keys**, and then do the following: 
    1. Enter a name of the key in the **Description** field.
    2. Set the expiration duration in the **Expires** field.
  
11. Click **Save**. Saving the key will display the **Value**. 

    > [!WARNING]
    > Be sure to copy the key **Value** after saving the key. This value will not be available when you leave the blade.

### Configure the B2B invitation service settings

1. Sign in to finance and operations as administrator.

2. Navigate to the **B2B Invitation Configuration** page, and click **Edit**.

3. Select **Enabled**.

4. Verify that the **Tenant ID** is the same as the **Directory ID** (which you noted in step 3 of the previous procedure).

5. In the **Client ID** field, enter the **Application ID** (which you noted in step 6 of the previous procedure).

6. Enter the key **Value**, copied from the above procedure, into the **Application Key** field.

7. **Save** the settings.

Now you can start using the **Provision Microsoft Entra B2B user** workflow task in your workflows to automatically export B2B users to Microsoft Entra ID.


[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
