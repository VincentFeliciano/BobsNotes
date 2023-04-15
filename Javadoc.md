## Javadoc

Javadoc is a nice tool for building web page documentation for your classes. Resulting web pages look like the ones you see in the Java API pages on the Sun web site. Comments need to be in a specific format. Javadoc comments are contained in block comments with these opening and closing markers:

```java
  /**      */
```


Javadoc comments are written in html, and there are specific Javadoc tags to use for certain items (like method parameters and returns).

-   [JavaDoc guide on Oracle Java SE documentation page](https://docs.oracle.com/en/java/javase/17/javadoc/javadoc.html#GUID-7A344353-3BBF-45C4-8B28-15025DDCC643)
-   [javadoc tags](https://docs.oracle.com/en/java/javase/17/docs/specs/javadoc/doc-comment-spec.html)
-   [Rectangle.java](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/tools/Rectangle.java)  - a simple class that contains Javadoc comments
-   [Javadoc pages generated for Rectangle class](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/tools/rect1/), when the following command is run:
    
      javadoc Rectangle.java
    
-   [Javadoc pages generated for Rectangle class](https://www.cs.fsu.edu/~myers/cop3252/notes/examples/tools/rect2/index.html), when the following command is run:
    
      javadoc -link https://docs.oracle.com/javase/17/docs/api/ -link . -private 
              -linksource -author Rectangle.java 
    
    Note that this one uses some extra command line options:
    -   `-link`: specifies that pages will create links to outside classes, given in the location after the phrase  `-link`
    -   `-private`: shows all classes and members in documentation
    -   `-linksource`: creates html version of source code file, with line numbers, linked in to documentation
    -   `-author`: includes the text from the author label in the documentation
    -   There are many other command line options -- tckedit.io/).