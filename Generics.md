# Generics

### Summary

-   Feature added in Java 1.5.0, and similar to C++ templates
-   Can use in methods and in classes
-   Uses type parameters, in angle brackets  < >, just like C++ templates -- one or more type parameters, separated by commas
-   Unlike C++ templates, only  **reference types**  can be used with generic methods and classes (i.e. no primitive types, like  int,  float, etc).
-   Syntactially similar to C++ templates, but instantiated differently when compiled.
    -   A C++ template generates separate copies of the code for each instantiated type
    -   Java typically uses one compiled version, where the type parameter is replaced with a more general parent type (thus making legal calls via polymorphism)
-   Helps eliminate many situations in which casting was previously necessary

----------

### Generic methods

#### Basic usage

Set up by putting a type parameter before the method's return type, and use the type parameter name in place of fixed types in the method signature (and definition, if necessary). Example:

 public static < T > void PrintArray( T[] arr )

-   Type parameters receive actual type arguments when the method is called
    -   Operations in the method body must be legal for the type arguments used in the call, or compiler errors will occur
-   Type parameters can represent only reference types, not primitive types
-   **Type Erasure**: When instantiated, the above translates to the method:
    
     public static void PrintArray(Object[] arr)
    
    This process of replacing the type parameters with actual types is called  **type erasure**.

#### Upper Bounds of Type Parameters

-   In the process of erasure, type parameters are replaced with their  **upper bound**
-   Unless specified otherwise,  Object  is the default upper bound for type parameters
-   To declare an upper bound on a type parameter, use the keyword  **extends**, followed by the class or interface that is to be the upper bound.
-   Example:
    -   If a generic method will use the  compareTo  method, declare the  Comparable<T>  generic interface as the upper bound with:
        
          public static < T extends Comparable< T > > T minimum(T x, T y, T z)
         
        
    -   Note that  Comparable< T >  objects  **will**  have a  compareTo()  method.  
        The translated version of the method after erasure will be:
        
          public static Comparable minimum(Comparable x, Comparable y, Comparable z)
         
        
    -   Now, the following call is legal, since  String  implements  Comparable<String>
        
          String min = minimum("one", "three", "eight");
         
        
    -   **Special case**: Even though type parameters can only take reference types, the following calls are legal due to an added feature since Java 1.5.0, called  **autoboxing**, where primitive types (like  int) can sometimes be auto-converted to objects of the corresponding "type wrapper" class (like  Intetger):

```java
int m1 = minimum(6, 9, 10);
double m2 = minimum(3.3, 10.5, 1.1);
```


-   Questions to ask yourself:
    -   If the compiler translates the generic method into a regular method using the upper bound type, why not write it that way in the first place?
    -   Or more specifically, what's the benefit of the "generic" method (as opposed to just using regular polymorphism, with interface or base class types as parameters and returns)?

----------

### Generic Classes

#### Creating a generic class

-   A generic class is declared like a regular class, with a type parameter section after the class name:
    
     public class Table< T >
    
-   The type parameter(s) can be used throughout the class, including in generic methods, to represent the element type(s)
-   The type parameter cannot be used after  new, to create objects or arrays. To create an array, for example, create an array of type  Object  (or whatever the type parameter's upper bound is), and then downcast the reference variable to the generic type:

```java
private T[] list;		// array variable, i.e. in a class

list = (T[]) new Object[size];	// creation of array of reference variables
```


#### Using a generic class

-   When declaring instances of a generic class, fill in the type parameter with an actual type argument
-   Example:
    
     // Suppose the following is a generic class:
     public class List< T > { // ... }
    
    Then the following are valid declarations of variables and objects:
    
     // suppose these are instance variables of a class
     private List< Double > dlist;
     private List< String > slist;
    
     // creation of objects
     dlist = new List< Double > (10);	// List of Doubles
     slist = new List< String > (20);	// List of Strings
    
-   Generic class types can be used as parameters in generic methods:
    
     public < T > void doSomething(List< T > x, T[] elements)
    
-   For backwards compatibility with older versions of Java, it is often possible to instantiate a generic class without a type argument. In this instance, a  **raw type**  is being used for the type argument:
    
     // this one implicitly uses Object as type argument
     List x = new List(5);	
    
     // this one is allowed because Int is a subclass of Object (used for the 
     //  type argument of the variable y)
     List y = new List< Integer > (5);
    
     // this one is permitted, but less safe, since the List object is not
     //  guaranteed to store type Double, although the variable is set that way.
     //  Compiler will probably issue a warning
     List< Double > dList = new List(10);
    

#### Wildcards in Methods that Accept Type Parameters

-   Suppose we have this method:
    
     public static double average(List< Number > x)  { // ... }
    
    -   Note that  java.lang.Number  is a base class for all the numeric type wrapper classes (like  Integer,  Float, etc).
    -   Numbers of various types could be stored in a  List<Number>  object
    -   BUT, a  List<Double>  object could not be passed into this method. Nor could a  List<Integer>  object.
    -   While  Number  is a superclass of  Integer  and  Double, the class  List<Number>  would not be considered a superclass of  List<Double>  and  List<Integer>
-   To make the above method more versatile (and accept these types), we can use a  **wildcard**, denoted by the question mark (?), and represents "unknown type"
    
     
     public static double average(List< ? extends Number > x)  { // ... }
    
    -   The unknown type may be filled with  Number  or any subclass of  Number  (like  Double  or  Integer)
    -   Number  is an upper bound
    
      
    
-   Other varieties of wildcards
    -   If  **<?>**  is used, it means  _any_  type could fill this slot:
        
           public static void func(List< ? > x)  { // ... }
           // any List object (with any type filled in) could be sent in
         
        
    -   If  **< ? super T >**  is used, this sets up  T  as a  _lower bound_  on the type that fills the slot
        
           public static void func(List< ? super Number > x)  { // ... }
           // can send in a List object instatiated with Number, or a
           //  super-type (a parent)
         
        

----------

### [Deitel Examples -- Chapter 18](https://www.cs.fsu.edu/~myers/cop3252/notes/deitel7/ch18/)