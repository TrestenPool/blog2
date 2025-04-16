---
layout: post
title: Section 11 (Abstraction) in Java. Udemy - Java Programming Masterclass
date: 2023-09-13 10:45 -0500
author: Tresten Pool
categories: [Udemy, Java]
tags: [Java, Programming, Udemy] 
image: 
  path: /2023-09-13-section-11-udemy-java-programming-masterclass/profile.png
---


- [Section 11 Abstraction in Java  Udemy - Java Programming Masterclass](#section-11-abstraction-in-java--udemy---java-programming-masterclass)
  - [Abstraction](#abstraction)
    - [Notes](#notes)
    - [Abstract classes](#abstract-classes)
      - [Example](#example)
      - [Abstract class extending another Abstract class](#abstract-class-extending-another-abstract-class)
      - [Why Use Abstract classes](#why-use-abstract-classes)
  - [Interface](#interface)
    - [Visibility](#visibility)
    - [Implementing interface](#implementing-interface)
    - [Examples](#examples)
    - [Interface post JDK 8 update](#interface-post-jdk-8-update)
    - [Interface Extension method](#interface-extension-method)
    - [Private methods](#private-methods)
  - [Abstract classes vs interfaces](#abstract-classes-vs-interfaces)
    - [Abstract classes](#abstract-classes-1)
    - [Interfaces](#interfaces)
  - [Coding Challenge](#coding-challenge)



# Section 11 Abstraction in Java <br> Udemy - Java Programming Masterclass 

<!--------------------------------------------------------------------------->
<!------------------------------- ABSTRACTION ------------------------------->
<!--------------------------------------------------------------------------->

---

## Abstraction

### Notes
  - keeps the user from viewing complex code

  - provides the user with only necessary information

  - If you consider an elephant, dog, lizard, you would probably say they are all animals
    - An animal is a really **abstract concept**
    - An animal doesn't really exists except to describe more specific things 
    - If you can't draw it on a piece of paper it is probably abstract

  - Concrete Method
    - A method body with at least one statement
    - Is set to **implement** **an abstract method** if it overrides one
  
### Abstract classes
  - ![alt-text](/2023-08-27-java-programming-masterclass-udemy/abstract_table.png)
  - Can have a mix of abstract and concrete methods

  - `abstract class Animal { `
    - default visibility is **package** which is something that you cannot specify other than by leaving off any access modifer before declaring the abstract class like this
    - visiblitiy of package means that only classes in the same package have access to the abstract class
    - The same goes for the abstract methods, if they are not specified, it will default to **package**

  - `public abstract class Animal {`
    - if we wanted to give access to this abstract class outside of this package you must specify **public** 

#### Example
  - ```java
    public abstract class Animal {
      // field properties
      protected String type;
      protected String size;
      protected double weight;

      // constructor
      public Animal(String type, String size, double weight) {
          this.type = type;
          this.size = size;
          this.weight = weight;
      }

      // methods
      protected abstract void breathe();
      protected abstract void move(int speed);
      protected abstract void breed();

      // final method
      public final void exists(){
          System.out.println("Existing out here");
      }
    }
  ```

  - ```java
    public class Dog extends Animal {
        public Dog(String type, String size, double weight) {
            super(type, size, weight);
        }

        @Override
        protected void breathe() {
            System.out.println("panting like a dog");
        }

        @Override
        protected void move(int speed) {
            System.out.println("Moving on all 4's at " + speed + "mph");
        }

        @Override
        protected void breed() {
            System.out.println("Pour hot water on us if we get stuck again");
        }
    }
  ```

#### Abstract class extending another Abstract class
  - when an abstract class extends another abstract class there are a couple of things to keep in mind
    - It has the option to implement **any number or none of the abstract methods** it is extending from

#### Why Use Abstract classes
  - An abstract class in your hierarchy forces the designers of subclasses, to think about , and create unique and targeted implementations, for the abstracted methods
  
<!--------------------------------------------------------------------------->
<!------------------------------- INTERFACE --------------------------------->
<!--------------------------------------------------------------------------->

--- 

## Interface
  - A class can implement multiple interfaces but only 1 abstract class
  - similiar to an abstract class, although it isn't a class at all
  - by using an interface you must implement all of the abstract methods on the interface
  - A class that implements an interface does so it can be known by that type
  - keyword **interface** is used to specify an interface
  - You don't have to put the keyword **abstract** before every method as it is implicity put there

### Visibility
  - Visibility of an interface is **package** by default, meaning only classes in the same package have access to it
  - the abstract methods can only be labeled with the public access modifer

  - **interface members** are implicitly **public**

### Implementing interface
  - An interface cannot implement another interface
  - An interface can however extend another interface
  - `public interface iA extends iB {`

### Examples
  - ```java
    /** interface **/
    public interface FlightEnabled {
      abstract void fly();
      abstract void land();
    }

    /** implements class **/
    public class Bird implements FlightEnabled {
      @Override
      public void fly() {
          System.out.println("Flying through the air");
      }

      @Override
      public void land() {
          System.out.println("Getting ready for landing");
      }
    }
  ```

### Coding to an interface
  - incredibly useful and scalable technique for writing systems that are highly dependent on changes.
  - **“Coding to interfaces, not implementation.”**
  - Coding to interfaces is a technique to write classes based on an interface; interface that defines what the behavior of the object should be. It involves creating an interface first, defining its methods and then creating the actual class with the implementation.
  - Scales well to support new subtypes
  - Downside is that alterations to the interface may wreak havoc no the client code
  - imagine there are 50 subclasses that implement an interface and you make a change, you would have to make that change in 50 other places to they can implement this 1 new method

  - ```java
    public static void main(String[alt-text] args) {
      // not coding to an interface
      // the ArrayList is not an interface but an implementation of a list
      ArrayList<Integer> ll1 = new ArrayList<>(Arrays.asList(1,2,3,4,5,6,7,8));

      // coding to an interface
      List<Integer> ll2 = new LinkedList<>(Arrays.asList(9,10,11,12));

      method1(ll1);
      method1(ll2);
    }

    // again this would not be coding to an interface but the argument is a concrete class and not an interface
    // public static void method1(ArrayList<Integer> list){

    // this is coding to an interface because List is an interfac and can accept any  class that implements the List interface
    public static void method1(List<Integer> list){
        for(var x : list){
            System.out.printf("%d ", x);
        }
        System.out.println();
    }
  ```

### Interface post JDK 8 update
  - before jdk 8 the interface could only have **public abstract methods**
  - jdk 8 introduced the **default** method and the **public static methods** 
  - jdk 9 introduced **private** **methods**, both static and non-static

### Interface Extension method
  - part of the jdk 8 update
  - an extension method is identified by the modifer **default**, so it is more commonly known as the **default method**
  - it is a concrete method, meaning it has curly braces and some code within it
  - Acts like a method on the superclass because we can override it
  - Adding a default method doesn't break any classes currenty implmenting the interface

###  Private methods
  - jdk 9 gave us private methods both static and not static
  - enhancement solves the problem of re-use of code, within concrete methods of an interface



<!--------------------------------------------------------------------------->
<!------------------ ABSTRACT CLASSES VS INTERFACES ------------------------->
<!--------------------------------------------------------------------------->

--- 

## Abstract classes vs interfaces
  - ![alt-text](/2023-09-13-section-11-udemy-java-programming-masterclass/interface_vs_abstract.png)

### Abstract classes
  - abstract classes are very similiar to interfaces
  - you can't instanciate both of them
  - both may contain a mix of methods declared with, or without a method block
  - you can use all but the **private** access modifer, for its abstract methods
  - abstract class can extend only one parent class, but can imlement multiple interfaces

### Interfaces
  - just a declaration of methods, which you want some classes to have, its not the implementation
  - in an interface we define what kind of operations an object can perform
  - since jdk8 can contain methods with implementation for backwords compability reasons
  - since jdk9 can contain private methods, commonly used when default methods share common code

## Coding Challenge
  - [github repo](https://github.com/TrestenPool/Java-Programming-MasterClass/tree/main/section11/Challenge/src)