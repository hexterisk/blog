---
author:
  name: "hexterisk"
date: 2020-10-10
linktitle: Introduction
type:
- post
- posts
title: Introduction
tags: ["design-patterns", "gangs-of-four", "frameworks", "toolkits"]
weight: 10
categories: ["Design-Patterns"]
---

A design pattern is a code structure used to solve commonly occurring problems in software development. It is a generic description of different components' design, their relationships, and how they come together to solve the said problem in the specified context. It is characterized by:

1.  Pattern Name
    *   To associate a certain solution to a name for ease of reference, through appropriate association.
2.  Problem
    *   The design problem and issues to be addressed in a specified context, to which the solution described by the design pattern is applicable.
3.  Solution
    *   The code structure to resolve the problem, consisting of comprehensive definition of the components and the relationships among them.
4.  Consequences
    *   The results of the design pattern on application to a problem. Addresses space-time trade-off and implementation issues, including the impact on the system's extensibility and portability.

The MVC model from Smalltalk-80 is the most basic and appropriate example to describe a design pattern.

**MVC(Model/View/Controller)** is a namesake for it's functionality. The design decouples different functionalities into different components for increased flexibility and re-usability, namely:

1.  Model
    *   Application object that handles all operations pertaining to data.
2.  View
    *   Screen representation that handles the appearance of the application.
    *   Ensures that the appearance reflects any change in the state of the model.
3.  Controller
    *   Defines how the user interface reacts to user interaction.

The idea is to separate objects so that one does not require to know any details of the other objects, and any changes to one object do not affect the other objects. This facilitates abstraction between the objects.

A simple subscribe/notify protocol between views and models ensure that a view knows when the state of the model changes.

![](/Design_Patterns_Introduction/a.png)

Different views for the same model.

In the sample diagram above, since each component works independently, multiple views can be attached to a single model for different representation for the same data, as opposed to clubbing all functionality together in a single module making it unfit for re-usability.

A view uses an instance of the controller, which can be used to define how each view reacts differently to the same user action.

## Approach

Defining the approach to different parts of a programming problem helps design patterns solve generic recurring problems.

*   Appropriate Objects
    *   Decomposing a complete implementation into different modules becomes hard when adhering to object-oriented philosophy.
    *   Design patterns help identify the correct abstraction and hierarchy to create objects in the system.
*   Object Granularity
    *   The size and the number of objects in a system can vary tremendously. The level of detail of the system that an object works at needs to be determined.
    *   Design patterns help define which parts of the system should be made into objects.
*   Object Interface
    *   An object's signature is any value to/from the object such as parameters, return value and name. Interface is the set of all signatures defined by an object's operations, defining how to interact with the said object. An object is only known through it's interface.
    *   Design patterns help identify key elements and the data exchange of a module, and thus design a specification for the object's interface. They also specify relationships between them.
    *   **Type** denotes a particular interface. An object may have many types, and widely different objects can share a type. Part of an object's interface may be characterized by one type, and other parts by other types.
*   Object Implementation
    *   Defined by the class of the object, and created by the instantiation of the said class. The object is therefore an instance of it's class.
    *   A child class inherits all definitions of data and operations from it's parent class, and can have operations that override definition from the parent class.
        *   An **Abstract Class** has a simple purpose - to define a common interface for all subsequent child classes, and it's unimplemented operations are called **Abstract Operations**.
        *   Any other class is a **Concrete Class**.
        *   **Mixin Class** provides an optional interface to other classes, and are not intended to be instantiated. It simply contains methods for use by other classes without being their parent.

NOTE: **Class Inheritance** is a mechanism to extend functionality by sharing already defined code and representation to another class. **Interface Inheritance** defines when an object can substitute other.

> Programming to an Interface, not an Implementation.

The philosophy preaches that classes shall be based on interfaces, that is, to focus on the behavior of the object. The interface shall be created first, define the methods and the implementation of the class itself later. This facilitates:

1.  Test Driven Development
    *   Mocking objects during the development process helps pass the tests when there is no implementation. As the code grows, simply replace the mock with the actual code.
2.  Flexibility and Maintainability
    *   Interaction between different parts of the code base is utmost necessary to ensure smooth operation of the whole system. Programming against the interface, that is, creating the implementation first and the interface later might break the module since interface is dependent on the implementation. Thereafter, modifying the interface to work with the modified implementation might break the system since the modified interface might become incompatible with other modules.

## Design Practice

The code base shall be designed with future requirements taken into consideration. It should be flexible, and accommodating to any changes as the requirements evolve with the growth of the code base. Making the code base robust towards such changes ensures that the system doesn't risk redesign in future, otherwise it would repeat the cycle of implementation and testing as well, costing precious resources.

Design Patterns keep the system structure sufficiently flexible in definite ways, allowing any modifications required along with keeping the design rigid enough to not completely change.

*   Loose coupling of classes keeps them flexible enough to make them work in a separate codebase altogether with minimal to no modifications.
*   Implementation of **Toolkits.**
    *   Maintaining a collection of classes that can be expected to be reused.
    *   Should avoid assumptions and dependencies which can put limitations of their functionality since the places it will be used are not known before-hand.
    *   They are generalized for various use cases, for example, iostream library in C is for input-output operations.
*   Constructing a **Framework.**
    *   Ensuring communication and cooperation between classes to build functionality.
    *   Helps in dictating the architecture for a software.
    *   Emphasizes design reuse over code reuse as the classes being used would have the same implementation but they can be composed in different manner to achieve different functionality.
    *   Applications should evolve with the framework because of the dependency of implementation.
    *   Specialized for a particular use case, for example, Tensorflow has been constructed to facilitate machine learning.