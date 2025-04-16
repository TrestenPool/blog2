---
layout: post
title: Section 14. (Lambda expressions, functional interfaces, method references)
  Udemy - Java Programming Masterclass
date: 2023-09-19 15:09 -0500
categories: [Udemy, Java, Spring, Springboot, Hibernate, JDBC]
tags: [Java, Programming, Udemy, Spring] 
image: 
  path: /2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/profile.png
---
- [Git](#git)
- [Lambda Expressions](#lambda-expressions)
  - [Overview](#overview)
    - [Functional interface](#functional-interface)
      - [Consumer functional interface](#consumer-functional-interface)
      - [Predicate functional interface](#predicate-functional-interface)
      - [Supplier functional interface](#supplier-functional-interface)
    - [Convienence Methods](#convienence-methods)
  - [Syntax](#syntax)
  - [Usuage example](#usuage-example)
  - [Multi line lambda](#multi-line-lambda)
  - [Scope](#scope)
  - [Method Reference](#method-reference)
    - [Method Reference restrictions](#method-reference-restrictions)


# Git

# Lambda Expressions

## Overview
  - introduced in **JDK 8**
  - thought of as implicit code for an anonymous class, using a special kind of interface
  - The method to be used is **inferred by java**
  - java requires types which support lambda expressions, to be a **functional interface**
  - considered java's first step into **functional programmming**
  - **Streams** make extensive use of lambdas because the form a pipline of work processed in a chain of events

### Functional interface
  - A functional interface is an interface that has one, and **only one abstract method**
  - referred to as **SAM** (Single abstract method)
  -  java provides a library of functional interfaces in **java.util.function.package**. Just over 40 interfaces and counting.
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/functional_interface_types.png)
    - 4 types of functional interface types
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/function_operator.png)
    - Notice for both **functions** on the left type is **R** which means it could be a different result type than the parameters
    - Notice for both **Operators** the type input and the **type result** are the **same**

#### Consumer functional interface
  - in the `java.util.function` package
  - One abstract method `void accept(T t);`. it takes in a single argument and doesn't return anything.
  - In the following example the ArrayList has a method with the signagure `public void forEach(Consumer<? super E> action) {..}`

```java
List<String> list = new ArrayList<>(List.of(
        "alpha", "bravo", "charlie", "delta"
));

// traditional way of printing an arraylist
for(var str : list){
    System.out.println(str);
}

// lambda expression print
list.forEach(s -> System.out.println(s));
```

- example 2 

```java
public static void main(){
  var coordinates = Arrays.asList(
          new double[alt-text]{47.182, -47.123},
          new double[alt-text]{61.222, -77.190},
          new double[alt-text]{12.331, -55.399}
  );

  // using a variable for the lambda expression for the consumer method
  BiConsumer<Double, Double> p1 = (lat, lng) -> System.out.printf("[lat:%.3f lon:%.3f]\n", lat, lng);
  coordinates.forEach(coordinate -> processPoint(coordinate[0], coordinate[1], p1));

  // using a lambda expression for the  consumer method to pass to processPoint
  coordinates.forEach(coordinate -> processPoint(coordinate[0], coordinate[1], (x,y) -> System.out.printf("[lat:%.3f lon:%.3f]\n", x, y)));
}

public static <T> void processPoint(T t1, T t2, BiConsumer<T, T> consumer){
    consumer.accept(t1, t2);
}
```

#### Predicate functional interface
  - Takes in 1 argument and returns true or false if a specification is met
  - `boolean test(T t);`
    - This is the abstract method for the predicate functional interface

```java
public static void main(String[alt-text] args){
  List<String> mylist = new ArrayList<>(List.of(
          "Tresten", "Josh", "Dave", "Mike", "Roxy", "Tim"
  ));

  fire_person( (str) -> str.equals("Tresten") || str.equals("Josh"), mylist);
  System.out.println(mylist); // Dave, Mike, Roxy, Tim
}
  
public static void fire_person(Predicate<String> fire_person_predicate, List<String> people){
    var iterator = people.iterator();
    while(iterator.hasNext()){
        var person = iterator.next();
        if(fire_person_predicate.test(person)) {
            System.out.println("YOUR FIRED!!! " + person);
            iterator.remove();
        }
    }
}
```

#### Supplier functional interface
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/supplier.png)
  - **Factory method** like code
  - Takes **no arguments** **returns** instance of type **T**

```java
public static void main(String... args){
  String[alt-text] mystrings = new String[alt-text]{"one", "two", "three", "four", "five", "six", "seven"};
  String[alt-text] randomSelectedValues = randomlySelectedValues(3, mystrings, () -> new Random().nextInt(7));
  System.out.println(Arrays.toString(randomSelectedValues));
}

public static String[alt-text] randomlySelectedValues(int count,
                                              String[alt-text] values,
                                              Supplier<Integer> s){
    String[alt-text] selectedValues = new String[count];
    for(int i = 0; i < count; i++){
        selectedValues[i] = values[s.get()];
    }
    return selectedValues;
}
```

```java
Consumer<String> consumer = (message) -> {
    String[alt-text] parts = message.split(" ");
    Arrays.asList(parts).forEach(s -> System.out.println(s));
};

consumer.accept("Hello world, nice to see you");
```
  
### Convienence Methods
  - default methods in the functional interface
  - In this example below we show the .andThen() in the Function interface
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/convenience_methods.png)

.andThen() example
```java
String name = "Tresten";

// first function
Function<String, String> uCase = String::toUpperCase;

// apply the first function and print out the results
System.out.println(uCase.apply(name));

// second function
Function<String, String> lastName = (s) -> s.concat(" Pool");

// setup of the first function calling the second one after
Function<String,String> uCaseLastName = uCase.andThen(lastName);

// call the setup method above with the name variable
System.out.println(uCaseLastName.apply(name));
```


.andThen() chaining example
```java
Function<String, String> uCase = String::toUpperCase;

Function<String, String[alt-text]> f0 = uCase
        .andThen(s -> s.concat(" Pool"))  // return String
        .andThen(s -> s.split(" "));    // return String[alt-text]

System.out.println(Arrays.toString(f0.apply("Tresten")));
```

.andThen() chaining example
```java
String[alt-text]names = {"Josh", "Dave", "Bob", "Carrol"};
Consumer<String> s0 = s -> System.out.print(s.charAt(0));
Consumer<String> s1 = System.out::println;
Arrays.asList(names).forEach(s0
        .andThen(s -> System.out.print(" - "))
        .andThen(s1)
);
```


Comparator Example

```java
default void sort(Comparator<? super E> c){ .. }
```

```java
public static <T, U extends Comparable<? super U>> Comparator<T> comparing(
        Function<? super T, ? extends U> keyExtractor)
```

```java
// compare by lastname then compare by firstname
list.sort(Comparator.comparing(Person::lastName)
    .thenComparing(Person::firstname));

// print out results
list.forEach(System.out::println);
```






## Syntax
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/syntax.png)

## Usuage example
  - lambda expression parameters are determined by the associated interface's method
  - The method to be used is **inferred by java**
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/lambda.png)
  - ![alt-text](/2023-09-19-section-14-lambda-expressions-functional-interfaces-method-references-udemy-java-programming-masterclass/example.png)

```java
// our list of people
List<Person> people = new ArrayList<>(Arrays.asList(
        new Main.Person("Mickey", "Mouse"), // just to show you we can use this syntax because the record is a static nested class
        new Person("Donald", "Duck"),
        new Person("Goofy", "Mcman"),
        new Person("Hubert", "Jensen")
));

// sort with a lambda expression which is a comparable statement
people.sort( (o1, o2) -> o1.firstName.compareTo(o2.firstName) );
```

```java
// Comparator interface that extends Comparator
interface EnhancedComparator<T> extends Comparator<T>{
    int secondLevel(T o1, T o2);
}

// concrete class for the above interface
var comparatorMixed = new EnhancedComparator<Person>(){
    @Override
    public int compare(Person o1, Person o2) {
        int result = o1.lastName.compareTo(o2.lastName);
        return (result == 0) ? secondLevel(o1, o2) : result; // if the last names are the same, match by the first name too, the second level
    }

    @Override
    public int secondLevel(Person o1, Person o2) {
        return o1.firstName.compareTo(o2.firstName);
    }
};

// we are unable to use a lambda expression for the intended comparator comparatorMixed because it is not a Functional Interface
// It is not a Functional Interface because it has 2 abstract methods!!
people.sort(comparatorMixed);

System.out.println(people);
```

## Multi line lambda

```java
List<String> list = new ArrayList<>(List.of(
        "alpha", "bravo", "charlie", "delta"
));

// multi-line lambda expression to make all the elements in list uppercase
list.forEach(mystring -> {
    int index = list.indexOf(mystring);
    list.set(index, list.get(index).toUpperCase());
});
```

## Scope
  - A lambda expression has access to **final** variables or **effectively final** of the enclosing method.

```java
// we are able to use this variable because it is EFFECTIVELY FINAL, meaning it hasn't been changed since its declaration
String prefix = "nato";
list.forEach(mystring -> {
    int index = list.indexOf(mystring);
    list.set(index, "%s %s".formatted(prefix, list.get(index).toUpperCase()) );
});
```

## Method Reference
  - You can just use a method reference in the lambda body
  - method references are for easier readibility
  - The second example shows just replacing with the method reference
  - Both achieve the same result of printing every element in the list

```java
backedByArray.forEach(s -> System.out.println(s));
```

```java
backedByArray.forEach(System.out::println);
```

```java
class Test{
    public static int ID_GENERATOR = 1000;
    private int id;

    public Test() {
        id = ID_GENERATOR++;
        System.out.println("Created Test object with id: " + this.id);
    }
}

public class Main {
    public static void main(String[alt-text] args) {
        seedArray(Test::new, 10);
    }

    public static Test[alt-text] seedArray(Supplier<Test> reference, int count){
        Test[alt-text] testArray = new Test[count];
        for(int i = 0; i < count; i++){
            testArray[i] = reference.get();
        }
        return testArray;
    }

}
```

### Method Reference restrictions
  - methods which can be used, are based on the context
  - you can reference a static or instance method
