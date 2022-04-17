---
author:
  name: "hexterisk"
date: 2021-07-02
linktitle: Creational Patterns
type:
- post
- posts
title: Creational Patterns
tags: ["design-patterns", "gangs-of-four", "frameworks", "toolkits", "creational-patterns", "builder", "prototype", "factory", "singleton"]
weight: 10
categories: ["Design-Patterns"]
---

**Creational Design Patterns** reduce the complexity in creation of different objects of shared type/properties.

These patterns simplify object creation mechanisms by separating the workings of an object's creation, composition and representation. This in turn results in increased flexibility. Instead of hardcoding data into classes for creating objects every time, we can employ these patterns for the instantiation of an object dependent on the situation. This ensures that the set of related objects share a common ancestor for common properties.

## Factory Method

> Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

We create a “factory” class that can use some logic to decide _at the moment of instantiation_ over what data to use for creating the object. Now, since it can't anticipate the needs of the client, this task of instantiation is delegated to a subclass specific for the situation. This localization of knowledge helps in hiding(abstraction) of the actual implementation details as well.

![](/Design_Patterns_Creational_Patterns/image.png)

Therefore, **Factory Method** pattern defines an interface for creation of objects, but lets a subclass suitable to the situation perform the instantiation. The suitability is defined by the logic implemented by the factory.

The **Creator** class is the factory with the operational details, and has an interface defined called `FactoryMethod` for creating an object. A subclass **ConcreteCreator** is created that is localized for a specific use-case. It creates an object of **ConcreteProduct** class, which implements the **Product** class.

For example, Creator class `AnimalFactory` has the task of producing different objects of Product class `Animal`. This factory could be under different environments which would cultivate different conditions, and may cater to two conditions through the following ConcreteCreator classes:

1.  `RandomPopulationFactory` where the animals are randomly generated.
2.  `BalancedPopulationFactory` where the population of different animals is kept equal respectively.

The decision as to which factory will be employed is dependent on the environment, and is decided by the AnimalFactory, which delegates the task to the suitable subclass (RandomPopulationFactory or BalancedPopulationFactory). These subclasses contain the logic for creation of objects pertaining to their own environments and can do the needful.

Implementation Example: [Factory Method Pattern](https://www.youtube.com/watch?v=pt1IbV1aSZ4)

## Abstract Factory

> Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

An extension of the Factory Method pattern, a super-factory whose sub-factories have the capability of creating multiple products, which then enables it's concrete factories to produce multiple products. This is to ensure that even a single factory has the capability to produce multiple products that are related, or family of products, and this responsibility/implementation is further delegated to their concrete factories respectively.

![](/Design_Patterns_Creational_Patterns/1_image.png)

The **AbstractFactory** pattern defines an interface to create multiple products, that is, `CreateProductA` and `CreateProductB`. It is implemented by two **ConcreteFactory** classes `ConcreteFactory1` and `ConcreteFactory2`. These concrete factories can instantiate objects `ProductA1`, `ProductB1` and `ProductA2`, `ProductB2`. These products implement **AbstractProductA** and **AbstractProductB** classes respectively. Since the same factory can produce A1,B1 and A2,B2 pairs, it is clear that one factory is keeping objects(products) of related types together since concretions of different products together, like A1 and B2, is not sensible. Therefore, enabling a factory to create A1 and B1 together ensures that a single factory can create products that make sense in conjunction with each other.

For example, AbstractFactory class `UIFactory` has the task of producing different objects of ProductA and ProductB classes `Scrollbar` and `Button`. This factory will have ConcreteCreator1 and ConcreteCreator2 classes that can produce objects suitable as per the environment conditions, such as:

1.  `WindowsFactory` where the factory can produce UI elements suitable for Windows platform.
2.  `LinuxFactory` where the factory can produce UI elements suitable for Linux platform.

The decision as to which factory will be employed is still dependent on the environment.

Implementation Example: [Abstract Factory Pattern](https://www.youtube.com/watch?v=j50FusMmUMw)

## Builder

> Separate the construction of a complex object from its representation so that the same construction process can create different representations.

The class delegates the initialization process to a Builder class with the aim of initializing members of the object separate from the definition. This is done to make the initialization process flexible against the data provided.  The advantages are two fold:

1.  Ensures that an object is always initialized in a complete state.
2.  Makes the constructor highly readable.

![](/Design_Patterns_Creational_Patterns/2_image.png)

The **Director** is the user of the **Builder** class. It defines an interface `BuildPart` for building an object. **ConcreteBuilder** implements Builder, implements the initialization logic for the object. This implementation is specific to the environment and produces an object that is complete in itself, as per the Director's instruction.

For example, a Director class `TextParser` requires a converter. The Builder class `TextConverterBuilder` will implement different ConcreteBuilder classes for different formats, such as `ExcelBuilder` and `CSVBuilder`. Since different file formats have different requirements to be able to parse the text, each builder can implement their own object initialization logic with the parameters provided by the, which is of no concern to both `TextParser` and  `TextConverterBuilder`.

Implementation Example: [Builder Pattern](https://www.youtube.com/watch?v=M7Xi1yO_s8E)

## Prototype Pattern

> Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

To avoid creation of a different instance of the same object for manipulation, the **Prototype** design pattern demands that the original class provide a method to get the prototype of the class. This prototype allows a new object to clone an old object, which can then be manipulated. This preserves the original object as well as the effort into creating a new object definition altogether.

![](/Design_Patterns_Creational_Patterns/3_image.png)

The **Prototype** class provides an interface `Clone` for to clone new objects from the original one. Subclasses **ConcretePrototype1** and **ConcretePrototype2** implement the prototype to return a copy of the original object.

For example, a Prototype class `Animal` provides ConcretePrototype classes `LionPrototype` and `BirdPrototype` to allow the client to modify these classes into different entities, such as the lion to sheep or bird to crocodile, to modify certain properties.

Implementation Example: [Prototype Pattern](https://www.youtube.com/watch?v=nZ76x13Nm8Q)

## Singleton Pattern

> Ensure a class only has one instance, and provide a global point of access to it.

**Singleton Pattern** specifies that only a single instance of it exists (which requires absolute surety that it can serve the purpose through it) and enforces that the class have “global scope".

![](/Design_Patterns_Creational_Patterns/4_image.png)

Global scope requires the constructor of the class to be private so that it can't be recreated, which means it would require a static method to instantiate it in the first place. The static method (since it's a class member) will have access to the constructor, defined as `Instance`., which would initialize it into the static member `uniqueInstance`.

Implementation Example: [Singleton Pattern](https://www.youtube.com/watch?v=KUTqnWswPV4)


Citation: [Gang of Four Design Patterns](https://www.journaldev.com/31902/gangs-of-four-gof-design-patterns)