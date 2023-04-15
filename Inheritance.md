# Inheritance

## Subclasses and superclasses

-   **Inheritance**  is a technique that allows one class to be  _derived_  from another.
-   A derived class inherits all of the data and methods from the original class

Example: Suppose that class Y is _inherited_ from class X.

-   class X is the  **superclass**. Also known as  _base class_  or  _parent class_
-   class Y is the  **subclass**. Also known as the  _derived class_, or  _child class_, or  _extended_  class
-   class Y consists of anything created in class Y,  _as well as_  everything from class X, which it inherits

### Declaring a subclass

Use the keyword extends to declare the derived class

  // **Example 1**
  public class AAA		// AAA is the base class
  { ... }

  public class BBB extends AAA  // BBB is the derived class
  { ... }


  // **Example 2**
  public class Employee {...}				// base class
  public class HourlyEmployee extends Employee { ... }  // derived

### The keyword  super

-   When you create a derived object, the derived class constructor needs to invoke the base class constructor
-   Do this with the keyword  super  -- in this context, it acts as the call to the base class constructor
    
      super();		// invokes base class default constructor
      super(parameters);    // invokes base class constructor with parameters
    
      // Example, for a class called HourlyEmployee, derived from Employee
      public class HourlyEmployee extends Employee
      {
        public HourlyEmployee()	// default constructor
        {
    	super();		// invokes Employee() constructor
        }
    
        public HourlyEmployee(double h, double r)
        {
    	super(h,r);		// invokes Employee constructor w/ 2 parameters
        }
        
        // ... more methods and data
    
      } // end class HourlyEmployee
    
-   The call to  super()  must be the first line of the derived class constructor
-   If explicit call to parent constructor not made, the subclass' constructor will  _automatically_  invoke  super(). (the default constructor of the base class, if there is one)
-   Can also use  super  to invoke a method from the parent class (from inside the derived class). Format:
    
      super.method(parameters)
    

  

### The  protected  modifier

-   Recall that  **public**  data and methods can be accessed by anyone, and  **private**  data and methods can be accessed only by the class they are in.
-   **protected**  data and methods of a public class can be accessed by any classes derived from the given class (this is also true in C++)
-   In Java, a  protected  member can also be accessed by any class in the same  **package**  (to be discussed later)

  

### The  final  modifier

In addition to creating constant variable identifiers, the keyword final can be used for a couple of special purposes involving inheritance:

-   When used on a class declaration, it means that the class cannot be extended. (i.e. it cannot become a parent class to a new subclass)
-   When used on a method declaration, it means that the method cannot be overridden in a subclass. (i.e. this is the final version of the method)

  

### Method Overriding

Although the derived class inherits all the methods from the base class, it is still possible to create a method in the derived class with the same signature as one in the base. Example:

-   Suppose a class Rectangle is derived from class Shape.
-   Shape has a method:
    
      void Draw() { ... }  
    
-   We can define a method in class Rectangle with the same signature. The derived class version will  _override_  the base class version, when called through an object of type Rectangle.
    
      Rectangle r = new Rectangle();  // create a Rectangle object
    				  //  which has all the Shape methods available
    
      r.Draw();			  // invokes the Draw method from the
    				  //  Rectangle class
    
-   Note that the Rectangle class'  Draw()  method can still invoke the superclass' method, with the keyword  super
    
      public void Draw()
      {
        super.Draw();		// invoke parent's Draw()
    
        // continue with any processing specific to Rectangle
      }
    

#### In-class Example

Here's a link to the code example we wrote up in class. Base class is Shape, and Circle is derived from Shape. The Tester.java file contains some sample calls

-   [Shapes](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/inher/shapes/)

  

### Abstract Classes

-   Superclasses are more general and subclasses are more specific.
-   Sometimes a base class is so general that it doesn't make sense to actually instantiate it (i.e. create an object from it).
    -   Such a class is primarily a grouping place for common data and behaviors of subclasses -- an  **abstract class**.
-   To make a class abstract, use the keyword  abstract  (which is a modifier)
    
      public abstract class Shape
    
-   Now that  Shape  is abstract, this would be illegal:
    
      Shape s = new Shape();        // specifically, it's  **new Shape();**
                                    //   that is illegal
    

