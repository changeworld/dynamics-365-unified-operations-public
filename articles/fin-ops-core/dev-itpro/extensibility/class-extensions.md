---
title: Class extension model in X++
description: Learn about the class extension model in X++, including overviews on the effective class concept and extension class variations.
author: pvillads
ms.author: pvillads
ms.topic: how-to
ms.custom: 
  - bap-template
ms.date: 02/03/2025
ms.reviewer: johnmichalak
ms.search.region: Global
ms.search.validFrom: 2016-05-31
ms.dyn365.ops.version: Platform update 1
ms.assetid: 271dabb1-ecb8-497f-b866-397733a954b8
---

# Class extension model in X++

[!include [banner](../includes/banner.md)]

This article describes the class extension model in X++.

Extension is a term used for features that let you extend existing artifacts in a new model. There are rich ways to extend both the X++ code and metadata. This article describes how X++ code can be extended and add methods and state to artifacts defined in other models without recompiling those models. 

A similar code extension mechanism already exists for X++ and is modeled after the corresponding feature in C\#. This extension mechanism allows a class to be designated as an extension class through a naming convention and by hosting public static methods. These classes are a programming utility concept that allows you to add methods to existing types, namely the type of the first parameter to the extension method. In this way, the method is "extending" the new class with a method that it didn't originally have. This article describes the next step that offers a more capable and natural extension story. In object-oriented programming, the term *extend* has a well-defined meaning. When we say, "class B extends class A," we mean that B inherits from A, that A is B's parent class, and the usual object-oriented rules are implied. This term in X++ syntax is used in class declarations to express this relationship. The term *extension* can describe metadata that has contributions from several models. *Class augmentation* is used to designate the relationship between a class A in a base model and a class B in a model that depends on it. Where B provides additional functionality to class A in the context of that model. We'll continue to use the term *extension class*, because it's so prevalent.

## The effective class concept
It's useful to have a term for a class that consists of the public members of the augmented artifact and all the public members of all the class extensions that augment that artifact. This class is called the effective class in a given model. The following illustration shows an artifact, **MyArtifact**, that is defined in a base model, **MyModel**, and two dependent models that have extension classes for **MyArtifact**.

[![Artifact MyArtifact that is defined in base model MyModel, and two dependent models that have extension classes for MyArtifact.](./media/extensions-11.png)](./media/extensions-11.png)

In this example, the effective class is the class in the extension models that contains all the original methods and all the public artifacts from the extension classes. The effective class isn't the same in every model because it includes only the class extensions that are defined in a given model. The following illustration shows the effective class of **MyArtifact** in the **MyExtensionModel** model.

[![Effective class of MyArtifact in MyExtensionModel.](./media/extensions-21.png)](./media/extensions-21.png)

Class extensions are described by using a class that is named **MyClass** in a model that is named **MyModel**.

```xpp
class MyClass
{
    public int mycState;
    public str mycMethod(int _arg)
    {
        // ...
    }
}
```

We can add new methods and state to **MyClass** by introducing an extension class in the extension model (**MyExtensionModel**) that builds on top of (that is, has a dependency on) **MyModel**.

## Extension class declarations
Extension classes are final classes that are adorned with the **ExtensionOf** attribute and that also have a name that has the **\_Extension** suffix. The name of the extension class is otherwise unimportant, but be consistent with your best practices. The class augments the artifact that is specified in the parameter of the **ExtensionOf** attribute, as shown in the following example.

```xpp
[ExtensionOf(classStr(MyClass))]
final class MyClass_Extension
{
    private void new()
    {
    }
}
```

Because the classes are expressed by the runtime system, it's not meaningful to derive from the extension class. Therefore, the extension class must be marked as **final**. The extension class **MyClass_Extension** doesn't extend the designated class (**MyClass**). Therefore, you cannot override methods from **MyClass** in **MyClass_Extension**. In the example above, the **classStr** compile-time function must be used to designate the augmented class, and it serves two purposes:

-   It produces a compilation error if the **MyClass** class doesn't exist.
-   The compile-time function informs the compiler about what kind of artifact is augmented. Artifact names by themselves don't uniquely identify a given artifact to augment. For example, forms can have the same names as tables, classes, and enums.

