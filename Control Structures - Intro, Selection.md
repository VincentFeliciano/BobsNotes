

## Flow of Control:

Flow of control through any given function is implemented with three basic types of control structures:

-   **Sequential**: default mode. Sequential execution of code statements (one line after another) -- like following a recipe
-   **Selection**: used for decisions, branching -- choosing between 2 or more alternative paths. In Java, these are the types of selection statements:
    -   if
    -   if/else
    -   switch
-   **Repetition**: used for looping, i.e. repeating a piece of code multiple times in a row. In Java, there are three types of loops:
    -   while
    -   do/while
    -   for

The  _function_  construct, itself, forms another way to affect flow of control through a whole program. This will be discussed later in the course.

#### Some useful tools for building programs or program segments

-   pseudocode - helps "think" out a problem or algorithm before trying to code it
-   flowcharting - graphical way to formulate an algorithm or a program's flow
-   stepwise refinement (top-down design) of algorithms

  

## True and False

-   Selection and repetition statements typically involve decision steps. These steps rely on conditions that are evaluated as either  **true**  or  **false**
-   Recall that Java has a type called  boolean, which can take two possible values,  true  and  false
-   Most functions that answer a yes/no question (or a true/false situation) will return a boolean answer
-   An expression that evaluates to a true/false value is called a  _Boolean expression_

  

## Logical Operators:

The comparison operators in Java work much like the symbols we use in mathematics. Each of these operators returns a Boolean value: a **true** or a **false**.

  x == y        // x is equal to y
  x != y        // x is not equal to y
  x < y         // x is less than y
  x <= y        // x is less than or equal to y
  x > y         // x is greater than y
  x >= y        // x is greater than or equal to y

We also have Boolean operators for combining expressions. Again, these operators return  **true**  or  **false**

  !x            // the NOT operator (negation) -- true if x is false
  x && y        // the AND operator -- true if both x and y are true
  x || y        // the OR operator -- true if either x or y (or both) are true
  x ^ y         // the **exclusive or** operator -- true if exactly one operand is true and one is false

These operators will be commonly used as test expressions in selection statements or repetition statements (loops).  

### Examples of expressions

  (x > 0 && y > 0 && z > 0)     // all three of (x, y, z) are positive
  (x < 0 || y < 0 || z < 0)     // at least one of the three variables is negative

  ( numStudents >= 20 && !(classAvg < 70))
        // there are at least 20 students and the class average is at least 70
  
  ( numStudents >= 20 && classAvg >= 70)
        // means the same thing as the previous expression

### Short Circuit Evaluation:

-   The  &&  and  ||  operators also have a feature known as  **short-circuit evaluation**.
-   In the Boolean AND expression  (X && Y), if  X  is false, there is no need to evaluate  Y  (so the evaluation stops). Example:
    
      (d != 0 &&  n / d > 0)
      
      // notice that the short circuit is crucial in this one.  If d is 0,
      //  then evaluating (n / d)  would result in division by 0 (illegal). But
      //  the "short-circuit" prevents it in this case.  If d is 0, the first
      //  operand (d != 0) is false.  So the whole && is false.
    
-   Similarly, for the Boolean OR operation  (X || Y), if the first part is true, the whole thing is true, so there is no need to continue the evaluation. The computer only evaluates as much of the expression as it needs. This can allow the programmer to write faster executing code.

----------

## Selection Statements

----------

## The  if/else  Selection Statement

-   The most common selection statement is the  **if**  statement. Basic syntax:
    
       if (_boolean expression_)
       {
          statement(s)
       }
    
-   The  if  statement can also have an  else  clause. This is sometimes known as an  if/else  statement. Basic syntax:
    
       if (_boolean expression_)
       {
          statement(s)
       }
       else
       {  
          statement(s)
       }
    
-   Note: In both of these formats, the set braces can be left out if the "body" of the  if  or the  else  is a single statement. Otherwise, the block is needed.
-   Note also that the condition is always a boolean expression. This means that it  _must_  be an expression that evaluates to a  **true**  or a  **false**
-   Appropriate indentation of the bodies of the if-clause and else-clause is a very good idea (for human readability), but irrelevant to the compiler

  

