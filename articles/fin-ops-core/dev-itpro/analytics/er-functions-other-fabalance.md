---
title: FA_BALANCE ER function
description: Learn about how the FA_BALANCE Electronic reporting (ER) function is used, including syntax strings, arguments, return values, and examples.
author: kfend
ms.author: filatovm
ms.topic: reference
ms.date: 12/17/2019
ms.reviewer: johnmichalak
audience: IT Pro
ms.search.region: Global
ms.search.validFrom: 2016-02-28
ms.search.form: ERDataModelDesigner, ERExpressionDesignerFormula, ERMappedFormatDesigner, ERModelMappingDesigner
ms.dyn365.ops.version: AX 7.0.0
ms.assetid: 24223e13-727a-4be6-a22d-4d427f504ac9
---

# FA_BALANCE ER function

[!include [banner](../includes/banner.md)]

The `FA_BALANCE` function returns a *Container (record)* value that consists of data for the fixed asset balance for the specified fixed asset item, value model code, reporting year, and reporting date.

## Syntax

```vb
FA_BALANCE (fixed asset code, value model code, reporting year, reporting date)
```

## Arguments

`fixed asset code`: *String*

A *String* value that represents the code of a fixed asset item that the balance is calculated for.

`value model code`: *String*

A *String* value that represents the code of a value model that the balance is calculated for.

`reporting year`: *Enumeration value*

An enumeration value of the **AssetYear** application enumeration that defines a period for the balance calculation.

`reporting date`: *Date*

A *Date* value that defines a date for the balance calculation.

## Return values

*Container (record)*

The resulting record value.

## Example

`FA_ BALANCE ("COMP-000001", "Current", AxEnumAssetYear.ThisYear, SESSIONTODAY ())` returns the data container of balances for fixed asset **COMP-000001** that has been prepared for the **Current** value model on the current application session date.

## Additional resources

[Other (business domain–specific) functions](er-functions-category-other.md)


[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
