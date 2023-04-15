

### Graphics classes

-   In the original version of Java, graphics components were in the AWT library (Abstract Windows Toolkit)
    
    -   Was okay for developing simple GUI applications
    -   For different platforms, AWT components mapped to platform-specific components
    -   Prone to platform specific bugs
    -   Primary package:  [java.awt](http://docs.oracle.com/javase/8/docs/api/java/awt/package-summary.html). See other awt package APIs on the java.sun site
    
      
    
-   When Java 1.2 was released, a set of libraries known as the  **Swing components**  were introduced (originally as extension libraries, then as part of the Standard Edition) with the idea of replacing the older AWT user-interface components (like  Button,  TextField,  TextArea, etc).
    
    -   less dependent on target platform
    -   a more robust and flexible library
    -   Primary package:  [javax.swing](http://docs.oracle.com/javase/8/docs/api/javax/swing/package-summary.html). See other swing package APIs on the java.sun site
    
      
    
-   Java was trying to move away from Swing library updates, focusing rather on a newer API for GUI-building known as JavaFX. (Oracle has since backtracked on this)
    
    -   JavaFX's API includes GUI, graphics, and multimedia (images, animation, audio, video)
    -   Layouts and components are handled with a special form of XML (Extended Markup Language) -- known as FXML -- as opposed to objects in Java code
    -   While FXML tags can get complicated, the usual technique is to use the JavaFX Scene Builder application, which contains design tools for dragging and dropping components onto a layout, then letting it write the FXML for you. (This is similar to the idea of a WYSIWYG editor for generating HTML pages).
    -   There are classes to help embed Swing capabilities into JavaFX apps, as well as vice versa
    -   Note that in Java 1.8, JavaFX is not listed in the standard edition (version 8) API -- it is a separate set of extension libraries. In Java version 9, JavaFX was included in the Standard Edition API, but it was removed from the Standard Development Kit around Java version 11.
    -   Currently (based on last update I read on their version releases), both Swing libraries and JavaFX extension packages are being supported currently as options. JavaFX is back to being an extension library only.
    
      
    
-   In this course, we will learn the core Swing library setup
    -   Swing libraries contains code and library patterns that you will likely find in other GUI library setups in other languages

### Primary GUI Concepts

The main factors that make up a Graphic User Interface in a program are:

-   Components and Containers
-   The layout of components on the screen (e.g. in a container, etc)
-   Event handling

The components are often pre-built items like buttons, text areas, slider bars, and the like. Some types of components are containers, meaning they can serve as ways to group other components together. Some components can act as canvases for general images, shapes, or other drawing.

Layout refers to how components are rendered on screen, relative to each other (position and size, etc).

Event handling refers to setting up actions that can trigger functionality -- examples: button clicks, selecting from a menu, pressing a key on the keyboard, timer expiring, etc.

----------

### Java Swing Graphics API

-   [Component](http://docs.oracle.com/javase/8/docs/api/java/awt/Component.html): A base class for all non-menu graphic user interface classes
-   [Container](http://docs.oracle.com/javase/8/docs/api/java/awt/Container.html): a base class for container classes. A container is used to group smaller components. The most important containers are:
    -   [JApplet](http://docs.oracle.com/javase/8/docs/api/javax/swing/JApplet.html)  - for holding Applets
    -   [JFrame](http://docs.oracle.com/javase/8/docs/api/javax/swing/JFrame.html)  - for holding GUI components in applications. A window that is on the outer level (not inside another window)
    -   [JPanel](http://docs.oracle.com/javase/8/docs/api/javax/swing/JPanel.html)  - invisible container holding user-interface components. Can be nested, and can be used as canvases for drawing graphics
    -   [JDialog](http://docs.oracle.com/javase/8/docs/api/javax/swing/JDialog.html)  - for creating dialog boxes (usually temporary popup messages or dialogs for receiving additional info
-   [JComponent](http://docs.oracle.com/javase/8/docs/api/javax/swing/JComponent.html): Base class for all of the lightweight Swing components, which are graphical items places on the canvases or containers. Its subclasses are the basic elements for constructing GUIs. Here are just a few of the more common elements (for the full list, see the Java API for the  javax.swing  package):
    -   [JButton](http://docs.oracle.com/javase/8/docs/api/javax/swing/JButton.html)  - for creating push buttons
    -   [JCheckBox](http://docs.oracle.com/javase/8/docs/api/javax/swing/JCheckBox.html)  - for creating toggle checkboxes
    -   [JMenu](http://docs.oracle.com/javase/8/docs/api/javax/swing/JMenu.html)  - for pop-up menus
    -   [JRadioButton](http://docs.oracle.com/javase/8/docs/api/javax/swing/JRadioButton.html)  - for radio buttons (made into a group, only one can be selected)
    -   [JLabel](http://docs.oracle.com/javase/8/docs/api/javax/swing/JLabel.html)  - a display area for a short string or image
    -   [JList](http://docs.oracle.com/javase/8/docs/api/javax/swing/JList.html)  - a component allowing the user to select from a list
    -   [JOptionPane](http://docs.oracle.com/javase/8/docs/api/javax/swing/JOptionPane.html)  - a component allowing the user to pop up an easy dialog box as an information message or for user input
    -   [JTextField](http://docs.oracle.com/javase/8/docs/api/javax/swing/JTextField.html)  - component allowing an editable line of text
    -   [JTextArea](http://docs.oracle.com/javase/8/docs/api/javax/swing/JTextArea.html)  - multi-line area for displaying text
    -   [JScrollPane](http://docs.oracle.com/javase/8/docs/api/javax/swing/JScrollPane.html)  - gives a scrollable view of a lightweight component
-   Helper classes - used by components and containers to control drawing and placing of objects. Some important helper classes (from package  java.awt):
    -   [Graphics](http://docs.oracle.com/javase/8/docs/api/java/awt/Graphics.html)  - abstract class. Provides graphical context for drawing
    -   [Color](http://docs.oracle.com/javase/8/docs/api/java/awt/Color.html)  - used for specifying colors in components and drawings
    -   [Font](http://docs.oracle.com/javase/8/docs/api/java/awt/Font.html)  - specify fonts used in Graphics drawings
    -   [FontMetrics](http://docs.oracle.com/javase/8/docs/api/java/awt/FontMetrics.html)  - abstract class. Encapsulates information and properties about the rendering of a font on screen
    -   [Dimension](http://docs.oracle.com/javase/8/docs/api/java/awt/Dimension.html)  - encapsulates width and height of a component in an object

### Event Handling

-   _Event_: A signal that something has happened in a program. Examples: Button clicks, mouse movements, menu selections
-   GUI programs generally driven by events, rather than a specific procedural order
-   Events are handled with event objects. These are triggered by actions on source objects (components or objects on which the event is generated), and they must implement corresponding event listener interfaces. The listener listens for the event, and invokes an event handler when event occurs
-   [java.util.EventObject](http://docs.oracle.com/javase/8/docs/api/java/util/EventObject.html): Base class for event classes in Java

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
