---
title: GS1 bar codes and QR codes
description: Learn how to set up GS1 bar codes and QR codes so that labels can be scanned in a warehouse with an outline on the GS1 bar code format.
author: Mirzaab
ms.author: mirzaab
ms.reviewer: kamaybac
ms.search.form: WHSGS1ParsingSetup, WHSGS1GenericSetup, WHSGS1PolicyTable, WHSWorkUserSession
ms.topic: how-to
ms.date: 06/17/2025
ms.custom: 
  - bap-template
---

# GS1 bar codes and QR codes

[!include [banner](../includes/banner.md)]

Warehouse workers often have to complete several tasks when they use a mobile device scanner to register movements of an item, palette, or container. These tasks can include both scanning bar codes and manually entering information on the mobile device. The bar codes use a company-specific format that you define and manage by using Microsoft Dynamics 365 Supply Chain Management.

GS1 bar codes for shipping labels were developed to provide a global standard for the exchange of data between companies. They're available in both linear (1D) symbologies (bar code formats), such as GS1-128, and 2D symbologies, such as GS1 DataMatrix and GS1 QR codes. GS1 bar codes not only encode data but also let you use a predefined list of *application identifiers* to define the meaning of that data. The GS1 standard defines the data format and the various kinds of data that it can be used to encode. Unlike older bar code standards, GS1 bar codes can have multiple data elements. Therefore, a single bar code scan can capture several types of product information, such as the batch and the expiration date.

GS1 support in Supply Chain Management dramatically simplifies the scanning process in warehouses where pallets and containers are labeled by using bar codes in GS1 format. Warehouse workers can extract all the required information through a single scan of a GS1 bar code. By eliminating the need to do multiple scans and/or manually enter information, GS1 bar codes help reduce the time that is associated with tasks. At the same time, they also help improve accuracy.

Logistics managers must set up the required list of application identifiers and associate each of them with the appropriate mobile device menu items. The application identifiers can then be used across warehouses as a global setting for moving and packing purposes. Therefore, all shipping labels take a unified form.

Unless otherwise stated, this article uses the term *bar code* to refer to both linear (1D) bar codes and 2D bar codes.

## The GS1 bar code format

