# Intro to GUI Libraries in Java

## Graphics Libraries

-   In the original version of Java, graphics components were in the AWT library (Abstract Windows Toolkit)
    
    -   Was okay for developing simple GUI applications
    -   For different platforms, AWT components mapped to platform-specific components
    -   Prone to platform specific bugs
    -   Primary package:  [java.awt](http://java.sun.com/javase/6/docs/api/java/awt/package-summary.html). See other awt package APIs on the java.sun site
    
      
    
-   When Java 2 was released, a library known as the  **Swing components**  were introduced with the idea of replacing the older AWT user-interface components (like  Button,  TextField,  TextArea, etc).
    
    -   less dependent on target platform
    -   a more robust and flexible library
    -   Primary package:  [javax.swing](http://java.sun.com/javase/6/docs/api/javax/swing/package-summary.html). See other swing package APIs on the java.sun site
    
      
    
-   Since release of Java 2, the Swing components are recommended for building graphic user interfaces for later browsers. Keep in mind that earlier browser versions may not be able to handle these. For now, the AWT components should still work in applets in most browsers, as well.

## Components and Containers

### Components

-   A graphics  **component**  is an object having a graphical representation that can be displayed on screen and that can interact with the user
-   Some examples of components:
    -   button
    -   check box
    -   text field
    -   combo box
-   [class  Component](http://java.sun.com/javase/6/docs/api/java/awt/Component.html): A class that serves as a basis for all non-menu graphic user interface classes
-   [class  JComponent](http://java.sun.com/javase/6/docs/api/javax/swing/JComponent.html): This class is the basis for all  **Swing**  components (except for the  _top level containers_)

### Containers

-   A  **container**  is a GUI component that can contain other components
    -   Note that a container  _is_  a component itself
    -   But more specifically, it can be used to hold other components in a specific area
-   Examples of GUI containers:
    -   window
    -   panel
    -   tabbed pane
    -   scroll pane
-   [class  Container](http://java.sun.com/javase/6/docs/api/java/awt/Container.html): This class library forms a basis for containers
-   A  **top level container**  is a special container that is intended to be the outermost container for some GUI context. In Java, there are three top level containers:
    -   Frame -- the outer container for an application window
    -   Applet -- the outer container for a Java applet
    -   Dialog -- the outer container for a dialog box
-   In the Swing libraries, these three top-level containers are in these three classes:
    -   [JFrame](http://java.sun.com/javase/6/docs/api/javax/swing/JFrame.html)
    -   [JApplet](http://java.sun.com/javase/6/docs/api/javax/swing/JApplet.html)
    -   [JDialog](http://java.sun.com/javase/6/docs/api/javax/swing/JDialog.html)
-   One very useful general purpose container:  [JPanel](http://java.sun.com/javase/6/docs/api/javax/swing/JPanel.html)
    -   A panel is an invisible container that can be used for storing components. It can be nested in other containers, and it can also be used as an easy drawing canvas

## Events

-   _Event_: A signal that something has happened in a program. Examples: Button clicks, mouse movements, menu selections
-   GUI programs generally driven by events, rather than a specific procedural order
-   Events are handled with event objects. These are triggered by actions on source objects (components or objects on which the event is generated), and they must implement corresponding event listener interfaces. The listener listens for the event, and invokes an event handler when event occurs
-   [java.util.EventObject](http://java.sun.com/javase/6/docs/api/java/util/EventObject.html): Base class for event classes in Java

Some examples of event types:

-   ActionEvent - clicking a button, pressing return on a text field
-   ItemEvent - clicking a check box, selecting an item
-   WindowEvent - Closing a window, opening a window
-   ContainerEvent - component added to a container
-   ComponentEvent - resizing a component, hiding a component
-   TextEvent - changing a text value
-   MouseEvent - clicking the mouse, dragging the mouse
-   KeyEvent - pressing a key on the keyboard

These are just a few examples, not a comprehensive list.


# class JOptionPane

## Intro

-   While it will take some more understanding of classes and other language concepts to fully dig into many Swing components and containers,  JOptionPane  is an easy one that we can use right away
-   [class  JOptionPane](http://java.sun.com/javase/6/docs/api/javax/swing/JOptionPane.html): API Description
-   JOptionPane is a class library that makes it easy to pop up a simple dialog box that either provides an information message or asks for a simple input from the user
-   While the class has a lot of methods, most uses of this class are through a few  static  methods
    -   Remember that this means you can call upon such features through the class name, without having to build objects

## Simple Dialog Box types

-   **Message**  dialog box
    -   This is a simple information dialog box
    -   To use it, call one of the  showMessageDialog()  methods
    -   These are  void  methods, so just call them by themselves to pop up a message box
-   **Input**  dialog box
    -   This is a dialog box that allows a user to type in some input
    -   To use it, call one of the  showInputDialog()  methods
    -   These methods return the input as a  String. Such calls should capture the returned value
-   **Confirm**  dialog box
    -   This is a dialog box that presents the user with a Yes/No/Cancel option
    -   To use it, call one of the  showConfirmDialog()  methods
    -   These methods return the user's answer as an  int  value.
    -   The returned integer value can be tested against pre-defined constants, shown in the Field Summary for the class

## A few simple things about Strings

-   You can assign a string literal to a variable of type  String:

```java
String s1, s2, s3;
s1 = "Hello World";
s2 = "Goodbye";
s3 = "World";
```

-   Just like we can concatenate strings inside of print calls, we can concatenate strings anywhere -- with literals and with String variables:

``

-   There is also a  static  method in class  String  called  format(). You can use this to  _return_  a string that uses  printf  style formatting. Example:
    
      String s5;
      s5 = String.format("Pi to 3 decimal places = %.3f", Math.PI);
    

## Using message dialogs

-   There are three versions of  showMessageDialog()
    
      void showMessageDialog(Component parentComponent, Object message) 
    
      void showMessageDialog(Component parentComponent, Object message, 
                                       String title, int messageType) 
    
      void showMessageDialog(Component parentComponent, Object message, 
                                       String title, int messageType, Icon icon) 
    
-   The parameters:
    1.  _parentComponent_: indicates what component this dialog will pop up over. Use  null  to make the message not connected to any other component
    2.  _message_: This is the actual message being displayed.
    3.  _title_: The string that will appear in the pop-up window's title bar
    4.  _messageType_: Use one of these static constants from the class. Except for plain message, each one uses a special icon on the message box
        -   PLAIN_MESSAGE
        -   ERROR_MESSAGE
        -   INFORMATION_MESSAGE
        -   WARNING_MESSAGE
        -   QUESTION_MESSAGE
    5.  _icon_: A custom icon to use
-   Note that all calls use the first two parameters. The others can be used optionally
-   [Try this sample program](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/jop/JOP1.java)

## Using input dialogs

-   There are several versions of  showInputDialog. Some of these have very similar options as the  showMessageDialog  methods
-   However, the easiest form is simply to pass in a message prompt as a single parameter. Example:
    
      String s1;
      s1 = JOptionPane.showInputDialog("Please enter an integer:");
    
-   Note that in the above call, we captured the  _return value_  into a variable. The  showInputDialog  call will always return the entered value
-   Also note that this value always comes back as a  String
-   If you want to save the entered data as a different type, you will need to convert it

### Converting Strings to primitive types

-   Each primitive type has a corresponding class in  java.lang
-   Each of these classes has a static method that does a type conversion from  String  to the appropriate type
-   Example:
    
      String s1;
      s1 = JOptionPane.showInputDialog("Please enter an integer:");
    
      int value = Integer.parseInt(s1);	// converts s1 into an integer  
    
-   The table below lists the class that goes along with the primitive type, as well as the conversion method
    
    Primitive type
    
    Corresponding wrapper class
    
    static conversion method
    
    boolean
    
    Boolean
    
    boolean parseBoolean(String)
    
    byte
    
    Byte
    
    byte parseByte(String)
    
    short
    
    Short
    
    short parseShort(String)
    
    int
    
    Integer
    
    int parseInt(String)
    
    long
    
    Long
    
    long parseLong(String)
    
    float
    
    Float
    
    float parseFloat(String)
    
    double
    
    Double
    
    double parseDouble(String)
    
-   [Example program showing inputs](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/jop/JOP2.java)

## Using confirm dialogs

-   There are several versions of  showConfirmDialog. Most of these have very similar options as the  showMessageDialog  methods
-   Parameters: All calls use the first two. Others are optional
    1.  _parentComponent_: Same as for message dialogs
    2.  _message_: Same as for message dialogs
    3.  _title_: Same as for message dialogs
    4.  _optionType_: Can be one of these static class constants:
        -   YES_NO_OPTION
        -   YES_NO_CANCEL_OPTION
        -   OK_CANCEL_OPTION
    5.  _messageType_: Same as for message dialog
    6.  _icon_: Same as for message dialog
-   These methods each return an integer value. That value can be captured, and then compared against one of the following static constants, to determine which one was selected:
    -   YES_OPTION
    -   NO_OPTION
    -   CANCEL_OPTION
    -   OK_OPTION
-   Sample call:
    
      int ans = JOptionPane.showConfirmDialog(null, "Are you a good student?",
                            "Student query", JOptionPane.YES_NO_OPTION);
    
      if (ans == JOptionPane.YES_OPTION)
         JOptionPane.showMessageDialog(null, "Hurrah!  A good student!");
      else
         JOptionPane.showMessageDialog(null, "Not another bad student!");
    
-   [Sample program that illustrates some Confirm Dialog boxes](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/jop/JOP3.java)
# Graphics and painting

(Chapter 12)

## paint()  methods

-   Lightweight Swing components that extend class  JComponent  have a method called  paintComponent, with this prototype:
    
      public void paintComponent(Graphics g)
    
-   Another similar method is the  paint  method in class  Component  (and thus all its children) with this prototype:
    
      public void paint(Graphics g)
    
-   The  JComponent  version of  paint()  actually delegates its work to three methods:  paintComponent,  paintBorder, and  paintChildren
-   The idea behind  paint()  is that they are invoked for any component  _automatically_  whenever that component needs to be drawn or re-drawn. Some examples of triggering events:
    -   When the component first is placed on the application
    -   When the component is resized
    -   When the component is covered by some other application, then uncovered and comes to the forefront again
-   Since this is triggered by such events, the programmer seldom needs to call  paint()  or  paintComponent()  explicitly
-   The programmer can call  repaint()  (also a  Component  method) to force the paint operation, if the need arises (i.e. some situation not covered by the automatic calls to  paint()
-   These methods both take as a parameter a reference variable of type  Graphics  -- which is an abstract class. The object will be a subtype that handles the drawing context for the given platform
-   For Swing components, it is usually sufficient to just define  paintComponent()  for drawing aspects, unless you want to control the other parts (border, children) as well

So, what can we DO in the paint() or paintComponent() methods? Pretty much anything that's available in the Graphics class, and then some.  

----------

### class  Graphics  and other useful helper classes

-   [Graphics](http://java.sun.com/javase/6/docs/api/java/awt/Graphics.html)  - helps manage drawing on the screen for GUI applications and applets.
    
    -   Keeps track of state information like current font, current color, the Component object being drawn on, and more
    -   Has methods for drawing various kinds of shapes (lines, ovals, polygons, rectangles, etc) as well as strings.
    -   Also has methods for setting the font, the color, the current clipping area, the paint mode, and other status information
    
      
    
-   [Color](http://java.sun.com/javase/6/docs/api/java/awt/Color.html)  - used for specifying colors in components and drawings
    
    -   colors stored and specified with RGB (Red Green Blue) values
    -   RGB values can be specified with ints (0-255) or floats (0.0-1.0)
    -   Color constants exist for common colors (Color.BLUE,  Color.GREEN, etc)
    -   To set or find out the current drawing color, use the  Graphics  methods  getColor()  and  setColor(). Example:
        
          g.setColor(Color.MAGENTA);
          g.setColor(new Color(255, 128, 3));	// using RGB values 
        
    -   [JColorChooser](http://java.sun.com/javase/6/docs/api/javax/swing/JColorChooser.html)  - a  javax.swing  component that enables application users to choose colors
    
      
    
-   [Font](http://java.sun.com/javase/6/docs/api/java/awt/Font.html)  - specify fonts used in Graphics drawings
    
    -   _Physical_  fonts are actual fonts on a system -- these depend on platform and what fonts are installed on a system
    -   _Logical_  fonts are the 5 font families supported in Java: Serif, Sans Serif, Monospaced, Dialog, and DialogInput. When using logical fonts, an appropriate font on the given system will be chosen
    -   Font constructor takes three parameters: font name, font style, font size
        -   Font name can be physical or logical
        -   Font styles are plain, italics, or bold
        -   Font size measured in  _points_
    -   To set or find out the current drawing font, use the  Graphics  methods  getFont()  and  setFont(). Example:
        
          Font f = g.getFont();			// retrieve current font
          g.setFont(new Font("Serif", Font.ITALICS, 12)); 
        
    -   Other methods available in class  Font  to set or retrieve properties for a Font object
    
      
    
-   [FontMetrics](http://java.sun.com/javase/6/docs/api/java/awt/FontMetrics.html)  - abstract class. Encapsulates information and properties about the rendering of a font on screen
    -   Helps track more specific font information like height, descent, ascent, and leading (interline spacing)
    -   Graphics  class has a couple of methods named  getFontMetrics():
        
           FontMetrics m1, m2;
           m1 = g.getFontMetrics();	// retrieve info about current drawing font 
           m2 = g.getFontMetrics(f1);	// retrieve info about font f1
         
        
-   [Polygon](http://java.sun.com/javase/6/docs/api/java/awt/Polygon.html)  - helper class for representing information about Polygons
    
    -   Stores a list of (x,y) coordinate pairs, representing vertices of a polygon
    -   Several Graphics class methods are for drawing polygons -  drawPolygon(),  drawPolyLine,  fillPolygon. There are versions of these last two that take a Polygon object as a parameter.
    
      
    

----------

## Java2D

The Java2D API provides advanced graphics capabilities, for more detailed and complex two-dimensional drawing.

[Java 2D API](http://java.sun.com/products/java-media/2D/index.html)  -- for an overview, see this page on the Java web site.

[A Java-2D Tutorial](http://java.sun.com/docs/books/tutorial/2d/index.html)

-   Allows more complex drawing, like lines of varying thickness, filling shapes with colors and patterns, drawing dashed lines, composite overlapping text and graphics, gradients and textures, and more
-   Involves a variety of packages:
    -   java.awt
    -   java.awt.image
    -   java.awt.color
    -   java.awt.font
    -   java.awt.geom
    -   java.awt.print
    -   java.awt.image.renderable
-   Need to use an instance of class  [Graphics2D](http://java.sun.com/javase/6/docs/api/java/awt/Graphics2D.html), which is a subclass of class Graphics. Must cast the Graphics object in the  paintComponent()  method into a Graphics2D reference when using:
    
      Graphics2D g2d = (Graphics2D) g;
    

See the last two chapter 12 examples -- these illustrate some sample uses of Graphics2D methods draw() and fill(), along with some of the Java2D shape types and drawing options.

----------

### [Deitel examples](http://www.cs.fsu.edu/~myers/cop3252/notes/deitel7/ch12)

```java
// Bouncing Ball example

import java.awt.event.*;
import java.awt.Graphics;
import java.awt.Color;
import javax.swing.JPanel;
import javax.swing.JFrame;
import javax.swing.Timer;

public class Ball
{
   // execute application
   public static void main( String args[] )
   {
      JFrame frame = new JFrame( "Bouncing Ball" );
      frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );

      BallPanel bp = new BallPanel(); 
      frame.add( bp );
      frame.setSize( 300, 300 ); // set frame size
      frame.setVisible( true ); // display frame
   } // end main
}


// class BallPanel

class BallPanel extends JPanel implements ActionListener
{
   private int delay = 10;
   protected Timer timer;

   private int x = 0;		// x position
   private int y = 0;		// y position
   private int radius = 15;	// ball radius

   private int dx = 2;		// increment amount (x coord)
   private int dy = 2;		// increment amount (y coord)

   public BallPanel()
   {
      timer = new Timer(delay, this);
	timer.start();		// start the timer
   }

   public void actionPerformed(ActionEvent e)
   // will run when the timer fires
   {
	repaint();
   }

   // draw rectangles and arcs
   public void paintComponent( Graphics g )
   {
      super.paintComponent( g ); // call superclass's paintComponent 
	g.setColor(Color.red);

	// check for boundaries
	if (x < radius)			dx = Math.abs(dx);
	if (x > getWidth() - radius)	dx = -Math.abs(dx);
	if (y < radius)			dy = Math.abs(dy);
	if (y > getHeight() - radius)	dy = -Math.abs(dy);

	// adjust ball position
	x += dx;
	y += dy;
	g.fillOval(x - radius, y - radius, radius*2, radius*2);
   }

}
```