Any number of extension classes can augment a given artifact in a particular model. Extension classes are referenced directly by the runtime system.

## Extension class inheritance
Any class that inherits from an augmented class also inherits the effective class. In other words, the classes that inherit from a class that has extensions inherit the methods defined in the extension classes.

## Constructors
Below is a description of restrictions and requirements for constructors in extension classes.

### Instance constructors

The instance constructor is the method that's named **new**. Constructors are useful for initializing the state of the extension objects. The instance constructor that is defined in an extension class can't have parameters. Instances of the extension classes are expressed, and the runtime system calls their constructors as required by the usage scenario. These constructors are never explicitly called by your code. It's guaranteed that the constructor that's provided in an extension class is called once before any instance method or the instance state on the extension class is accessed. However, if no such references are made, the constructor isn't called.

### Static constructors

Static constructors are the parameter-less static methods that are named **typenew**. Static constructors can be defined on extension classes. It's guaranteed that the runtime system calls the constructor exactly once before the first reference to the extension type. You can't assume any particular order of invocation for static construction among a set of extensions. Be careful about referencing static data from other classes in static constructors.

## Methods
The public methods that are defined in extension classes provide additional functionality to the augmented class in the context of the model where the extension class is defined. Only public methods are exposed in this way. You can define private methods to help implement the public methods, but those private methods aren't part of the effective class. Because extension classes are final, methods shouldn't be marked as **protected** since no derived classes can be created to override the method.

### Instance methods

The following example defines an extension method named **ExtensionMethod** in a class that augments **MyClass**.

```xpp
[ExtensionOf(classStr(MyClass))]
final class MyClass_Extension
{
    private void new()
    {
    }
    public int ExtensionMethod(int arg)
    {
    }
}
```

The public instance method (**ExtensionMethod**) is defined in the extension class. It's available as if it were defined in **MyClass** in the context of the model where the extension class is defined. The following example shows how to call the method in the model.

```xpp
MyClass c = new MyClass();
print c.ExtensionMethod(32); // Call the extension method from MyClass_Extension on the instance of the class
```

As shown, the instance method that is defined in the extension class is used as an instance method on the augmented artifact. An extension method can access public and protected members only from the artifact that it augments. This behavior is by design. No artifact should be able to interact directly with state and methods that are explicitly hidden through the **private**, or **internal** keywords. Otherwise, direct interaction with explicitly hidden state and methods could cause malfunction by invalidating key implementation assumptions in those artifacts. Methods and statements in the method body can use the **this** keyword. In this context, the type of **this** is the effective class of the augmented artifact.

### Static methods

Methods that are defined as public and static in the extension class are available as static methods on the artifact that is augmented.

```xpp
[ExtensionOf(classStr(MyClass))]
final class MyClass_Extension
{
    private void new()
    {
    }
    public int method1(int arg)
    {
    }
    public static real CelsiusToFahrenheit(real celsius)
    {
        return (celsius * 9.0 / 5.0) + 32.0;
    }
}
```

The following example shows how to call the method in the model.

```xpp
var temp = MyClass::CelsiusToFahrenheit(20.0);
```

A static method can access the public static methods and state in the effective class of the augmented artifact. As an interesting side effect, static extension methods on the **Global** class become available in the language as functions, which are available without any prefix.

## State
In addition to providing static and instance methods to an artifact, you can add instance state and static state.

### Instance state

Instance state, which is state that pertains to a particular instance of an artifact, can be specified on extension classes. The following example defines a state that is named **state**.

```xpp
[ExtensionOf(classStr(MyClass))]
final class MyClass_Extension
{
    public int state;
    private void new()
    {
    }
}
```

The following example shows how to use **state** in your code.

```xpp
MyClass c = new MyClass();
c.state = 12;
```

### Static state

Static state applies to the type, not instances of the type. The following example defines a static member called **staticState** in the Extension class augmenting the **MyClass** class.

```xpp
[ExtensionOf(classStr(MyClass))]
final class MyClass_Extension
{
    public int state;
    public static int staticState;
    static void TypeNew()
    {
        staticState = 77;
    }
}
```




[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
