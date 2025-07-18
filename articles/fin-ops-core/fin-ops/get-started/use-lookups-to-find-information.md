---
title: Find information by using lookups
description: Learn about lookup features and will receive some helpful tips to get the optimal use out of lookups in the system.
author: jasongre
ms.author: jasongre
ms.topic: article
ms.custom: 
  - bap-template
  - evergreen
ms.reviewer: johnmichalak
ms.date: 01/23/2025
ms.update-cycle: 1095-days
ms.search.region: Global
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.assetid: f20cbd2c-14e0-47e7-b351-8e60d3537f96
---

# Find information by using lookups

[!include [banner](../includes/banner.md)]

Many fields have lookups that can help you easily find the correct or desired value. Several enhancements have been added to lookups that make these controls more usable and make users more productive. In this article, you will learn about these new lookup features and receive some helpful tips to get the optimal use out of lookups in the system.

## Responsive lookups

In previous versions, when interacting with a lookup control, users would have to take an explicit action to open the drop-down menu. This may have been by typing an asterisk (\*) in the control to filter the lookup based on the current value of the control, clicking the drop-down button, or by using the **Alt**+**Down arrow** keyboard shortcut. Lookup controls have been modified in the following ways to better align with current web practices:

- Lookup drop-down menus now open automatically after a slight pause in typing, with the drop-down menu contents filtered based on the lookup control's value.

    Note that the old behavior of automatic opening of the dropdown after typing an asterisk (\*) has been deprecated.

- After the lookup drop-down menu has opened, the following occurs:

    - The cursor stays in the lookup control (instead of focus moving into the drop-down menu) so you can continue to make modifications to the control's value. However, the user can still use the **Up arrow** and **Down arrow** to change rows in the drop-down menu, and enter to select the current row in the drop-down menu.
    - The contents of the drop-down menu adjusts after any modifications are made to the lookup control's value.

For example, consider a lookup field called **City**.

When focus is in the **City** field, you can start looking for the city that you want by typing a few letters, like "col." After you stop typing, the lookup will open automatically, filtered to those cities that begin with "col".

At this point, the cursor is still in the lookup field. If you continue typing so the value is "colum," the lookup contents adjust automatically to reflect the latest value in the control.

Even though focus is still in the lookup control, you can also use the **Up arrow** or **Down arrow** keys to highlight the row that you want to select. If you press **Enter** the highlighted row will be selected from the lookup and the control's value will be updated.


## Typing in more than IDs

When entering data, it's natural for users to attempt to identify an entity, such as a customer or vendor, in terms of the name rather than an identifier representing the entity. Many (but not all) lookups now allow contextual data entry. This powerful feature allows the user to type the ID or the corresponding name into the lookup control.

For example, consider the **Customer account** field when creating a sales order. This field shows the **Account ID** for the customer, but a user would typically prefer to enter an **Account name** instead of an **Account ID** for this field when creating a sales order, such as "Forest Wholesales" instead of "US-003."

If the user started to enter an **Account ID** into the lookup control, the drop-down menu would automatically open as described in the previous section.

However, the user can now enter the beginning of an **Account name** as well. If this is detected, the **Name** column is moved to be the first column in the lookup, and the lookup is sorted and filtered based on the **Name** column.

## Using grid column headers for more advanced filtering and sorting

The lookup enhancements discussed in the previous two sections greatly improve a user's ability to navigate the rows in a lookup based on a "begins with" search of the **ID** or **Name** field in the lookup. However, there are situations in which more advanced filtering (or sorting) is needed to find the correct row. In these situations, the user needs to use the filtering and sorting options in the grid column headers inside the lookup. For example, consider an employee entering a sales order line who needs to locate the right "cable" as the product. Typing "cable" into the **Item number** control isn't helpful, as there are no product names that begin with "cable."

Instead, the user needs to clear the value of the lookup control, open the lookup drop-down menu, and filter the drop-down menu using the grid column header. A mouse (or touch) user can simply click (or touch) any column header to access the filtering and sorting options for that column. For a keyboard user, the user simply needs to press **Alt**+**Down** **arrow** a second time to move focus into the drop-down menu, after which the user can tab to the correct column, and then press **Ctrl**+**G** to open the grid column header drop-down menu.

After the filter has been applied, the user can find and select the row as usual.



[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
