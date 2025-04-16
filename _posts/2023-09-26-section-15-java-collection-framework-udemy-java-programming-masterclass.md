---
layout: post
title: Section 15. (Java Collection Framework) Udemy - Java Programming Masterclass
date: 2023-09-26 16:50 -0500
categories: [Udemy, Java]
tags: [Java, Programming] 
image: 
  path: /2023-09-26-section-15-java-collection-framework-udemy-java-programming-masterclass/profile.png
---

- [Java Collections](#java-collections)
  - [Overview](#overview)
  - [What's in the framework, what's not?](#whats-in-the-framework-whats-not)
  - [Collection is the root of the collection hierarchy](#collection-is-the-root-of-the-collection-hierarchy)
  - [Collection interface methods](#collection-interface-methods)
  - [What's a Collection Class?](#whats-a-collection-class)
- [Collection Types](#collection-types)
  - [List](#list)
  - [Queue](#queue)
  - [Set](#set)
  - [SortedSet](#sortedset)
  - [Map](#map)
  - [Deque](#deque)
- [Collection Helper methods](#collection-helper-methods)
  - [Collections.nCopies(int count, Object o)](#collectionsncopiesint-count-object-o)


# Java Collections

## Overview
  - just an object that represents a group of objects where there is some relationship for them
  - arrays, lists, vectors, sets, queues, tables, dictionaries and maps
  - They are differentiated by the way the store the objects in memory, how they are accesses and ordered, and whether they allow duplicates and null value s

## What's in the framework, what's not?
  - Objects who implement they Collection interface 
    - except: maps

## Collection is the root of the collection hierarchy
  - Everything branches off of the Collection interface
  - ![alt-text](/2023-09-26-section-15-java-collection-framework-udemy-java-programming-masterclass/tree.png)

## Collection interface methods
  - ![alt-text](/2023-09-26-section-15-java-collection-framework-udemy-java-programming-masterclass/collection_methods.png)

## What's a Collection Class?
  - The Collections class is not the Collections Framework

# Collection Types

## List
  - **Ordered**
  - aka sequence

## Queue
  - Ordered
  - Special methods for the first & last elements
  - FIFO / LIFO
  - Stack and Queues

## Set
  - **Unordered**
  - **No Duplicates**

## SortedSet
  - Ordered
  - No Duplicates

## Map
  - Stores **key,value** pairs

## Deque


# Collection Helper methods

## Collections.nCopies(int count, Object o)
  - Similiar to Arrays.fill()
  - Collections has Collections.fill() but it doesn't work
  
```java
List<Card> king_of_clubs = Collections.nCopies(2, Card.getFaceCard(Card.Suit.CLUB, 'K'));
```


  