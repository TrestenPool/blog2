---
layout: post
title: UML Diagrams
date: 2023-09-11 11:14 -0500
author: Tresten Pool
categories: [Java, UML, OOP]
image: 
  path: /2023-09-11-uml-diagrams/profile.png
---

- [Overview](#overview)
  - [What are UML diagrams](#what-are-uml-diagrams)
  - [Types of UML diagrams](#types-of-uml-diagrams)
  - [Good resources](#good-resources)
- [Arrows, Symbols explained](#arrows-symbols-explained)
  - [Visibility / Access Modifers](#visibility--access-modifers)
  - [Static](#static)
  - [Relationships](#relationships)
    - [Dependency](#dependency)
    - [Inheritence](#inheritence)
    - [Generalization](#generalization)
    - [Realization](#realization)
    - [Association](#association)
    - [One-way association](#one-way-association)
    - [Aggregation](#aggregation)
    - [Composition](#composition)
    - [Multiplicity](#multiplicity)
- [Diagrams](#diagrams)
  - [Structural Diagrams](#structural-diagrams)
    - [Class diagram](#class-diagram)
    - [Component diagram](#component-diagram)
  - [Behavioral Diagrams](#behavioral-diagrams)

<!-- Overview -->
# Overview

## What are UML diagrams
  - Unified Modeling Language
  - It’s a rich language to model software solutions, application structures, system behavior and business processes. 

## Types of UML diagrams
  - ![alt-text](/2023-09-11-uml-diagrams/uml_diagram_types.png)
  - There are two main categories of UML Diagrams
    - **Structural**
      - Class diagram
      - Component diagram 
      - Deployment diagram
      - Object diagram
      - Package diagram
      - Profile diagram
      - Composite structure diagram

    - **Behaviorial**
      - Use case diagram
      - Activity diagram
      - State machine diagram
      - Sequence diagram
      - Communication diagram
      - Interaction Overview diagram
      - Timing diagram

## Good resources
  - [UML Diagram Types Guide: Learn About All Types of UML Diagrams with Examples](https://creately.com/blog/diagrams/uml-diagram-types-examples/)
  - [UML cheat sheet](https://khalilstemmler.com/articles/uml-cheatsheet/)
  - [UML cheat sheet UTSA](http://www.cs.utsa.edu/~cs3443/uml/uml.html)
  - {% include embed/youtube.html id='6XrL5jXmTwM' %}
  
  

<!-- Arrows, symbols -->
# Arrows, Symbols explained

## Visibility / Access Modifers
  - ![something](/2023-09-11-uml-diagrams/visibility.png)

## Static 
  - ![alt-text](/2023-09-11-uml-diagrams/static.png)
  - Static attributes and methods are underlined
  - instance scope by default

<!-- Relationships -->
## Relationships
  - The arrows define relationships between the different components 
  - Different types of Relationships

### Dependency
  - ![alt-text](/2023-09-11-uml-diagrams/Dependency.png)
  - An object of one class might use an object of another class in the code of a method. If the object is not stored in any field, then this is modeled as a dependency relationship. For example, the Person class might have a hasRead method with a Book parameter that returns true if the person has read the book (perhaps by checking some database).

### Inheritence
  - ![alt-text](/2023-09-11-uml-diagrams/inheritence.png)
  - Ex, the Tortoise, Otter and Slow Loris **inherit** the Animal class

### Generalization
  - ![alt-text](/2023-09-11-uml-diagrams/generalization.png)
  - A class extends another class. For example, the Book class might extend the Document class, which also might include the Email class. The Book and Email classes inherit the fields and methods of the Document class (possibly modifying the methods), but might add additional fields and methods.
  - Generally used for a base class or a subclass that extends a base class or abstract class

### Realization
  - ![alt-text](/2023-09-11-uml-diagrams/realization.png)
  - A class implements an interface. For example, the Owner interface might specify methods for acquiring property and disposing of property. The Person and Corporation classes need to implement these methods, possibly in very different ways.
  - Generally used when a class implements an interface

### Association
  - ![alt-text](/2023-09-11-uml-diagrams/association.png)
  - simple
  - Ex. Otter eats sea urchin

### One-way association

### Aggregation
  - ![alt-text](/2023-09-11-uml-diagrams/aggregation.png)
  - Where there can be multiple of something
  - Where the **part can exist without the whole**
  - a tortoise can exists by itself or it could be in a creep, which is just a group of toroises
  - the child object can exist without the parent object
  - the diamond is at the end where it contains all the parts
    - ex. The creep contains the tortoises

### Composition
  - ![alt-text](/2023-09-11-uml-diagrams/composition.png)
  - The child object cannot exists without the parent object
  - in the example the visitor center has a lobby, and also has a bathroom
  - if the visitor center was to be closed for construction so would the lobby and bathroom. So the lobby and bathroom cannot exist without the visitor center

### Multiplicity
  - refers to the concept of denoting a number on a specific side in a uml relationship
  - ![alt-text](/2023-09-11-uml-diagrams/multiplicity.png)
  - ex. there is 1.. to many bathrooms that can be at the visitor center
  - ex. but there is only 1 lobby




<!-- Diagrams -->
# Diagrams

## Structural Diagrams

### Class diagram
  - ![alt-text](/2023-09-11-uml-diagrams/class_diagram.png)
  - Class diagrams are the main building block of any object-oriented solution. It shows the classes in a system, attributes, and operations of each class and the relationship between each class.

### Component diagram


## Behavioral Diagrams
