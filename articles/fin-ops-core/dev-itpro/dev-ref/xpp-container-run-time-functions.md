---
title: X++ container runtime functions
description: Learn about the container run-time functions, including a syntax string, a table outlining descriptions for various parameters, and additional values.
author: pvillads
ms.author: pvillads
ms.topic: language-reference
ms.date: 05/19/2025
ms.reviewer: johnmichalak
audience: Developer
ms.search.region: Global
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
---

# X++ container runtime functions

[!include [banner](../includes/banner.md)]

This article describes the container run-time functions.

These functions manipulate the contents of containers.

## conDel
Removes the specified number of elements from a container.

### Syntax

```xpp
container conDel(container container, int start, int number)
```

### Parameters
| Parameter | Description                                                 |
|-----------|-------------------------------------------------------------|
| container | The container to remove elements from.                      |
| start     | The one-based position at which to start removing elements. |
| number    | The number of elements to delete.                           |

### Return value

A new container that doesn't include the removed elements.

### Example

```xpp
static void conDelExample(Args _args)
{
    container c = ["Hello world", 1, 3.14];
    
    // Deletes the first two items from the container.
    c = conDel(c, 1, 2);
}
```

## conFind
Locates the first occurrence of an element in a container.

### Syntax

```xpp
int conFind(container container, anytype element)
```

### Parameters
| Parameter | Description                                              |
|-----------|----------------------------------------------------------|
| container | The container to search.                                 |
| element   | The element to search for. |

### Return value

**0** if the item was not found; otherwise, the sequence number of the item.

### Example

```xpp
static void conFindExample(Args _args)
{
    container c = ["item1", "item2", "item3"];
    int i = conFind(c, "item2");
    int j = conFind(c, "item4");

    print "Position of 'item2' in container is " + int2Str(i);
    print "Position of 'item4' in container is " + int2Str(j);
}
```

## conIns
Inserts one or more elements into a container.

### Syntax

```xpp
container conIns(container container, int start, anytype element, ... )
```

### Parameters

| Parameter | Description                                          |
|-----------|------------------------------------------------------|
| container | The container to insert elements into.               |
| start     | The position to insert elements at.                  |
| element   | One or more elements to insert, separated by commas. |

### Return value

A new container that contains the inserted elements.

### Remarks

The first element of the container is specified by the number **1**. To insert after the n element, the *start* parameter should be n+1. You can also use the **+=** operator to add values of any type to a container. For example, to create a container that contains the squared values of the first 10 loop iterations, use the following code.

```xpp
int i;
container c;

for (i = 1; i < = 10; i++)
{
    // Append the square of the index to the container
    c += i*i;
}
```

### Example

```xpp
static void conInsExample(Args _arg)
{
    container c;
    int i;

    c = conIns(c,1,"item1");
    c = conIns(c,2,"item2");

    for (i = 1 ; i <= conLen(c) ; i++)
    {
        // Prints the content of a container.
        print conPeek(c, i);
    }
}
```

## conLen
Retrieves the number of elements in a container.

### Syntax

```xpp
int conLen(container container)
```

### Parameters

| Parameter | Description                                       |
|-----------|---------------------------------------------------|
| container | The container to count the number of elements in. |

### Return value

The number of elements in the container. The conNull container has no elements.

### Example

```xpp
static void conLenExample(Args _arg)
{
    container c = conins(["item1", "item2"], 1);

    for (int i = 1 ; i <= conLen(c) ; i++)
    {
        print conPeek(c, i);
    }
}
```

## conNull
Retrieves an empty container.

```xpp
container conNull()
```

### Return value

An empty container.

### Example

```xpp
static void conNullExample(Args _arg)
{
    container c = ["item1", "item2", "item3"];

    print "The size of container is " + int2str(conLen(c));

    // Set the container to null.
    c = conNull();
    print "Size of container after conNull() is " + int2Str(conLen(c));
}
```

## conPeek
Retrieves a specific element from a container and converts it into another data type, if conversion is required.

### Syntax

```xpp
anytype conPeek(container container, int number)
```

### Parameters

| Parameter | Description     |
|-----------|-----------------|
| container | The container to return an element from.                         |
| number    | The position of the element to return. Specify **1** to get the first element. An invalid position number, such as **-3**, **0**, or a number that is higher than the length of the container, might cause unpredictable errors. |

### Return value

The element in the container at the position that is specified by the *number* parameter. The **conPeek** function automatically converts the peeked item into the expected return type. Strings can automatically be converted into integers and real numbers, and integers and real numbers can be converted into strings.

### Example

```xpp
static void main(Args _args)
{
    container cnI, cnJ;
    int i, j;
    anytype aty;
    
    info("container cnI ...");
    cnI = ["itemBlue", "itemYellow"];

    for (i=1; i <= conLen(cnI); i++)
    {
        aty = conPeek(cnI, i);
        info(int2str(i) + " :  " + aty);
    }

    info("container cnJ ...");
    cnJ = conIns(cnI, 2, "ItemInserted");

    for (j=1; j <= conLen(cnJ); j++)
    {
        aty = conPeek(cnJ, j);
        info(int2str(j) + " :  " + aty);
    }
}
/***  Output pasted from InfoLog ...
Message (10:20:03 am)
container cnI ...
1 :  itemBlue
2 :  itemYellow
container cnJ ...
1 :  itemBlue
2 :  ItemInserted
3 :  itemYellow
***/
```

## conPoke
Modifies a container by replacing one or more of the existing elements.

### Syntax

```xpp
container conPoke(container container, int start, anytype element, ...)
```

### Parameters

| Parameter | Description                                           |
|-----------|-------------------------------------------------------|
| container | The container to modify.                              |
| start     | The position of the first element to replace.         |
| element   | One or more elements to replace, separated by commas. |

### Return value

A new container that includes the new elements.

### Remarks

The first element of the container is specified by the number **1**.

### Example

```xpp
static void conPokeExample(Args _arg)
{
    container c1 = ["item1", "item2", "item3"];
    container c2;
    int i;

    void conPrint(container c)
    {
        for (i = 1 ; i <= conLen(c) ; i++)
        {
            print conPeek(c, i);
        }
    }

    conPrint(c1);
    c2 = conPoke(c1, 2, "PokedItem");
    print "";
    conPrint(c2);
}
```

[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
