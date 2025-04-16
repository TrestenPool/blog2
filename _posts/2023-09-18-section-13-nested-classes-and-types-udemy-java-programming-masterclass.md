---
layout: post
title: Section 13. (Nested Classes and types) Udemy - Java Programming Masterclass
date: 2023-09-18 17:25 -0500
categories: [Udemy, Java]
tags: [Java, Programming, Udemy] 
image: 
  path: /2023-09-18-section-13-nested-classes-and-types-udemy-java-programming-masterclass/profile.png
---

- [Git](#git)
- [Nested Classes](#nested-classes)
  - [When to use nested classes](#when-to-use-nested-classes)
  - [4 types of Nested classes](#4-types-of-nested-classes)
  - [JDK versions](#jdk-versions)
  - [Static nested class](#static-nested-class)
  - [Inner classes](#inner-classes)
  - [Local Classes](#local-classes)
  - [Anonymous Class](#anonymous-class)


# Git
  - [Section 13 code](https://github.com/TrestenPool/Java-Programming-MasterClass/tree/main/section13/Nested_Classes/src)

# Nested Classes

## When to use nested classes
  - when your classes are tightly coupled, meaning their functionality is interwoven

## 4 types of Nested classes
  - ![4 types](/2023-09-18-section-13-nested-classes-and-types-udemy-java-programming-masterclass.md/4_types.png)

  1. Static Nested class
  2. Instance or inner class
  3. local class
  4. anonymous class

## JDK versions
  - Before JDK16, only static nested classses were allowed to have static methods
  - As of JDK16, all four types of nested classes can have static members of any type, including static methods

## Static nested class
  - a class enclosed in another class, declared as static
  - access to the static nested class requires the outer class name as part of the qualifying name
  - This class has the advantage of being able to access private attributes on the outer class.

```java
class A {
  private String name;

  public A(String name){
    this.name = name
  }

  // static class
  static class B{
    public void test(A a){
      System.out.println(a.name); // we can access the private field "name" because we are in a static nested class
    }
  }
}

```

```java
class Main{
  public static void main(String... args){
    A.B b = new A.B();
    b.test(new A("Tresten"));
  }
}
```

## Inner classes
  - non-static classes, declared on an enclosing class, at the member level
  - an inner class has access to instance members, including private members, of the enclosing class
  
  - to create an instance of an inner class, you must first have an instance of the Enclosing Class

```java
public class A{

  public class B{

    public void printSecret(){
      System.out.println("I am a secret, shhh..");
    }

  }

}
```

```java
public class Main{
  public static void main(String... args){

    A a1 = new A();
    A.B b1 = a1.new B();
    b1.printSecret();

    // or all on line line
    new A().new B().printSecret();
  }
}
```

## Local Classes
  - local classes are inner classes, but **declared directly in a code block**, usually a **method body**.
  - Because of that, **they don't have access modifers**, and are only accessible to that method body while executing
  - Like an inner class they have access to all fields and methods on the enclosing class

```java
// outer class
public class A {
    private String aName;
    
    public A(String aName) {
        this.aName = aName;
    }
    
    public void printMessage(){
        // local class
        class compliment{
            private String comp;
            public compliment(String comp){
                this.comp = comp;
            }
            public String getComp() {
                return comp;
            }
        }
        System.out.println(aName + ", you look " + new compliment("GREAT").getComp());
    }
}
```

```java
public class Main{
  public static void main(String... args){
    A a1 = new A("Tresten");
    a1.printMessage(); // output: Tresten you look GREAT
  }
}
```

  - As of JDK 16, you can also **create a local record, interface and enum type** in your method block
    - These are all implicityly static types, and therefore arent' inner classes, or types, but static nested types

## Anonymous Class
  - a local class that **doesn't have a name**
  - all of the other nested classes before have been created with a class declaration
  - Anonymous classes are created without a **class declaration**
  - Anonymous classes are **used a lot less**, since the introduction of **lambda expressions** in jdk 8
  - There are a couple of ways to use anonymous classes, I will show two ways below

```java
public class Main{
  public static void main(String... args){
    var comp = new Comparator<Mammal>(){
        @Override
        public int compare(Mammal o1, Mammal o2) {
            return o1.getName().compareTo(o2.getName());
        }
    };
  }
}
```