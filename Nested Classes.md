# Nested Classes

The Java programming language allows you to define a class within another class. Such a class is called a  _nested class_  and is illustrated here:

```java
class OuterClass {
    ...
    class NestedClass {
        ...
    }
}

----------

**Terminology:** Nested classes are divided into two categories: non-static and static. Non-static nested classes are called  _inner classes_. Nested classes that are declared  `static`  are called  _static nested classes_.

----------

class OuterClass {
    ...
    class InnerClass {
        ...
    }
    static class StaticNestedClass {
        ...
    }
}
```

A nested class is a member of its enclosing class. Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private. Static nested classes do not have access to other members of the enclosing class. As a member of the  `OuterClass`, a nested class can be declared  `private`,  `public`,  `protected`, or  _package private_. (Recall that outer classes can only be declared  `public`  or  _package private_.)

## Why Use Nested Classes?

Compelling reasons for using nested classes include the following:

-   **It is a way of logically grouping classes that are only used in one place**: If a class is useful to only one other class, then it is logical to embed it in that class and keep the two together. Nesting such "helper classes" makes their package more streamlined.
    
-   **It increases encapsulation**: Consider two top-level classes, A and B, where B needs access to members of A that would otherwise be declared  `private`. By hiding class B within class A, A's members can be declared private and B can access them. In addition, B itself can be hidden from the outside world.
    
-   **It can lead to more readable and maintainable code**: Nesting small classes within top-level classes places the code closer to where it is used.
    

## Inner Classes

As with instance methods and variables, an inner class is associated with an instance of its enclosing class and has direct access to that object's methods and fields. Also, because an inner class is associated with an instance, it cannot define any static members itself.

Objects that are instances of an inner class exist  _within_  an instance of the outer class. Consider the following classes:

```java
class OuterClass {
    ...
    class InnerClass {
        ...
    }
}
```


An instance of  `InnerClass`  can exist only within an instance of  `OuterClass`  and has direct access to the methods and fields of its enclosing instance.

To instantiate an inner class, you must first instantiate the outer class. Then, create the inner object within the outer object with this syntax:

```java
OuterClass outerObject = new OuterClass();
OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```

There are two special kinds of inner classes:  [local classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html)  and  [anonymous classes](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html).

## Static Nested Classes