### Examples

  

----------

  if (grade >= 68)
    System.out.print("Passing");

// Notice that there is no else clause. If the grade is below 68, we move on.

----------

 
  if (x == 0)
    System.out.println("Nothing here");
  else
    System.out.println("There is a value");

// This example contains an else clause. The bodies are single statements.

----------

  if (y != 4)
  {
    System.out.println("Wrong number");
    y = y * 2;
    counter++;
  }   
  else
  {
    System.out.println("That\'s it!");
    success = true;
  }   

Multiple statements are to be executed as a result of the condition being true or false. In this case, note that the blocks are needed.

----------

  
Be careful with **if**s and **else**s. Here's an example of an easy mistake to make. If you don't use { }, you may think that you've included more under an **if** condition than you really have.

// What output will it produce if val = 2? Does the "too bad" statement really go with the "else" here?

  if (val < 5)
    System.out.println("True");
  else
    System.out.println("False");
    System.out.println("Too bad!");

* Indentation is only for people! It improves readability, but means nothing to the compiler.

#### Example links

-   [Miscellaneous if/else examples](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/misc.txt)
-   [Example program: Figuring a letter grade](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Grades1.java)
-   [Example program: Computing overtime pay](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Overtime.java)

#### Some common errors

What's wrong with these if-statements? Which ones are syntax errors and which ones are logic errors?

-   if (x == 1 || 2 || 3)
       System.out.print("x is a number in the range 1-3");
    
-   if (x > 5) && (y < 10)
      System.out.print("Yahoo!");
    
-   if (response != 'Y' || response != 'N')
       System.out.print("You must type Y or N (for yes or no)");
    

----------

## The  switch  statement

-   A  **switch**  statement is often  _convenient_  for occasions in which there are multiple cases to choose from. The syntax format is:
    
    switch (_expression_)
    { 
        case _constant_: 
            statements 
        case _constant_: 
            statements 
    
        ...  (as many case labels as needed) 
    
        default:            // optional label 
            statements 
    } 
    
-   The switch statement evaluates the  _expression_, and then compares it to the values in the case labels. If it finds a match, execution of code jumps to that case label.
-   The values in case labels must be  _constants_, and may only be types  char,  byte,  short, or  int.
    -   This also means the case label must be a  _literal_  or a variable declared to be constant (with  final)
    -   **Note:**  You may  _not_  have case labels with regular variables, strings, floating point literals, operations, or function calls
-   If you want to execute code only in the case that you jump to, end the case with a  break  statement, otherwise execution of code will "fall through" to the next case
-   **Examples**:
    -   [Recall this example](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/switch/Ifelse1.java)  -- an if/else structure to determine a letter grade
    -   [Switch Example 1](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/switch/Switch1.java)  -- An attempt to convert the letter grade example into a switch. Syntactically correct, but has a logic flaw. What is it?
    -   [Switch Example 2](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/switch/Switch2.java)  -- corrected version of Example 1

  

----------

## The Conditional Operator

There is a special operator known as the **conditional operator** that can be used to create short expressions that work like if/else statements.

-   **Format:**
    
      _boolean_expression_ ? _true_expression_ : _false_expression_
    
-   **How it works:**
    -   The  _boolean_expression_  is evaluated for true/false value. This is like the test expression of an if-statement
    -   If the expression is true, the operator returns the  _true_expression_  value
    -   If the test expression is false, the operator returns the  _false_expression_  value
-   Note that this operator takes  **three**  operands. It is the one  _ternary_  operator in the Java language
-   **Example 1:**
    
      System.out.print( (x > y) ? "x is greater than y" : "x is less than or equal to y");
    
      // Note that this expression gives the same result as the following
      if (x > y)
         System.out.print("x is greater than y");
      else
         System.out.print("x is less than or equal to y");
    
-   **Example 2:**
    
      (x < 0 ? value = 10 : value = 20);
    
      // this gives the same result as:
      value = (x < 0 ? 10 : 20);
    
      // and also gives the same result as:
      if (x < 0)
         value = 10;
      else
         value = 20;ackedit.io/).