The GS1 General Specifications specify which symbologies can be used for GS1 bar codes and how to encode the data in the bar code. This section provides a short introduction to the article. For full details, see the [GS1 General Specifications](https://www.gs1.org/docs/barcodes/GS1_General_Specifications.pdf) published by GS1. The GS1 specifications document is regularly updated, and the information that it provides is up to date with GS1 General Specifications release 22.0.

GS1 bar codes use the following symbologies:

- **Linear or 1D bar codes** – GS1-128 and GS1 DataBar
- **2D bar codes** – GS1 DataMatrix, GS1 QR Code, and GS1 Dotcode

GS1 is mentioned in GS1-128, which is a special case of the ordinary Code-128 linear bar code, GS1 DataMatrix, and GS1 QR Code. The difference between the GS1 version and the non-GS1 version is the presence of a special character (FNC1) as the first character in the bar code data. The presence of an FNC1 character indicates that the data in the bar code should be interpreted according to the GS1 specification.

The data in the bar code itself consists of multiple data elements, each of which is identified by an application identifier at the start of the field. Usually, the data is also presented under the bar code in a human-readable format, where the application identifier is shown in parenthesis. Here's an example: `(01) 09521101530001 (17) 210119 (10) AB-123`. This bar code contains three elements:

- **Application identifier 01** – The GS1 global trade item number (GTIN) of the item.
- **Application identifier 17** – The expiration date.
- **Application identifier 10** – The batch number.

For each element, the data might have either a predefined length or a variable length. There's a fixed list of application identifiers that have predefined lengths. All other application identifiers have variable length, and the GS1 application identifier list specifies the maximum length and format of data. For example, application identifier 01 has a predefined length of 16 characters (two for the application identifier itself and then 14 for the GTIN), and application identifier 17 has a predefined length of eight characters (two for the application identifier itself and then six for the date). However, application identifier 10 has two numbers for the application identifier itself and then up to 20 alphanumeric characters.

When elements are put together, if an element follows a variable length element, a separator character must be used. This separator can be either the special FNC1 character or the group separator character (a nonprintable character that has ASCII code 29 and hexadecimal code 1D). The separator shouldn't be used after the last element. Although the separator also shouldn't be used after elements that have predefined length, its presence isn't a critical error.

In the bar code data from the previous example of a bar code that contains application identifiers 01, 17, and 10, the data in a Code-128, QR Code, or DataMatrix symbol will be encoded as `<FNC1>`**`01`**`09521101530001`**`17`**`210119`**`10`**`AB-123` (application identifiers are shown in bold). As a best practice, any element that has variable length should be put at the end, to eliminate the need for an extra group separator character. However, the bar code can also have a different order of elements, where the separator is mandatory. Here's an example: `<FNC1>`**`01`**`09521101530001`**`10`**`AB-123<GS>`**`17`**`210119`.

### Dates and decimal numbers

Dates are always represented in *YYMMDD* format, where the century of the year is determined by GS1 specifications. Only dates from 49 years in the past to 50 years in the future (relative to the current year) can be represented.

Some data elements contain decimal numbers. For example, application identifiers 3100, 3101, ... 3105 represent a net weight in kilograms. Because these application identifiers have a predefined length of 10, six numbers are available for the quantity. The position of the decimal point is specified by the last number of the application identifier. Therefore, this family of application identifiers can also be represented as *310n*. Because the GS1 standard specifies that there must always be at least one number to the left of the decimal point, a maximum of five decimal places is allowed.

Here are a few examples that show how the number *123456* will be interpreted by different application identifiers (shown in bold):

- **`3100`**`123456` &rarr; 123456 (integer)
- **`3101`**`123456` &rarr; 12345.6 (one decimal place)
- **`3102`**`123456` &rarr; 1234.56 (two decimal places)
- **`3103`**`123456` &rarr; 123.456 (three decimal places)
- **`3104`**`123456` &rarr; 12.3456 (four decimal places)
- **`3105`**`123456` &rarr; 1.23456 (five decimal places)

## Scanning GS1 bar codes in Supply Chain Management

To scan GS1 bar codes, warehouse workers use a scanner that is built into or connected to a mobile device. The scanner then transmits the scanned bar code to the Warehouse Management mobile app as a series of keyboard events. This mode of operation is also known as a *keyboard wedge* or *wedge*. The mobile app then sends the received text as-is to Supply Chain Management. When the system receives input data, it first determines whether the data begins with one of the configured prefixes that indicate that the data is actually a GS1 bar code (see the [Set up global GS1 options](#set-gs1-options) section). If the scanned data does begin with one of those prefixes, the system uses a GS1 parser to parse the data and extract individual data elements according to their application identifiers. After the data has been parsed, either the current input field or multiple fields will be filled in with the scanned data.

### Configuration of bar code scanner hardware and software

For Supply Chain Management to correctly recognize and decode GS1 bar codes, the hardware scanner or supporting software must be configured to perform the following actions:

- Add a prefix to the scanned bar codes, so that the system can recognize a GS1 bar code.
- Convert the nonprintable ASCII group separator character (ASCII code 29 or hexadecimal code 1D) to a printable character, such as a tilde (~).

Although you can add any prefix to the scanned bar code, one option is to add an ISO/IEC 15424 symbology identifier, also known as an *AIM identifier*. This three-character identifier starts with `]`, then has one character that identifies the symbology that is used, and then has a number that is used as a further modifier. For example, the AIM identifier `]C1` specifies a Code 128 bar code (because of the character `C`), and the modifier `1` specifies that there's an FNC1 character in the first position of the data. On the other hand, `]C0` is a Code 128 bar code that has any other character as the first character of the data.

The following five symbology identifiers correspond to GS1 bar codes that have application identifier elements:

- `]C1` – Code 128 (`C`) with FNC1 character in first position (`1`), also known as GS1-128.
- `]e0` – GS1 DataBar.
- `]d2` – DataMatrix (`d`) with ECC 200 and FNC1 in first position (`2`), also known as GS1 DataMatrix.
- `]Q3` – QR Code (`Q`) Model 2 symbol with FNC1 in first position (`3`), also known as GS1 QR Code.
- `]J1` – GS1 DotCode.

If you use these identifiers, compatibility with non-GS1 bar codes requires that the scanners or scanning software be configured to remove any identifiers that don't correspond to the GS1 identifiers. For example, if you scan a "normal" Code 39 bar code, the prefix `]A0` will be added. Because the system won't understand this prefix as one of the GS1 prefixes, it will interpret it as data and produce unexpected results.

> [!NOTE]
> For convenience, version 2.0.17.0 and later of the Warehouse Management mobile app will remove any AIM prefixes that aren't included in the previous list. This behavior supports cases where you can configure the scanner to add the AIM prefix but not to remove the unwanted prefixes.

### Single and multiple field scanning

After the data has been parsed from the bar code, it will be fed into the mobile device flow controls. There are two methods that will be processed in turn:

- **Single field scanning** – This method fills in only the field that the bar code was scanned into. For example, if you scan the bar code `<FNC1>`**`01`**`09521101530001`**`17`**`210119`**`10`**`AB-123` while the cursor is in the **Item** field, the GTIN `09521101530001` from the bar code will be entered in that field. If you scan the same bar code while the cursor is in the **Batch ID** field, the batch number `AB-123` from the bar code will be entered. This mode works for all fields in all flows and requires only that the generic bar code data setup be configured. If a bar code contains multiple elements, it must still be scanned multiple times, because only one piece of the bar code at a time will be entered into the mobile device flow. This behavior is controlled by the generic bar code data setup, as described in the [Establish the generic bar code data setup](#generic-gs1-setup) section.
- **Multiple field scanning** – This method fills in multiple fields when one bar code is scanned, by pushing additional data into the mobile device flow state. For example, the policy is configured to push application identifier 01 into the `ItemId` control and application identifier 10 into the `InventBatchId` field. In this case, if you scan the bar code `<FNC1>`**`01`**`09521101530001`**`17`**`210119`**`10`**`AB-123`, data for both variables will be pushed at the same time. Therefore, the system won't prompt you for the item and/or batch number in the flow. This behavior is controlled by bar code data policies that are linked to menu items, as described in the [Set up bar code data policies for mobile device menu items](#policies-for-menus) section.

> [!WARNING]
> The default bar code data policies have been tested to work without unexpected behavior. However, customization of bar code data policies that are linked to menu items can cause unexpected behavior, because the flow might not expect some data to be available at a particular time.

## Turn on GS1 features for your system

To use GS1 bar codes, the *Scan GS1 barcodes* feature must be turned on for your system. As of Supply Chain Management version 10.0.32, this feature is mandatory and can't be turned off. If you're running a version older than 10.0.32, then admins can turn this functionality on or off by searching for the *Scan GS1 barcodes* feature in the [**Feature management** workspace](../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md).

If you use GS1 bar codes, we recommend that you also turn on the *Enhanced parser for GS1 barcodes* feature. (As of Supply Chain Management version 10.0.32, this feature is turned on by default. As of Supply Chain Management version 10.0.36, this feature is mandatory and can't be turned off.) This feature provides an improved implementation of the GS1 bar code parser. It adds the following improvements:

- It follows the GS1 General Specification algorithm for symbol data parsing and validates that the data in the symbol is valid according to the specification.
- It doesn't require that you set up a **Maximum length of identifier** value and uses longest prefix matching from configured application identifiers.
- It lets you more easily configure decimal application identifiers by using the letter *n* to match any number. For example, you can configure just one application identifier (*310n*) instead of separate application identifiers (*3101*, *3102*, *3103*, and so on).
- It fixes an issue where incorrectly encoded data is interpreted as field data.
- It comes as a separate class that can be reused in other contexts and enables an extensibility point to be used to manipulate scanned data before the flow fields are filled in.

## <a name="set-gs1-options"></a>Set up global GS1 options

The **Warehouse management parameters** page provides a few settings that establish global GS1 options.

To set up global GS1 options, follow these steps.

1. Go to **Warehouse management \> Setup \> Warehouse management parameters**.
1. On the **General** tab, on the **Bar codes** FastTab, set the following fields:

    - **FNC1 Character**, **Datamatrix character**, and **QR code character** – Specify characters that should be interpreted as a prefix for each type of GS1 bar code.
    - **Group separator** – Specify the character that replaces the ASCII group separator character.
    - **Maximum length of identifier** – Specify the maximum number of characters that is permitted for the application identifier. This field isn't required if the *Enhanced GS1 Parser* feature is turned on for your system.
    - **Unknown application identifier policy** – Select one of the following values to specify what the system should do if it encounters an unknown application identifier when it parses a GS1 bar code:

        - *Error* – The system will report an error and won't scan any part of the bar code. To scan this type of bar code, you must add a matching entry in the GS1 application identifier table.
        - *Skip the data element* – The system will continue to parse the bar code without reporting an error or a warning. The data from the unknown application identifier won't be available to the application for further processing.

> [!NOTE]
> Prefixes tell the system that a bar code is encoded according to the GS1 standard. Up to three prefixes (**FNC1 Character**, **Datamatrix character**, and **QR code character**) can be used simultaneously and for various purposes.

## Bar code data application identifiers

GS1 formats not only encode the data but also let you use a predefined list of application identifiers to define the meaning of the data. Logistics managers must set up the required list of application identifiers and associate each of them with the appropriate mobile device menu items. The identifiers can then be used across warehouses as a global setting for moving and packing purposes. Therefore, all shipping labels will take a unified form.

The system uses the data, especially the predefined application identifiers, to establish the rules that should be applied to the relevant piece of scanned information.

Each application identifier signals to the system that subsequent characters in the scanned bar code should be considered a block of encrypted information. The setup of the application identifiers defines how the system should interpret a bar code and save it as a value in the system.

Logistics managers can use standard international application identifiers and/or create their own.

### Load the standard application identifiers

To get started quickly, you can load a list of common international application identifiers. You can then extend or edit the list later, as you require.

To load the standard application identifiers, follow these steps.

1. Go to **Warehouse management \> Setup \> GS1 \> Barcode data application identifiers**.
1. On the Action Pane, select **Create default setup**.

> [!WARNING]
> The **Create default setup** command deletes all currently defined application identifiers and replaces them with the standard list. However, after you load the default setup, you can customize the list as you require.

### Set up custom application identifiers

If some or all application identifiers that your company uses differ from the standard set, you can create your own codes from scratch or customize the standard set as you require.

To set up and customize your GS1 own application identifiers, follow these steps.

1. Go to **Warehouse management \> Setup \> GS1 \> Barcode data application identifiers**.
1. Follow one of these steps:

    - To create a new identifier: On the Action Pane, select **New**.
    - To edit an existing identifier: Select the identifier, and then, on the Action Pane, select **Edit**.

1. Set the following fields for the new or selected identifier:

    - **Application identifier** – Enter the identification code for the application identifier. Typically, this code is a two-digit integer, but it can be longer. For decimal values, the last digit indicates the number of decimal places. For more information, see the description of the **Decimal** checkbox later in this list. If the *Enhanced parser for GS1 barcodes* feature is enabled, you can create a single application identifier for all decimal place variants by using the letter *n* as the last character in the application identifier. For example, you can configure just one application identifier (*310n*) instead of a separate application identifier for each number of decimal places (*3101*, *3102*, *3103*, and so on).
    - **Description** – Enter a short description of the identifier.
    - **Fixed length** – Select this checkbox if values that are scanned by using this application identifier have a fixed number of characters. Clear this checkbox if the length of values is variable. In this case, you must indicate the end of the value by using the group separator character that you specified on the **Warehouse management parameters** page.
    - **Length** – Enter the maximum number of characters that can appear in the values that are scanned by using this application identifier. If the **Fixed length** checkbox is selected, exactly this number of characters is expected.
    - **Type** – Select the type of value that is scanned by using this application identifier (*Numeric*, *Alphanumeric*, or *Date*). For more information about how dates and numbers are represented in bar code data, see the [Dates and decimal numbers](#dates-and-decimal-numbers) section.
    - **Decimal** – Select this checkbox if the value includes an implied decimal point. If this box is selected, the system will use the last digit of the application identifier to determine the number of decimal places. For more information about how dates and numbers are represented in bar code data, see the [Dates and decimal numbers](#dates-and-decimal-numbers) section.

> [!WARNING]
> Although the system will allow you to set the **Fixed length** checkbox for any application identifier, it should be used only for the subset of application identifiers that have a predefined length per the GS1 General Specifications. The enhanced GS1 parser already contains the list of all application identifiers that have predefined lengths.

> [!NOTE]
> The **Group separator** value that is specified on the **Warehouse management parameters** page is optional if a value that is followed by an application identifier has a fixed length.

## <a name="generic-gs1-setup"></a>Establish the generic bar code data setup

The generic bar code data setup establishes a collection of common mappings. These mappings match each relevant input field in the mobile app to the application identifier that controls how values from scanned bar codes should be interpreted and stored in that field. By default, these settings apply to all scans for all mobile device menu items. However, they can be overwritten for one or more specific fields by a bar code data policy that is assigned to a specific menu item.

The generic bar code data setup allows only one value to be scanned at a time. Therefore, if you want to load multiple field values from a single scan, you must set up a bar code data policy for the relevant menu items.

For more information about bar code data policies, see the next section.

### Load the standard generic bar code data setup

The **Barcode data generic setup** page lets you load a standard set of mappings between mobile device fields and standard application identifiers that are created by the default setup.

To establish the generic bar code data setup, go to **Warehouse management \> Setup \> GS1 \> Barcode data generic setup**. Then select **Create default setup** to automatically assign a suitable application identifier to each field that is typically used by mobile device menu items.

> [!WARNING]
> If any generic bar code data setup already exists, the **Create default setup** command completely deletes it and loads the standard setup.

### Customize the standard generic bar code data setup

To customize the generic bar code data setup, follow these steps.

1. Go to **Warehouse management \> Setup \> GS1 \> Barcode data generic setup**.
1. Follow one of these steps:

    - To create a new mapping: On the Action Pane, select **New**.
    - To edit an existing mapping: Select the mapping, and then, on the Action Pane, select **Edit**.

1. Set the following fields for the new or selected mapping:

    - **Field** – Select or enter the mobile app input field that the incoming value should be assigned to. The value isn't the display name that workers see. Instead, it's the key name that is assigned to the field in the underlying code. The default setup provides a collection of fields that are likely to be useful, and includes intuitive key names for each field and matching programmed functionality. However, you might have to talk to your development partners to find the correct selections for your implementation.
    - **Application identifier** – Select the applicable application identifier, as defined on the **Barcode data application identifiers** page. The identifier establishes how the bar code will be interpreted and stored as a value for the named field. After you select an application identifier, the **Description** field shows the description of it.

## <a name="policies-for-menus"></a>Set up bar code data policies for mobile device menu items

The purpose of the GS1 standard is to enable workers to load several values when they scan a single bar code one time. To achieve this purpose, logistics managers must set up bar code data policies that tell the system how to interpret multi-value bar codes. Later, you can assign policies to mobile device menu items to control how a bar code will be interpreted when workers scan it while they're using a specific menu item.

If no bar code data policy is assigned to a menu item, the system can capture only a single value. This value is applied to the mobile app input that is selected when the worker takes the scan, as specified by the generic bar code data setup. If a bar code data policy is assigned to the menu item, the system still uses the generic bar code data setup to map the first bar code value to the selected field. However, it can then capture additional field values, as specified by the applicable policy.

### Load the standard specific bar code data policies

To get started quickly, you can load a set of standard bar code data policies. You can then extend or edit the policies later, as you require.

To load the standard application identifiers, follow these steps.

1. Go to **Warehouse management \> Setup \> GS1 \> Barcode data policy**.
1. On the Action Pane, select **Create default setup**.

> [!WARNING]
> The **Create default setup** command deletes all currently defined policies and replaces them with the standard set of policies. However, after the default setup is loaded, you can customize the policies as you require.

### Set up custom specific bar code data policies

> [!WARNING]
> Some bar code data policies might not work with every mobile flow that you use. When you configure custom bar code data policies, you must test the mobile device flow by using different pieces of information that are scanned at different points in the flow. In this way, you can determine whether the flow behaves as you expect.

To set up and customize your bar code data policies, follow these steps.

1. Go to **Warehouse management \> Setup \> GS1 \> Barcode data policy**.
1. Follow one of these steps:

    - To create a new policy: On the Action Pane, select **New**.
    - To edit an existing policy: Select the policy in the list pane.

1. On the header of the new or selected policy, set the following fields:

    - **Policy name** – Enter a name for the policy.
    - **Description** – Enter a short description of the policy.
    - **Field value capturing method** – Select one of the following values to specify how the individual bar code values should be handled as part of the mobile device flow:

        - *Process immediately* – The application identifier values will immediately be passed to the next mobile device step, even though the recorded values aren't required for capture as part of a later mobile device step. Depending on the recorded values, this value can cause unexpected mobile device flow processing.
        - *Save as default* – The application identifier values will be stored throughout the whole mobile device menu item flow and will be used only in mobile device steps that require the defined fields. Therefore, the exact mobile device step field control names must be specified as part of the bar code data policy setup, to link the application identifier values from the bar codes to the Warehouse Management mobile app fields. For more information about how to find the correct field names, see [Inspect details of active Warehouse Management mobile app sessions](work-user-sessions.md).

    - **Auto submit** – This option is available only when the **Field value capturing method** field is set to *Save as default*. Set it to *Yes* to automatically submit the mobile device step if all the fields are set.

1. On the **Policy lines** FastTab, map field names to application identifiers as required for the current policy. Use the buttons on the toolbar to add or remove rows as you require. For each row, set the following fields:

    - **Field** – Select or enter the mobile app input field that the incoming value should be assigned to. The value isn't the display name that workers see. Instead, it's the key name that is assigned to the field in the underlying code. The default setup provides a collection of fields that are likely to be useful, and includes intuitive key names for each field and matching programmed functionality. However, you might have to talk to your development partners to find the correct selections for your implementation. For more information about how to look up field names, see [Inspect details of active Warehouse Management mobile app sessions](work-user-sessions.md).
    - **Application identifier** – Select the applicable application identifier, as defined on the **Barcode data application identifiers** page. The identifier establishes how the bar code will be interpreted and stored as a value for the named field. After you select an application identifier, the **Description** field shows the description of it.
    - **Sorting** – This column is available only when the **Field value capturing method** field is set to *Process immediately*. Every multi-value bar code includes a series of application identifiers, each of which is followed by a value. The applicable bar code data policy identifies which application identifier is mapped to each database field. However, if a bar code uses the same application identifier more than once, the system uses the order in which application identifiers appear in the code to map them to fields. For rows that share an application identifier with one or more other rows, use this field to establish the order that the matching rows should be processed in. The row that has the lowest sorting value will be processed first.
    - **Allow overwriting** – This column is only available on the **Policy lines** grid when **Field value capturing method** in the policy details header is set to *Save as default*. Select the checkbox in the **Policy lines** grid for rows where scanned data should replace the default data related to the specified **Application identifier** in the system. Only field values that are enabled for editing in the mobile application step will be overwritten when this option is selected.

> [!NOTE]
>
> - For bar codes that include more than one identical application identifier, you *must* use the **Sorting** field to establish the order of the fields.
> - When **Auto Submit** is set to *Yes*, the mobile device immediately sends scanned information to the system. After the information is received, the mobile device displays a new screen, ready for the next input. This feature allows for a quick and efficient scanning process. The device only displays data after scanning when user interaction is required.
> - Select the **Allow overwriting** checkbox for rows where scanned information should replace the default data in the system. For example, if there's a purchase order for 10 pieces, but you only need to scan 5 pieces, this option will allow the scanned data to override the default quantity.

## Assign bar code data policies to mobile device menu items

By default, all mobile device menu items provide input fields where workers can scan a single value, according to the generic bar code data setup. If you want workers to be able to scan more than one field value in a single scan for any mobile device menu item, you must assign a bar code data policy by following these steps.

1. Go to **Warehouse management \> Setup \> Mobile device \> Mobile device menu items**.
1. Create or open a menu item.
1. On the **General** FastTab, set the **Barcode data policy** field to the policy that applies to the menu item.

## GS1 setup example

This example applies to a system where the GS1 options are set up in the following way:

- On the **Warehouse management parameters** page, the following global settings are established:

    - **FNC1 character:** *\]C1*
    - **Group separator:** *\~*

- On the **Barcode data application identifiers** page, the following application identifiers are relevant to this example.

    | Application identifier | Description | Fixed length | Length | Type | Decimal |
    |---|---|---|---|---|---|
    | 01 | GTIN | Selected | 14 | Numeric | Cleared |
    | 10 | Batch number | Cleared | 20 | Alphanumeric | Cleared |
    | 17 | Expiry date | Selected | 6 | Date | Cleared |
    | 30 | Receiving quantity | Cleared | 8 | Numeric | Cleared |

- On the **Barcode data generic setup** page, the following settings for the generic bar code data policy are relevant to this example.

    | Field | Application identifier | Description |
    |---|---|---|
    | ItemId | 01 | GTIN |

- On the **Barcode data policy** page, there's policy where the **Policy name** field is set to *Purchase receiving*. This policy includes the following lines.

    | Field | Application identifier | Description | Sorting |
    |---|---|---|---|
    | ExpDate | 17 | Expiry date | 0 |
    | InventBatchId | 10 | Batch number | 0 |
    | Qty | 30 | Receiving quantity | 0 |

- On the **Mobile device menu items** page, there's a menu item that is named *Purchase receiving*. Its **Barcode data policy** field is set to *Purchase receiving*.

After goods for a purchase order arrive at the warehouse, the worker follows these steps.

1. On the mobile device, select the **Purchase receiving** menu item.
1. Enter the purchase order number.
1. Select the **Item** field, and scan the following bar code: `]C10100000012345678~3030~10b1~17220215`.

Because of the settings that are established for this example, the system parses the scanned bar code in the following way.

| Field key | Application ID | Value | Note |
|---|---|---|---|
| ItemId | 01 | 00000012345678 | Because the worker scanned to the **Item** field, the first value in the bar code is mapped to that field. The mapping is taken from the generic bar code data setup. |
| Qty | 30 | 30 | Because several field values are being captured in a single scan, this mapping and all remaining mappings are taken from the bar code data policy that is assigned to the **Purchase receiving** menu item. This value is the quantity that was received. |
| InventBatchId | 10 | b1 | This value is the batch ID. |
| ExpDate | 17 | 220215 | The date format is YYMMDD. Therefore, the expiry date is February 15, 2022. |

The receipt is then registered, and the relevant database values are entered after the single scan.

> [!TIP]
> If GS1 bar codes that contain multiple values don't work as part of a Warehouse management mobile app flow, check the following settings:
>
> - On the **Barcode data generic setup** and **Barcode data application identifiers** pages, make sure that the settings are aligned with the bar codes that you're using and with the bar code data policy that's assigned on the **Mobile device menu item** page.
> - On the **Barcode data policy** page, select the policy that you're having trouble with, and check the following settings:
>
>    - Set the **Field value capturing method** field to *Save as default*.
>    - In the grid, make sure that all the field names are aligned with the step ID input control names for the actual mobile device. For more information about how to look up field names, see [Inspect details of active Warehouse Management mobile app sessions](work-user-sessions.md). For some typical examples, see the table after this list.
>
> - On the **Warehouse management parameters** page, on the **General** tab, on the **Bar codes** FastTab, set the **Unknown application identifier policy** field to *Skip the data element*.
>
> The following table shows some typical examples where the step ID field mapping fails, so that a scanned GS1 bar code can't be processed.
>
> | Used field name | Correct field name  | Process                   |
> |-----------------|---------------------|---------------------------|
> | ItemId          | ProductConfirmation | Item confirmation step    |
> | CatchWeight     | OutboundWeight      | Catch weight picking step |
