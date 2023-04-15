## I/O Foundations and Classes

### Streams

-   In Java, I/O handled with streams.
-   Think of a  _stream_  as a sequence of data flowing from one place to another (useful to think of as a buffer of data going one way or the other).
    -   An input stream flows from an input source (e.g. keyboard, file) into a program, usually to be stored in variables
    -   An output stream flows from a program to an output destination (e.g. screen, file, network socket)
-   Three stream objects already associated with devices in Java:
    -   System.in  -- standard input stream object
    -   System.out  -- standard output stream object
    -   System.err  -- standard error stream object
-   I/O libraries are in the package  [java.io](http://docs.oracle.com/javase/8/docs/api/java/io/package-summary.html)
    -   [Package Tree](http://docs.oracle.com/javase/8/docs/api/java/io/package-tree.html)  -- You can see the hierarchy of  java.io  classes here
-   Many built-in stream classes in Java, for processing different types of data. Two primary categories:  _byte streams_  and  _character streams_.
    -   [InputStream](http://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html)  is the base class for byte stream input classes
    -   [OutputStream](http://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html)  is the base class for byte stream output classes
    -   [Reader](http://docs.oracle.com/javase/8/docs/api/java/io/Reader.html)  is the base class for character stream input classes
    -   [Writer](http://docs.oracle.com/javase/8/docs/api/java/io/Writer.html)  is the base class for character stream output classes

### Reading and Writing with Files

-   [File](http://docs.oracle.com/javase/8/docs/api/java/io/File.html)  is a class used for retrieving properties of files or directories on a disk.
    -   Objects of class  File  do  **not**  open files or provide file processing features.
-   Text files are typically created with character-based streams. Binary files are typically created with byte streams.
-   **Sequential File**: no regular record structure, typically read or written as an entire file
-   **Random Access File**: structured as uniformly-sized records. Can read/write either sequentially or by accessing single records anywhere in the file.
-   Basic File I/O classes.
    -   [FileInputStream](http://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)  - for byte streams
    -   [FileOutputStream](http://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)  - for byte streams
    -   [FileReader](http://docs.oracle.com/javase/8/docs/api/java/io/FileReader.html)  - for character streams
    -   [FileWriter](http://docs.oracle.com/javase/8/docs/api/java/io/FileWriter.html)  - for character streams
-   For the input streams, the primary method is called  read. There is a version that reads one byte (or char), and a version that reads an array of bytes (or chars).
-   For the output streams, the primary methods are called  write. For writing single bytes (or chars) and for arrays of byte (or chars).
-   [JFileChooser](http://docs.oracle.com/javase/8/docs/api/javax/swing/JFileChooser.html)  -- a Swing component for popping up a dialog box for easy browsing and selection of a file on a local file system

**Example:**  [CopyFileUsingByteStream.java](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/text/ch17/CopyFileUsingByteStream.java)  -- older example, which uses the file stream classes to copy one file to another

### Buffered Streams

-   Buffered streams help increase efficiency. They use a buffered array of bytes or characters. The buffered stream classes are:
    -   [BufferedInputStream](http://docs.oracle.com/javase/8/docs/api/java/io/BufferedInputStream.html)  - for byte streams
    -   [BufferedOutputStream](http://docs.oracle.com/javase/8/docs/api/java/io/BufferedOutputStream.html)  - for byte streams
    -   [BufferedReader](http://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html)  - for character streams
    -   [BufferedWriter](http://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html)  - for character streams
-   Buffered streams are used to add functionality to other streams (i.e. the buffering). Usually constructed out of other stream objects
-   For example, to applied buffered streams to file i/o, we can create file streams, and then wrap them in a buffered stream object. Examples:
    
       BufferedReader infile1 = new BufferedReader(new FileReader(filename));
       BufferedOutputStream outfile1 = new BufferedOutputStream(new FileOutputStream(filename));
       Reader r1 = new BufferedReader(new FileReader("file1.txt"));
    
    Note that in the last declaration, the buffered reader object is attached to a  Reader  reference variable. This is legal since  Reader  is the base class for all reader classes

#### Examples

These examples work in earlier versions of Java. These use the BufferedReader and BufferedWriter classes.

-   [Test1.java](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/io/Test1.java)  -- This program reads an input file and writes an all-uppercase copy of it to an output file. First argument is the input file, second argument is the output file.
-   [Test2.java](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/io/Test2.java)  -- This program reads an input file and counts the number of times a word appears. First argument is the input file, second argument is the word to search for.
-   [Test3.java](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/io/Test3.java)  -- This program uses some classes from the  java.util  package in addition to a file reader, and it lists all the words in the input file along with the number of times each word appears. The one command-line argument is the input file.
-   [Frost.txt](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/io/Frost.txt)  -- here is a sample text file you can use to test each of these programs

### Newer Java capabilities (useful for File I/O)

With Java 1.5, a number of new classes were introduced that made I/O tasks a little easier.

-   [Formatter](http://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html)  class -- an interpreter for printf-style format strings. Can create a Formatter object already attached to a file
-   [Scanner](http://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html)  class -- a text scanner that parses simple tokens more easily. Can create a Scanner and pass in an input stream, or a File object

### Input and Output of Objects

-   **Serialization**  of objects: representing an object as a sequence of bytes, which includes:
    -   the object's data
    -   info about the object's type
    -   info about the types of data in the object
-   A serialized object can be written to a file as a single item, and then it can be read from a file and deserialized
-   This can be done with the classes:
    -   [ObjectOutputStream](http://docs.oracle.com/javase/8/docs/api/java/io/ObjectOutputStream.html)
    -   [ObjectInputStream](http://docs.oracle.com/javase/8/docs/api/java/io/ObjectInputStream.html)
-   An object can be serialized if its class implements the interface  **Serializable**
    -   Serializable  is a marker (or tagging) interface
    -   To write an object with class  ObjectOutputStream, it must be a  Serializable  object
    -   Each instance variable in the object must also be  Serializable  (or must be declared  transient, and will be left out of the serialization)
-   Can combine with File I/O streams. Example:
    
      ObjectOutputStream output;
      output = new ObjectOutputStream(new FileOutputStream("myfile.dat")); 
    

----------

### [Deitel Examples -- Chapter 14](https://www.cs.fsu.edu/~myers/cop3252/notes/deitel7/ch14/)

-- Some of these examples use Scanner, Formatter, newer features

### [Deitel ed. 5 Examples -- Chapter 17](http://www.cs.fsu.edu/~myers/cop3252/notes/deitel5/ch17/)

-- these examples do I/O without the newer Scanner and Formatter features