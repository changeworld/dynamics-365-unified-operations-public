---
title: Invalid users in Dynamics 365 Finance
description: Learn about how to address invalid users in Microsoft Dynamics 365 Finance, including outlines on different types of invalid users.
author: pnghub
ms.author: kkhajuria
ms.topic: how-to
ms.date: 11/08/2024
ms.custom:
ms.reviewer: twheeloc
---

# Invalid users in Dynamics 365 Finance

Users in any Microsoft Dynamics 365 finance and operations environment must comply with Microsoft guidelines to avoid sign-in failures. As of Dynamics 365 Finance version 10.0.39, administrators can use the **Invalid users** page to view details about invalid users.

To view invalid users, follow these steps.

1. Go **System administration** \> **Invalid users**.
2. Select **Refresh**. This page shows a list of users who require attention from the system administrator. If there are no invalid users, the page is blank.

The following sections describe the five types of invalid users that must be addressed.

## Users who aren't found in Microsoft Entra ID

All finance and operations apps users must be present in your Microsoft Entra ID tenant. Administrators can directly add users to your tenant through the Microsoft Entra ID portal. For more information, see [Add or delete users](/entra/fundamentals/add-users).

You can use business-to-business (B2B) functionality to include these users in Microsoft Entra ID. For more information, see [Export business-to-business (B2B) users to Microsoft Entra ID](../../dev-itpro/sysadmin/implement-b2b.md).

## Users whose telemetry ID doesn't match the object ID from Microsoft Entra ID

For sign-in functionality to work correctly, the telemetry ID of a user in finance and operations apps must be aligned with the object ID of the same user in Microsoft Entra ID. If the IDs don't match, we recommend that you delete and then reimport the user. For more information, see [Find the user object ID](/partner-center/find-ids-and-domain-names#find-the-user-object-id).

1. Verify that a user who has the corresponding email address exists in your Microsoft Entra ID.
2. Delete the user from finance and operations apps. Note the user roles before deleting so the roles can be added back after reimporting the users. 
3. Reimport the user. For more information, see [Create new users](create-new-users.md).

If this process is challenging or requires substantial effort, administrators can update the email address on the **Users** page to a different user email that is present in Microsoft Entra ID and change it back to the original email of the user. That change repopulates the object ID for the new email.

## Users whose email address contains an invalid "MAIL#" prefix

Previously, some customers who had trouble signing in were advised to append the prefix "MAIL\#" to their Gmail or Live email address. Because the issue has now been fixed, an administrator must follow these steps to remove the prefix from email addresses.

1. Go to **Users**.
2. Select **Edit** to remove the prefix from the email addresses.

## Users with duplicate telemetry IDs 

Telemetry IDs are unique identifiers for every user. Duplicate telemetry IDs can cause serious security issues, such as user impersonation or inappropriate access levels. It's essential to ensure that each user has a distinct telemetry ID. To ensure compliance, either delete and reimport or edit the affected users to repopulate unique telemetry IDs from Microsoft Entra ID. 

> [!IMPORTANT]
> If three users share the same telemetry ID, and one user has the correct ID, the system flags only the two incorrect users. The user that has the correct ID isn't marked as invalid. 

## Duplicate users 

Duplicate users imply users who have the same email address. This can cause inconsistent behavior due to conflicting roles or settings. You must ensure that every user has a unique email address. 

To make these users compliant, you must delete the duplicates from the **Users** page (**System administration** \> **Users**) and ensure that only one user exists per email address.

### Fix

By selecting **Repair telemetry IDs**, you can have the system automatically fix some user issues. This command performs the following actions:

1. **Repair incorrect telemetry IDs.** The system fixes users that are listed in Microsoft Entra ID, but that have incorrect telemetry IDs in the finance and operations environment.
2. **Handle missing users in Microsoft Entra ID.** If a user isn't listed in Microsoft Entra ID, the system sets their telemetry ID to null. Administrators must add these users to Microsoft Entra ID and run the repair again.
3. **Fix users that have duplicate telemetry IDs.** The system corrects the telemetry ID for the user that is listed in Microsoft Entra ID, and sets it to null for the other users.
4. **Disable duplicate users.** For security reasons, the system disables duplicate users that have the same email address and sets their telemetry ID to null. Administrators must ensure that each user is unique, and must remove duplicates to fix this issue.

After you select **Repair telemetry IDs**, administrators must manually fix any users that remain.

> [!NOTE]
> The **Repair telemetry IDs** command can disable some invalid users and set their telemetry ID to null. As a result, those users are prevented from signing in. Proceed with caution, and fix all the invalid users as soon as possible.