Methods can be abstract as well:

-   An abstract method is a method signature without a definition
-   Abstract methods can  _only_  be created inside abstract classes
-   The main purpose of an abstract method is to be overridden in derived classes (with the same signature)
-   Example:
    
      public abstract class Shape		// Shape is an abstract class
      {
        public abstract double findArea();	// findArea is an abstract method
    
        // other methods and data
      }
    

----------

## The  Object  class

In Java, **every** class is derived automatiacally from a class called Object. If no specific inheritance is declared for a class, it automatically has Object as a superclass.

While there are several methods in class  Object, here are three important such methods, inherited by every Java class

-   public boolean equals(Object object)
-   public String toString()
-   public Object clone()

Let's look at each.

----------

#### public boolean equals(Object object)

tests whether two objects are equal

  object1.equals(object2)	// returns true if equal, false if not
				// (object1 and object2 same class type)

Default implementation is:

  public boolean equals(Object obj)
  {
	return (this == obj);
  }

Note that this default implementation is equivalent to the == operator, since it only tests the reference variables for equality. The intent is that subclasses of Object should override the equals method whenever they want a test of equality of two objects' **contents**.

----------

#### public String toString()

returns a string that represents the object. Call format:

  objectName.toString();

The default version of the string might not always be useful, but this can be overridden in any derived class. Example for a class called Fraction:

  public String toString()
  {
    return numerator + "/" + denominator;
  }

Assuming the above function for a Fraction class, the following illustrates its usage:

  Fraction f1 = new Fraction(4,5);	// create the fraction 4/5
  System.out.print(f1.toString());	// will print "4/5"

  System.out.print(f1);		// also prints "4/5" as this
				//  always invokes a class' toString method

----------

Examples:

-   [Example of default operation of  equals  and  toString](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/inher/frac1)  -- This uses the Fraction class from a previous notes set
-   [Example of overriding  equals  and  toString](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/inher/frac2)  -- in the Fraction class

----------

#### public Object clone()

Remember, direct assignment between object names will only copy one reference variable to another. Use the clone() method to make copies of objects.

  newObject = someObject.clone();

Not all objects can be cloned. Only objects imeplementing the java.lang.Cloneable interface (which will be discussed later) can use the clone method.

The  clone()  method from the object class does a "shallow copy" (i.e. copies reference variables verbatim). If a "deep copy" is needed (a la copy constructors in C++), you should override  clone()  for a class.

----------

#### Other methods from class  Object

-   finalize  -- called by garbage collector to perform to perform cleanup on an object. Can be overridden, but rarely done
-   getClass  -- returns an object of type  Class, with information about the calling object's type
-   hashCode  -- returns hash value that can be used as a key for the object (for use in a hash table, for example)
-   notify,  notifyAll,  wait  -- related to multithreading
# Polymorphism and Interfaces

## Polymorphism and Dynamic Binding

If a piece of code is designed to work with an object of type X, it will also work with an object of a class type that is derived from X (any subclass of X). This is a feature known as **polymorphism** and is implemented by the Java interpreter through a mechanism called **dynamic binding**. Examples:

-   Suppose there is a base class called  Shape. Suppose that  Rectangle,  Triangle, and  Circle  are all subclasses of  Shape
-   Then it is legal to attach derived objects to the base reference variables:
    
      Shape s1 = new Circle();
      Shape s2 = new Rectangle();
      Shape s3 = new Triangle();
    
-   Suppose a method  findArea()  is called through one of these variables (s1, s2, s3) in the above example. The method must exist in the Shape class, but there can be override versions in the subclasses. If so, then through dynamic binding, the method that runs will be based on the attached object's type, as a priority over the reference variable type (Shape):
    
      s1.findArea();	// runs the findArea() method from the Circle class
      s2.findArea();	// runs the findArea() method from the Rectangle class
      s3.findArea();	// runs the findArea() method from the Triangle class
    
      // if any of these subclasses did not override the finArea() method, 
      //  then the Shape class' findArea() method will run
    
