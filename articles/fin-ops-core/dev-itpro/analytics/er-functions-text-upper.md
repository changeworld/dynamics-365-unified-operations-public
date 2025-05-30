---
title: UPPER ER function
description: Learn about how the UPPER Electronic reporting (ER) function is used, including syntax strings, arguments, return values, and examples.
author: kfend
ms.author: filatovm
ms.topic: article
ms.date: 12/05/2019
ms.reviewer: johnmichalak
audience: IT Pro
ms.search.region: Global
ms.search.validFrom: 2016-02-28
ms.search.form: ERDataModelDesigner, ERExpressionDesignerFormula, ERMappedFormatDesigner, ERModelMappingDesigner
ms.dyn365.ops.version: AX 7.0.0
ms.assetid: 24223e13-727a-4be6-a22d-4d427f504ac9
---

# UPPER ER function

[!include [banner](../includes/banner.md)]

The `UPPER` function returns the specified text string as a *String* value after it has been converted to uppercase letters.

## Syntax

```vb
UPPER (text )
```

## Arguments

`text`: *String*

The valid path of a data source of the *String* type.

## Return values

*String*

The resulting text value.

## Example

`UPPER ("Sample")` returns **"SAMPLE"**.

## Additional resources

[Text functions](er-functions-category-text.md)


[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
