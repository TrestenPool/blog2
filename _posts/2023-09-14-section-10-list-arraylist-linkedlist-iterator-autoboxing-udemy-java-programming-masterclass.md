---
layout: post
title: Section 10. (List, ArrayList, LinkedList, Iterator, Autoboxing) Udemy - Java
  Programming Masterclass
date: 2023-09-14 10:45 -0500
categories: [Udemy, Java]
tags: [Java, Programming, Udemy] 
image: 
  path: /2023-09-14-section-10-list-arraylist-linkedlist-iterator-autoboxing-udemy-java-programming-masterclass/profile.png
---

- [Arrays](#arrays)
  - [Notes](#notes)
  - [Declaration](#declaration)
  - [Instanciating](#instanciating)
  - [Print](#print)
  - [Sorting](#sorting)
  - [Searching](#searching)
  - [Equality](#equality)
  - [Fill](#fill)
  - [CopyOf](#copyof)
  - [Multi-Dimensional arrays](#multi-dimensional-arrays)
    - [Declaration](#declaration-1)
    - [Printing](#printing)
    - [Lambdas](#lambdas)
- [Iterator](#iterator)
  - [Iterator Position](#iterator-position)
  - [ListIterator](#listiterator)
- [List, ArrayList, LinkedLists, Iterator, Autoboxing](#list-arraylist-linkedlists-iterator-autoboxing)
  - [ArrayList](#arraylist)
  - [LinkedList](#linkedlist)
  - [Arrays.asList() vs List.of() when instanciating](#arraysaslist-vs-listof-when-instanciating)
- [Autoboxing, Unboxing](#autoboxing-unboxing)
  - [Autoboxing](#autoboxing)
  - [Unboxing](#unboxing)



# Arrays
  - arrays

## Notes
  - Arrays are not resizable
  - You can't add or delete elements
  - You can only modify values 

## Declaration
```java
int[alt-text] integerArray;
String[alt-text] nameList;

// not as common to have the square brackets after the array variable name
String courseList[alt-text];
```

## Instanciating
  - `int[alt-text] integerArray = new int[10];`


## Print
  - Easy way to print out all elements out instead of using a for or for each loop is to use the static method in Arrays

```java
public static void Main(String... args){
  int[alt-text] integerarray = {1,2,3,4,5,6,6};

  System.out.println(Arrays.toString(integerarray));
}
```

## Sorting
  - `Arrays.sort(myintarray);`
  - You have to use the static method **sort** in Arrays class


## Searching
  - Best way to search through a sorted array is using `Arrays.binarySearch(arr, "key");`
    - returns the index of where it found the element, -1 if not found
    - has to be sorted before using

## Equality
  - you can check if two arrays have the same elements with `Arrays.equals(arr1, arr2);`

## Fill
  - `Arrays.fill(myintarray, 0);`
  - This will fill all of the elements in the array with 0

## CopyOf
  - `int[alt-text] secondarr = Arrays.copyOf(myintarray, myintarray.length);`

## Multi-Dimensional arrays

### Declaration
  - standard matrix declaration

```java
// declare 3x3 matrix, defaults to 0's
int[alt-text][alt-text] array = new int[3][3];
```
  - Multi-dimensional array with varrying lengths

```java
// 3 row matrix varrying lengths of rows
int[alt-text][alt-text] matrix = new int[3][alt-text];

matrix[0] = new int[5];
matrix[1] = new int[2];
matrix[2] = new int[3];
```

### Printing
  - easiest way to print out multi dimensional array with **Arrays.deepToString()**
```java
System.out.println(Arrays.deepToString(matrix));
```

### Lambdas  
  - The Arrays class has many methods you can use on it to achieve different tasks
  - Arrays.fill() Arrays.setAll() Arrays.replaceAll()
  - here is an example of using Arrays.setAll() on an array
    - setAll() takes in an array of any type and an IntegerFunction with the following method signature
      - `R apply(int value);`

```java
  String[alt-text] firstNames = new String[alt-text]{
          "Tresten", "Briana", "Kim", "Anna", "Timmy", "Josh", "Dave", "Quin"
  };
  Arrays.setAll(firstNames, (i) -> firstNames[i].toUpperCase());
```

  



<!--------------------------------------------------------------------------->
<!------------------------------- ITERATORS --------------------------------->
<!--------------------------------------------------------------------------->
# Iterator
  - Notes
    - Iterator starts off before the first element, meaning it is not pointing to anything when you first get the iterator
    - Only goes forward
    - Cannot get the current element it is currently pointed to, it can only go to the next object and return you that object
    - You can't reset an interator, once it finishes its traversal it is done, if you wanted to reset it you would have to request a new iterator
  
  - methods
    - **Collection.iterator()** - get the iterator
      - `Iterator iterator = Collection.iterator()`
    - **Iterator.hasNext()** - Checks to see if there is another element to go to next
      - `while(iterator.hasNext())`
    - **Iterator.next()** - goes to the next element
      - `iterator.next()`
    - **Iterator.remove()** - removes the element that is currently at the cursor of the iterator

## Iterator Position
  - The iterator position never at an index but between the indexes
  - ![alt-text](/2023-08-27-java-programming-masterclass-udemy/iterator.png)

## ListIterator
  - Notes
    - there is a list iterator
    - Adds a couple more methods
      - **ListIterator.previous** - Goes to the prevoius object 
    - Adds an object at the current cursor
      - **ListIterator.add()** - Adds an object at the current position in the list
    - Removes an object in the current cursor




<!--------------------------------------------------------------------------->
<!--------- Lists, Arraylist, LinkedList, Iterator, Autoboxing ------------->
<!--------------------------------------------------------------------------->
# List, ArrayList, LinkedLists, Iterator, Autoboxing
  - They are **java containers**
  - **No support** for **primitive** datatypes 
  - Why do we have these in the first place when we have arrays
    - Arrays are mutable but **do not** **allow for resizing**
  - List is the interface that classes like the ArrayList implement to achieve consistency
  - Make sure to specify a type in the diamond brackets because otherwise it will default to the **raw parameterized type**
    - `ArrayList mylist = new ArrayList(); // raw type`
    - `ArrayList<Integer> mylist = new ArrayList<>() //  specifying type;`
      - Make sure to include the <> on the right side of the assignment otherwise it will default to raw type

## ArrayList
  - Differences between arrays and arraylists
    - ![alt-text](/2023-08-27-java-programming-masterclass-udemy/array_arraylist.png)
    - ![alt-text](/2023-08-27-java-programming-masterclass-udemy/array_arraylist_search.png)
    - ![alt-text](/2023-08-27-java-programming-masterclass-udemy/array_arraylist_sort.png)
  - implments List
  - Does not implement Synchronizable therefore is **not thread-safe**
  - Maintains an array in memory that is actually bigger than what we need in most cases
  - Keeps track of the capacity and the size of the array and resizes if needed behind the scenes
  - ```java
    ArrayList<GroceryItem> grocerList = new ArrayList<>();
    grocerList.add(new GroceryItem("milk"));
    grocerList.add(new GroceryItem("yogurt"));
    grocerList.add(new GroceryItem("apples", "Produce", 6));

    System.out.println(grocerList);
  ```
  - instanciating an array with **Arrays.asList()**
  - ```java
    ArrayList<String> arrayList = new ArrayList<>(Arrays.asList("Hello", "World"));
  ```

## LinkedList
  - Can be more performance efficient if you are performing a majority of operations at the head or end of the list

## Arrays.asList() vs List.of() when instanciating
  - Arrays.asList() returns a mutable list
  - List.of() returns an immutable list

```java
List<Integer> list = Arrays.asList(1, 2, 3);
list.set(1, 10); // OK

List<Integer> list = List.of(1, 2, 3);
list.set(1, 10); // Fails with UnsupportedOperationException
```

  - Arrays.asList() allows null elements
  - List.of() does not allow null elements

```java
Integer[alt-text] array = {1,2,3};
List<Integer> list = Arrays.asList(array);
array[1] = 10;
System.out.println(list); // Prints [1, 10, 3]

Integer[alt-text] array = {1,2,3};
List<Integer> list = List.of(array);
array[1] = 10;
System.out.println(list); // Prints [1, 2, 3]
```
  - Arrays.asList() returns a view of the passed array, so the changes to the array will be reflected in the list too.
  - List.of() returns a completely new immutable list that does not refelect changes in the new array

<!--------------------------------------------------------------------------->
<!----------------------- AUTOBOXING, UNBOXING ------------------------------>
<!--------------------------------------------------------------------------->
# Autoboxing, Unboxing
  - Autoboxing
    - Going from primitive to wrapper class
  
  - Unboxing
    - Going from a wrapper to a primitive

## Autoboxing
  - **Integer.valueOf()** - Converts int to Integer

  ```java
  // manually doing it ourselves
  int x = 15;
  Integer integer = Integer.valueOf(x);

  // Letting java do it for us (PREFERRED)
  Integer intWrappper = x;
  ```

## Unboxing
```java
Integer integer = 15;

// manually unboxing
int intval = integer.intValue();

// letting java do it for us (PREFFERED)
int intval = integer;
```