As with class methods and variables, a static nested class is associated with its outer class. And like static class methods, a static nested class cannot refer directly to instance variables or methods defined in its enclosing class: it can use them only through an object reference.  [Inner Class and Nested Static Class Example](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#inner-class-and-nested-static-class-example)  demonstrates this.

----------

**Note:** A static nested class interacts with the instance members of its outer class (and other classes) just like any other top-level class. In effect, a static nested class is behaviorally a top-level class that has been nested in another top-level class for packaging convenience.  [Inner Class and Nested Static Class Example](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#inner-class-and-nested-static-class-example)  also demonstrates this.

----------

You instantiate a static nested class the same way as a top-level class:

```java
StaticNestedClass staticNestedObject = new StaticNestedClass();
```

## Inner Class and Nested Static Class Example

The following example,  [`OuterClass`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/OuterClass.java), along with  [`TopLevelClass`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/TopLevelClass.java), demonstrates which class members of  `OuterClass`  an inner class (`InnerClass`), a nested static class (`StaticNestedClass`), and a top-level class (`TopLevelClass`) can access:

### OuterClass.java

public class OuterClass {

```java
    String outerField = "Outer field";
    static String staticOuterField = "Static outer field";

    class InnerClass {
        void accessMembers() {
            System.out.println(outerField);
            System.out.println(staticOuterField);
        }
    }

    static class StaticNestedClass {
        void accessMembers(OuterClass outer) {
            // Compiler error: Cannot make a static reference to the non-static
            //     field outerField
            // System.out.println(outerField);
            System.out.println(outer.outerField);
            System.out.println(staticOuterField);
        }
    }

    public static void main(String[] args) {
        System.out.println("Inner class:");
        System.out.println("------------");
        OuterClass outerObject = new OuterClass();
        OuterClass.InnerClass innerObject = outerObject.new InnerClass();
        innerObject.accessMembers();

        System.out.println("\nStatic nested class:");
        System.out.println("--------------------");
        StaticNestedClass staticNestedObject = new StaticNestedClass();        
        staticNestedObject.accessMembers(outerObject);
        
        System.out.println("\nTop-level class:");
        System.out.println("--------------------");
        TopLevelClass topLevelObject = new TopLevelClass();        
        topLevelObject.accessMembers(outerObject);                
    }
}
```


### TopLevelClass.java

public class TopLevelClass {

```java
    void accessMembers(OuterClass outer) {     
        // Compiler error: Cannot make a static reference to the non-static
        //     field OuterClass.outerField
        // System.out.println(OuterClass.outerField);
        System.out.println(outer.outerField);
        System.out.println(OuterClass.staticOuterField);
    }  
}
```


This example prints the following output:

Inner class:
------------
Outer field
Static outer field

Static nested class:
--------------------
Outer field
Static outer field

Top-level class:
--------------------
Outer field
Static outer field

Note that a static nested class interacts with the instance members of its outer class just like any other top-level class. The static nested class  `StaticNestedClass`  can't directly access  `outerField`  because it's an instance variable of the enclosing class,  `OuterClass`. The Java compiler generates an error at the highlighted statement:

```java
static class StaticNestedClass {
    void accessMembers(OuterClass outer) {
       // Compiler error: Cannot make a static reference to the non-static
       //     field outerField
       **System.out.println(outerField);**
    }
}
```


To fix this error, access  `outerField`  through an object reference:

```java
System.out.println(outer.outerField);
```


Similarly, the top-level class  `TopLevelClass`  can't directly access  `outerField`  either.

## Shadowing

If a declaration of a type (such as a member variable or a parameter name) in a particular scope (such as an inner class or a method definition) has the same name as another declaration in the enclosing scope, then the declaration  _shadows_  the declaration of the enclosing scope. You cannot refer to a shadowed declaration by its name alone. The following example,  [`ShadowTest`](https://docs.oracle.com/javase/tutorial/java/javaOO/examples/ShadowTest.java), demonstrates this:

 
public class ShadowTest {

```java
    public int x = 0;

    class FirstLevel {

        public int x = 1;

        void methodInFirstLevel(int x) {
            System.out.println("x = " + x);
            System.out.println("this.x = " + this.x);
            System.out.println("ShadowTest.this.x = " + ShadowTest.this.x);
        }
    }

    public static void main(String... args) {
        ShadowTest st = new ShadowTest();
        ShadowTest.FirstLevel fl = st.new FirstLevel();
        fl.methodInFirstLevel(23);
    }
}
```


The following is the output of this example:

x = 23
this.x = 1
ShadowTest.this.x = 0

This example defines three variables named  `x`: the member variable of the class  `ShadowTest`, the member variable of the inner class  `FirstLevel`, and the parameter in the method  `methodInFirstLevel`. The variable  `x`  defined as a parameter of the method  `methodInFirstLevel`  shadows the variable of the inner class  `FirstLevel`. Consequently, when you use the variable  `x`  in the method  `methodInFirstLevel`, it refers to the method parameter. To refer to the member variable of the inner class  `FirstLevel`, use the keyword  `this`  to represent the enclosing scope:

```java
System.out.println("this.x = " + this.x);
```


Refer to member variables that enclose larger scopes by the class name to which they belong. For example, the following statement accesses the member variable of the class  `ShadowTest`  from the method  `methodInFirstLevel`:

```java
System.out.println("ShadowTest.this.x = " + ShadowTest.this.x);
```


## Serialization

[Serialization](https://docs.oracle.com/javase/tutorial/jndi/objects/serial.html)  of inner classes, including  [local](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html)  and  [anonymous](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html)  classes, is strongly discouraged. When the Java compiler compiles certain constructs, such as inner classes, it creates  _synthetic constructs_; these are classes, methods, fields, and other constructs that do not have a corresponding construct in the source code. Synthetic constructs enable Java compilers to implement new Java language features without changes to the JVM. However, synthetic constructs can vary among different Java compiler implementations, which means that  `.class`  files can vary among different implementations as well. Consequently, you may have compatibility issues if you serialize an inner class and then deserialize it with a different JRE implementation. See the section  [Implicit and Synthetic Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html#implcit_and_synthetic)  in the section  [Obtaining Names of Method Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html)  for more information about the synthetic constructs generated when an inner class is compiled.