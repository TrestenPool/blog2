---
layout: post
title: Section 12. (Generics) Udemy - Java Programming Masterclass
date: 2023-09-13 13:58 -0500
author: Tresten Pool
categories: [Udemy, Java]
tags: [Java, Programming, Udemy] 
image: 
  path: /2023-09-13-section-12-generics-udemy-java-programming-masterclass/profile.png
---

- [Git](#git)
- [Overview](#overview)
  - [Example](#example)
- [Generic naming convention](#generic-naming-convention)
- [Raw usage of generic classes](#raw-usage-of-generic-classes)
- [Converting ArrayList to a List of a specific type](#converting-arraylist-to-a-list-of-a-specific-type)
- [Comparable interface](#comparable-interface)
- [Comparator interface](#comparator-interface)
- [Generic Method example](#generic-method-example)
  - [Limitation of a reference of generic classs with a list argument](#limitation-of-a-reference-of-generic-classs-with-a-list-argument)
- [Generic Type Parameters](#generic-type-parameters)
- [Multiple bounds](#multiple-bounds)
- [Generic Wildcards](#generic-wildcards)
  - [Wildcard upperbound, lowerbound](#wildcard-upperbound-lowerbound)
  - [Type Erasure](#type-erasure)
  - [Pitfalls of wildcards](#pitfalls-of-wildcards)


# Git
  - [Github link to Section 12 example code Sports teams examples](https://github.com/TrestenPool/Java-Programming-MasterClass/tree/main/section12/Generics/src)
  - [Github link to Section 12 Challenge map ](https://github.com/TrestenPool/Java-Programming-MasterClass/tree/main/section12/Generics_Challenge/Generics_Challenge/src/tresten)
    - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/challenge_class_diagram.png)

# Overview
  - java supports generic types, such as
    - classes
    - records
    - interfaces
    - methods
  
  - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/anatomy.png)
  - generics allow the compiler to do **compile-time type checking**, when adding and processing elements in the list


## Example
  - ```java
    // not using generics
    public class ITellYou {
      private String field;
    }

    // using generics
    public class ITellYou<T> {
        private T field;
    }
  ```
  - T is the placeholder for a type that will be specified later
  - T is the **type identifier**
  - The type idenfiter can be **any letter** or word but **T** is short for Type which is why it is commonly used


## More than 1 Generic Type
  - You can have more than 1 type parameter
  - convention is T, S, U in that order

  - ```java
    public class Team<T, S, U, V> {
      private T variable1;
      private S variable2;
      private U variable3;
      private V variable4;
    }
  ```

# Generic naming convention
  - some letters are **reserved** for special use cases
  - the most commonly used type parameters are
    - **E** - element (used extensively by the Java Collections framework)
    - **K** - key (used for mapped types)
    - **N** - for Number
    - **T** - for Type
    - **V** - for Value
    - **S, U, V** etc for 2nd, 3rd, 4th types

# Raw usage of generic classes
  - you can use generic classes without specifying a type in the type parameters
  - this is called the **Raw Use** of the reference type
  - raw use is still available for backwards compability, but is highly discouraged
  - ```java
    public class MyArray <T> {
      T myvar;
    }

    public static void Main(String.. args){
      // raw type
      MyArray rawtype = new MyArray();

      // generic type (preferred)
      MyArray<Integer> myintarray = new MyArray<>();
    }
  ```

# Bounded Generic classes
  - Generic classes can be bounded, limiting the types that can use it
  - ```java
    public class Team <T extends Player> 
  ```
  - this **extends** keyword **doesn't have the same meaning** as extends, when its used in a class declaration
    - This isn't saying that our type T extends Player although it could
    - All this is saying is that the paramaterized type T, has to be a Player, or a **subtype of Player**
    - A subclass that has extended or implements Player would work just fine
  - this is saying that a type that extends the Player class can be passed as a type to this class during instanciation
  - the example is called an **upper bound**

# Converting ArrayList to a List of a specific type
  - [stackoverflow](https://stackoverflow.com/questions/36598928/java-generics-in-arraylist-toarray)
  - ArrayList.toArray() will always return an array of objects if no parameter of the specific type requested is passed to it

```java
// our String arraylist
ArrayList<String> someData = new ArrayList<>();

// this works fine
String someLine = someData.get(0);

// but this will fail, this is because .toArray() will return an array of objects
String[alt-text] arrayOfData = someData.toArray();

// the way to do it is the following
String[alt-text] arrayOfData = someData.toArray(new String[0]);
// or
String[alt-text] arrayOfData = someData.toArray(new String[alt-text]{});

```

# Comparable interface
  - Comparable is an interface
  - if a class implements **Comparable** it may use the **Arrays.sort()** to sort the elements in the array

```java
public interface Comparable<T> {
  int compareTo(T o);
}
```
  - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/compareto.png)

  - If we wanted to have our class be able to use the sort method on an array we would have to implement it

```java
enum Name{TRESTEN, KLARI, BRIANA}

public class Student implements Comparable<Student> {
    // field
    private Name name;

    // constructor
    public Student(Name name) {
        this.name = name;
    }

    @Override
    public int compareTo(Student otherStudent) {
        return name.ordinal() - otherStudent.name.ordinal();

        // example if Tresten is comparing against Klari would return -1 which means that Klari > Tresten
        // example if Tresten is comparing against Briana would return -2 which means that Briana > Tresten
        // example if Tresten is comparing against Tresten would return 0 which means that Tresten == Tresten

        // ordinal() is a method you can call on an enum to return the index in the enum, if we wanted to change the order we would just have to 
        // ... change the order in the enum
    }

}
```

  - We have to pass the **Student** into the Comparable Type parameter on **line 3** to tell the **interface** to take in a **Student** as an argument for the **compareTo()** method

# Comparator interface
  - the **Comparator** interface is similiar to the **Comparable** interface, and they often get confused for one another
  - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/compareto.png)
  - They both have **different method signatures**
  - it's common practice to include a **Comparator** as a **nested class**

```java
public interface Comparator<T> {
  int compare(T o, T o2);
}
```

  - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/comparable_comparator.png)

```java
public class StudentGPAComparator implements Comparator<Student> {

    @Override
    public int compare(Student o1, Student o2) {
        return (String.valueOf(o1.gpa)).compareTo(String.valueOf(o2.gpa));
    }

}
```

```java
public static void main(String... args){
  // create the students
  Student student1 = new Student("Tresten");
  Student student2 = new Student("Briana");
  Student student3 = new Student("Bianca");

  // fill the array
  Student[alt-text] studentsArray = new Student[alt-text]{student3, student1, student2};

  // create instance of the Comparator
  Comparator<Student> gpaSorter = new StudentGPAComparator();

  // sort the array in reverse order
  Arrays.sort(studentsArray, gpaSorter.reversed());
}

```

  - to sort in reverse order just use the **.reversed()** method on the class that implements **Comparator**







# Generic Method example
  
  -  For the following assume the following. A subclass LPAStudent extends the Student base class

```java
public class Student {
  // implementation goes here
}

public class LPAStudent extends Student{
  // implementation goes here
}
```

  - In the main function we are creating an arraylist of LPAStudents
  - We also create a static function called printList() which takes in a List of Students as an argument
    - We will get a compiler error if we try to call printList(students) with a list of LPAStudents even though it is a subclass of Student

```java
    public static void main(String... args){
        // regular students
        int studentCount = 10;
        List<Student> students = new ArrayList<>();
        for(int i = 0; i < studentCount; i++){
            students.add(new Student());
        }
        students.add(new LPAStudent()); // we can add an lps student to the List<Student>
        printList(students);

        // lpa students
        int lpaStudentCount = 10;
        List<LPAStudent> lpaStudents = new ArrayList<>();
        for(int i = 0; i < lpaStudentCount; i++){
            lpaStudents.add(new LPAStudent());
        }

        printList(lpaStudents); // this gives compiler error because LPAStudent doesn't inherit from the Student class
        // however, if we removed the <Student> out of the type parameter for the printList method this would work but it would mean that
        // ... List is using raw generic type, which is bad

    }

    public static void printList(List<Student> students){
        for (var student : students){
            System.out.println(student);
        }
        System.out.println();
    }
```

  - So how do we get around this ???
    - but we can also use a generic wildcard shown later
    - or we can create a generic method with type parameters like shown below

```java
// now the parameter will be a class that is upper bounded by the Student class meaning any subclass of Student
public static <T extends Student> void printList(List<T> students){
    for (var student : students){
        System.out.println(student);
    }
    System.out.println();
}
```

  - When used as a **reference types**, a container of one type has **no relationship** to the same container of another type, even if the contained types do have a relationship
  - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/reference_types.png)


## Limitation of a reference of generic classs with a list argument
  - When we declare a variable or method parameter with 
    - `List<Student>`
    - Only List subtypes with Student elements can be assigned to this variable or method argument like the following:
      - `ArrayList<Student>()`
      - `LinkedList<Student>()`
    
  
# Generic Type Parameters
  - Type parameters are placed after any modifer and before the methods return type
  - Type parameters can be referenced in the:
    - method parameters
    - method return type
    - method code block
  - We can also add an upperbound to the generic type

```java
public static <T extends Student> void printList(List<T> students){
    for (var student : students){
        System.out.println(student);
    }
    System.out.println();
}
```
# Multiple bounds
  - you can specifiy a type parameter to be a subclass of multiple base classes as shown below
  - if you extend a class and an interface, the class be listed first
  - **you can extend up to one class at most**
  - **you can extend zero to many interfaces**
  
```java
  public class GenericClass<T extends AbstractClassA & interfaceA & interfaceB>
  {
    // implementation ...
  }
```

# Generic Wildcards
  - Generic method that use type parameters are **different** than generic wildcards
  - **Wildcards** are represented by a question mark **?**
  - Wildcards cannot be used to define a generic class or interface
  - A **wildcard** can only used in a **type argument**, **not** in the **type parameter declaration** like below
    - `public static void myFunc(List<? extends Animal> inputList){ ... }` This is OKAY in a type argument
    - `Team<? extends Player> myteam = new Team<>();` This would NOT BE VALID in a **type parameter declaration** 


```java
// using generic wildcard that means that the List parameter can accept any subtype of Student
public static void printList(List<? extends Student> students){
    for (var student : students){
        System.out.println(student);
    }
    System.out.println();
}
```

## Wildcard upperbound, lowerbound
  - ![alt-text](/2023-09-13-section-12-generics-udemy-java-programming-masterclass/bounded.png)

## Type Erasure
  - Generics exist to enforce **tighter type checks**, at **compile time**.
  - The compiler **transforms** a **generic class** into a **typed class**, meaning the byte code, or class file, contains no type parameters
  - Everywhere a type parameter is used in a class, it gets replaced with either the type **Object**, if no upperbound was specified. or the upper bound type itself
  - This transformation process is called **type erasure**, because the **T parameter is erased**, or **replaced with a true type**
  - Understanding how type erasure works for overloaded methods, may be imporant

  - Example
```java
public static  <E> boolean containsElement(E [alt-text] elements, E element){
    for (E e : elements){
        if(e.equals(element)){
            return true;
        }
    }
    return false;
}
```

  - gets transformed into this since the Type E was **unbounded** and thus gets turned into the Object type at compile-time
 
```java
public static  boolean containsElement(Object [alt-text] elements, Object element){
    for (Object e : elements){
        if(e.equals(element)){
            return true;
        }
    }
    return false;
}
```

## Pitfalls of wildcards

  - in he example below we are accepting a wildcard of Student or any subclass of Student
  - however we get an error on line 5 because it says that we are trying to set the an element in a of subclass Student but not Student with a Student object
  - The compiler is saying that the list students may be a Student but may also be a subtype of Student so it would not be valid

```java
public static void printMoreList(List<? extends Student> students){

    // assigning the first element in the students list to the last student in the list
    Student last = students.get(students.size()-1);
    students.set(0, last); // COMPILE-TIME ERROR: Required type : "capture of ? extends Student" Provided: "Student"

    for (var student : students){
        System.out.println( student);
    }
    System.out.println();
}
```