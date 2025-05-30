---
title: NEWGUID ER function
description: Learn about how the NEWGUID Electronic reporting (ER) function is used, including syntax strings, return values, and examples.
author: kfend
ms.author: filatovm
ms.topic: article
ms.date: 09/09/2021
ms.custom: 
ms.reviewer: johnmichalak
audience: IT Pro
ms.search.region: Global
ms.search.validFrom: 2021-09-08
ms.search.form: ERDataModelDesigner, ERExpressionDesignerFormula, ERMappedFormatDesigner, ERModelMappingDesigner
ms.dyn365.ops.version: AX 10.0.23
ms.assetid: 
---

# NEWGUID ER function

[!include [banner](../includes/banner.md)]

The `NEWGUID` function generates a new globally unique identifier (GUID) and returns it as a *[GUID](er-formula-supported-data-types-primitive.md#guid)* value.

## Syntax

```vb
NEWGUID ()
```

## Return values

*GUID*

The resulting GUID value.

## Example

`NEWGUID()` always returns a new *GUID* value, such as **3afcf7ff-af10-ec11-b6e6-000d3a13209e**.

## Additional resources

[Text functions](er-functions-category-text.md)

[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