-   If a method expects a parameter of type X, it is legal to pass in an object of a type derived from X in that slot:
    
      // Sample method
      public int draw(Shape s)
      {   // definition code   }
    
      // sample calls
      Shape s1 = new Shape();
      Shape s2 = new Circle();
      Shape s3 = new Rectangle();
    
      draw(s1);		// normal usage
      draw(s2);		// passing in a Circle object
      draw(s3);		// passing in a Rectangle object
    

#### Another example

Notice that a useful application of polymorphism is to store many related items, but with slightly different types (i.e. subclasses of the same superclass), in one storage container -- for example, an array -- and then do common operations on them through overridden functions.

Example: Assume the setup in the previous example, base class  Shape  and derived classes  Rectangle,  Circle,  Triangle. Suppose the base class has a  findArea()  method (probably abstract, since we don't know how to compute the area for a generic shape), and each derived class has its own  findArea()  method.

  Shape[] list = new Shape[size];	// create an array of Shape reference variables
  list[0] = new Circle();		// attach a Circle to first array slot
  list[1] = new Rectangle();		// attach a Rectangle to second slot
  list[2] = new Triangle();		// attach a Triangle to third slot

  // ....   continue in a like manner, attaching a variety of different
  //        shapes to the array.  Note that there could be MANY subcategories
  //        of shapes and MANY array elements.  Notice that we are using 
  //        the polymorphism feature

  for (int i = 0; i < list.length; i++)
     System.out.println("The area of shape # " + i + " = " + list[i].findArea()) 

Note that in this for-loop, the appropriate area methods are called for **each** shape attached to the array, without the need for separate storage for different shape types (i.e. no need for an array of circles, and a separate array of rectangles, etc).

#### Casting

Since a derived object can always be attached to a corresponding base class reference variable, this is a type of casting that is implicitly allowed. Similarly, direct assignment between variables (derived type assigned into base type) in this order is also allowed, as are explicit cast operations.

  Shape s1, s2;		// Shape is the base class
  Circle c;		// Circle is a derived class

  s1 = new Circle();	// automatically legal (as seen above)

  s2 = c;		// automatically legal
  s1 = (Shape)c;	// explicit cast used, but equivalent to above

To convert an instance of a superclass (base) to an instance of a subclass (derived), the explicit cast operation must be used:

  c = s1;		// would be illegal -- cast needed

  c = (Circle)s1;	// legal (though not always so useful)

#### The  instanceof  operator

The instanceof operator checks to see if the first operand (a variable) is an instance of the second operand (a class), and returns a response of type boolean.

  Shape s1;
  Circle c1;
  // other code.....

  if (s1 instanceof Circle)
     c1 = (Circle)s1;		// cast to a Circle variable

----------

## Interfaces

-   Java does not allow multiple inheritance
    -   A subclass can only be derived from one base class with the keyword  extends
    -   In Java, the  **interface**  can obtain a similar effect to multiple inheritance
-   **Interface**  - A construct that contains only constants and abstract methods
    -   Similar to abstract class
    -   Different, since an abstract class can also contain regular variables and methods
    -   Can use as a base type name (just like regular base classes)
    -   Cannot instantiate (like an abstract class)

Format for declaring an interface:

  modifier interface Name
  {
    // constant declarations
    // abstract method signatures - keyword "abstract" not needed
    //   for these.  ALL methods in an interface are abstract
  }

Use the keyword implements to state that a class will use a certain interface. In this example, Comparable is the name of an interface. The class ComparableCircle inherits the data from the Comparable interface, and would then need to implement the methods (to be able to use them).

  class ComparableCircle extends Circle implements Comparable
  {
    // ....
  }

Other rules:

-   Only single inheritance for classes, with  extends
-   Interfaces can inherit other interfaces (even multiple), with  extends
    
        public interface NewInterface extends interface1, ..., interfaceN
      
    
-   classes can implement more than one interface with  implements
    
        public class NewClass extends BaseClass implements interface1, ..., interfaceN
      
    

#### The  Cloneable  interface

A special interface in the Java.lang package which happens to be empty:

  public interface Cloneable
  {
  }

This is a _marker interface_ -- no data or methods, but special meaning in Java. A class can use the clone() method (inherited from class Object) only if it implements Cloneable.

----------

### [Code Examples from Deitel, Ch. 10](http://www.cs.fsu.edu/~myers/cop3252/notes/deitel7/ch10)