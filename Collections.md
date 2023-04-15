## 

### Overview

-   The Java  **collections framework**  contains pre-packaged data structures, interfaces, and algorithms

-   Similar to the idea of the C++ Standard Template Library
-   Since version 1.5.0, uses generics, as well

-   Involves classes and interfaces in the package  java.util
-   A  **collection**  is a data structure, an object that stores groups of other objects (or object references) in a single unit.
    -   In previous versions of Java, collections stored  Object  references
    -   Since 1.5.0, generics are used, so exact types can be specified
-   [Link to Tutorial Trail on the Collections Framework (Java web site)](http://docs.oracle.com/javase/tutorial/collections/index.html)

### What does the collections framework consist of?

-   [Interfaces](http://docs.oracle.com/javase/tutorial/collections/interfaces/index.html)  -- representing abstract data types. Operations are not dependent on the physical storage representation
    -   [Collection](http://java.sun.com/javase/6/docs/api/java/util/Collection.html)  - This is the root interface in the collection hierarchy
-   [Implementations](http://docs.oracle.com/javase/tutorial/collections/implementations/index.html)  -- reusable data structures. These are the actual implementations, with specific storage setups.
-   [Algorithms](http://docs.oracle.com/javase/tutorial/collections/algorithms/index.html)  -- methods that perform common algorithms and manipulations. Set up to be reusable across multiple types of implementations.
    -   [Collections](http://java.sun.com/javase/6/docs/api/java/util/Collections.html)  -- this is a class that contains mostly static methods for manipulating collections -- the algorithms

### Quick reference to common collection interfaces and classes

-   **List**: an ordered container that can contain duplicate elements. In Java, an interface.
    -   **Vector**: Resizable array-based list of elements of same type. Synchronized (for use in multi-threading).
    -   **ArrayList**: Like a Vector, but unsynchronized (faster than Vector, typically)
    -   **LinkedList**: an implementation of a list where the data is not consecutive, but rather a linear group of linked nodes
-   **Stack**: a "last in first out" (LIFO) data structure. In Java, it extends class Vector
-   **Queue**: a "first in first out" container. Like waiting in line to be served. An interface in Java
    -   **PriorityQueue**: an implementation of a queue that allows elements to be inserted in such a way that higher priority elements will be removed first
-   **Set**: a collection that contains unique elements (like a mathematical set -- no duplicates). An interface, in Java. Common classes that implement are:
    -   **HashSet**: a set that stores elements in a hash table
    -   **TreeSet**: a set that stores its elements in a tree, a non-linear group of linked nodes
-   **Map**: Used for associating keys to values, in a one-to-one mapping. (An interface in Java). Common classes that implement:
    -   **HashTable**  - a hash table is a way to use key values from a large range and still get high-speed lookups without using too much storage
    -   **HashMap**  - like HashTable, but unsynchronized
    -   **TreeMap**  - tree-based implementation of a Map

----------

### [Deitel Examples](https://www.cs.fsu.edu/~myers/cop3252/notes/deitel7/ch19/)