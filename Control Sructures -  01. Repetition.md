# Control Sructures - Repetition

## Repetition Statements

-   Repetition statements are called  _loops_, and are used to repeat the same code mulitple times in succession.
-   The number of repetitions is based on criteria defined in the loop structure, usually a true/false expression
-   The three loop structures in Java are:
    -   **while**  loops
    -   **do-while**  loops
    -   **for**  loops
-   Three types of loops are not actually needed, but having the different forms is convenient

  

## while  and  do-while  loops

-   Format of  while  loop:

```java
**while (_boolean_expression_)
{
statement(s)
}** 

-   Format of  do/while  loop:

**do
{
statement(s)
}
while (_boolean_expression_);** 
```

-   The  _boolean_expression_  in these formats is sometimes known as the  **loop continuation condition**
-   The loop body must be a block, or a single statement (like with the  if-statements)
-   We could also write the formats as follows (illustrating more visually what they look like when a compound statement makes up the loop "body"):

// while loop format

```java
while (_boolean_expression_) 
{
statement1;
statement2;
// ...

statementN;
} 
```

// do-while loop format

```java
do
{
statement1;
statement2;
// ...

statementN;
} while (_boolean_expression_);
```

-   **HOW THEY WORK**
    -   The boolean expression is a test condition that is evaluated to decide whether the loop should repeat or not.
        -   **true**  means run the loop body again.
        -   **false**  means quit.
    -   The  while  and  do/while  loops both follow the same basic flowchart -- the only exception is that:
        -   In a  while  loop, the test expression is checked first
        -   In a  do/while  loop, the loop "body" is executed first

----------

### Examples

Both of the following loops add up all of the numbers between 1 and 50.

 // **while loop example** 
 // loop body runs 50 times, condition checked 51 times 

```java
 int i = 1, sum = 0; 
 while (i <= 50) 
 { 
    sum += i;		// means:  sum = sum + i; 
    i++; 		// means:  i = i + 1;
 } 
```

 System.out.println("Sum of numbers from 1 through 50 is " + sum); 
  

 // **do/while loop example** 
 // loop body runs 50 times, condition checked 50 times 

```java
 int i = 1, sum = 0; 
 do 
 { 
    sum += i;		// means:  sum = sum + i; 
    i++; 		// means:  i = i + 1;
 } while (i <= 50); 
```

 System.out.println("Sum of numbers from 1 through 50 is " + sum); 

#### Example Links

-   [A simple while-loop example (controlled by counting)](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Insecure1.java)
-   [Same example, but the while-loop counts backwards](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Insecure2.java)
-   [Another simple while-loop example, this one not controlled by counting](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Insult1.java)
-   [Similar example, but with a do/while loop (and slightly different control condition).](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Insult2.java)

----------

## The  for  loop

-   The  **for**  loop is most convenient with  _counting loops_  -- i.e. loops that are based on a counting variable, usually a known number of iterations
-   Format of  for  loop:

```java
**for (_initialCondition_; _boolean_Expression_; _iterativeStatement_) 
{   
statement(s)
}** 
```

-   As usual, the loop body is a block of statements, or if just a single statement, the block can be omitted. An alternate way to write the format might be:

**for (_initialCondition_; _boolean_Expression_; _iterativeStatement_) 
{
statement1;
statement2;
// ...

statementN;
}** 

-   How it works
    -   The  _initialCondition_  runs once, at the start of the loop
    -   The  _boolean_Expression_  is checked. (This is just like the expression in a  while  loop). If it's false, quit. If it's true, then:
        -   Run the loop body
        -   Run the  _iterativeStatement_
        -   Go back to the  _boolean_Expression_  step and repeat

----------

### Examples of  for  loops

-   Recall this  while  loop example, which adds the numbers from 1 to 50:
    
     int i = 1, sum = 0; 
     while (i <= 50) 
     { 
        sum += i; 
        i++; 
     } 
    
     System.out.println("Sum of numbers from 1 through 50 is " + sum); 
    
    Here's a  for  loop that does the same job:
    
     // **for loop example** 
     // loop body runs 50 times, condition checked 51 times 
     int i, sum = 0; 
     for (i = 1; i <= 50; i++) 
     { 
        sum += i; 
     } 
    
     System.out.println("Sum of numbers from 1 through 50 is " + sum); 
    
-   This loop prints out the word "Hello" 10 times:
    
      for (int i = 0; i < 10; i++)
        System.out.println("Hello");
    
    So does this one
    
      for (int i = 1; i <= 10; i++)
        System.out.println("Hello");
    
-   A few common types of algorithms using for-loops:
    -   [A counting algorithm](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/for/Counting.java)
    -   [A summing algorithm](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/for/Summing.java)  -- Adding up something with a loop
    -   [A product algorithm](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/for/Product.java)  -- Multiplying things with a loop
-   Examples using nested loops:
    -   [Simple nested loop example](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/for/Nested.java)
    -   [Prints out a rectangle](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/for/Rect.java)
    -   [Prints out a triangle](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/for/Triangle.java)

----------

### Special notes about for loops:

1.  It should be noted that if the control variable is declared inside the for header, it only has scope through the for loop's execution. Once the loop is finished, the variable is out of scope:
    
        for (int counter = 0; counter < 10; counter++) 
        {
           // loop body    
        } 
    
        System.out.println(counter);   // illegal.  counter out of scope
    
    This can be avoided by declaring the control variable before the loop itself.
    
        int counter;    // declaration of control variable 
    
        for (counter = 0; counter < 10; counter++) 
        {
           // loop body    
        } 
    
        System.out.println(counter);   // OK.  counter is in scope
    
2.  For loops also do not have to count one-by-one, or even upward. Examples:
    
        for (i = 100; i > 0; i--)
    
        for (c = 3; c <= 30; c+=4)
    
    The first example gives a loop header that starts counting at 100 and decrements its control variable, counting down to 1 (and quitting when i reaches 0). The second example shows a loop that begins counting at 3 and counts by 4's (the second value of c will be 7, etc).

----------

## Special statements:  break  and  continue

-   These statements can be used to alter the flow of control in loops, although they are not specifically  _needed_. (Any loop can be made to exit by writing an appropriate  _test expression_).
-   **break**: This causes immediate exit from any loop (as well as from  switch  blocks)
    -   [An example of break](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Break.java)
-   **continue**: When used in a loop, this statement causes the current loop iteration to end, but the loop then moves on to the next step.
    -   In a  while  or  do-while  loop, the rest of the loop body is skipped, and execution moves on to the  _test condition_
    -   In a  for  loop, the rest of the loop body is skipped, and execution moves on to the  _iterative statement_
    -   [An example of continue](https://www.cs.fsu.edu/~myers/cgs3416/notes/examples/control/Continue.java)