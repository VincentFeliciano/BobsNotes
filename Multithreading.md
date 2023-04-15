## Multithreading

### Background Concepts

-   **Processor**: the part of the machine that executes instructions (CPU)
    -   Some computers today have multiple processors
-   **Process**: a program running on a processor in its own address space
-   **Multitasking**: the ability to run multiple programs at the same time (on the same machine), even a machine with one processor.
    -   **Concurrency**  is a general term for the idea of performing multiple operations in parallel
-   **Preemptive Multitasking**: Most common form of process scheduling in multi-user systems today
    -   The processor is shared between running processes
    -   A scheduler gives one process a "turn" (or a "time slice"), then switches to another (even though the first hasn't finished), and so on
    -   This gives the illusion that processes are running simultaneously.
    -   The only way for processes to  **truly**  run simultaneously is on a multi-processor system
-   **Context switch**: the activity of saving the state of a running process (so it can be restored later), and then restoring the context of another process
    -   Somewhat expensive in computing resources

### Concurrency within a program

-   **Threads**  are used to allow concurrent operations within a single program (process)
    -   This is similar to the notion of multiple processes running on a machine. Multiple threads can run within a single program
    -   As with processes, only one thread can use the processor at a time
    -   But parallel tasks can still be simulated. A lengthy task doesn't have to finish before another starts
    -   A multi-processor machine can actually run multiple threads simultaneously, increasing performance
-   Of course, multiple tasks  _could_  still be done with separate processes, but threads have some advantages:
    -   Context switch between threads fast and inexpensive
    -   Threads run within the same process, so they share the same address space
    -   Easy access to shared data
    -   When one thread is blocked, another can still proceed
    -   Natural decomposition of work (one thread for one task)
-   Examples of thread use:
    -   Java provides a  _garbage collector thread_  for cleaning up dynamically allocated memory. This runs as a seperate thread so that it can do its job without halting the rest of the program
    -   A media player, which downloads and plays back a video clip. One thread to download, one thread to play, and they can do their jobs simultaneously
-   class  [Thread](http://java.sun.com/javase/6/docs/api/java/lang/Thread.html)  implements the  [Runnable](http://java.sun.com/javase/6/docs/api/java/lang/Runnable.html)  interface and overrides its  run()  method. The two common ways of obtaining a thread are:
    -   extend the  Thread  class and override the  run()  method
    -   create a class that implements  Runnable

### Thread States

-   **new**  - thread has been created, but not started by the program
-   **runnable**  - thread has been started, and is considered to be executing its task
    -   Within the runnable state, the operating system manages threads and puts them in a  **ready**  state or a  **running**  state at the OS level
-   **waiting**  - thread is stopped while waiting for another thread to perform a task
-   **timed waiting**  - sometimes called  _sleeping_. Thread can wait for an interval of time, or set a default time while waiting for another thread
-   **terminated**  (or dead) - thread has completed its task and is finished.

### Priorities

-   Every thread is given a priority from 1 to 10, with 10 being the highest
-   class  Thread  has three pre-defined constants:
    -   MIN_PRIORITY  = 1
    -   NORM_PRIORITY  = 5
    -   MAX_PRIORITY  = 10
-   Typically, higher priority threads are more important to a program, and they have a better chance of running sooner
-   The operating system's thread scheduler will determine exactly when threads run -- may vary between platforms (different OSes)

### Creating Threads

-   Threads can be created by extending class  Thread  and overriding the  run()  method
    -   This has been a common technique, especially in older versions of Java
-   **Preferred**  in J2SE version 1.5.0 and later:
    -   Create classes that implement the  Runnable  interface (which means overriding the  run()  method)
    -   Use built-in features from the package  [java.util.concurrent](http://java.sun.com/javase/6/docs/api/java/util/concurrent/package-summary.html)  to create the Threads that execute the Runnables
    -   This helps hide complexity from the programmer and makes multithreading less error-prone
    -   This way, the programmer doesn't usually have to worry about setting and adjusting priorities
-   **java.util.concurrent**
    -   Runnables are executed by an object that implements the  Executor  interface (has method  execute())
    -   **thread pool**  - a group of threads managed by an Executor object
    -   The Executor assigns a Runnable to an available thread, or it can make the Runnable wait for a thread to become available

### Synchronization

**Thread Synchronization** is the coordination of access to shared data by multiple concurrent threads. Typically handled with _locks_, to implement _mutual exclusion_ when threads are sharing resources.

-   **Mutual exclusion**  - allowing only one thread at a time to access and/or modify a shared object
-   **locks**  are used to handle this.
    -   interface  Lock  is in package  java.util.concurrent.locks
    -   method  lock()  called to obtain a lock, and method  unlock()  releases it
    -   Only one thread may have the lock on a resource at a time. Other threads that need it are placed in a  _waiting_  state for the lock
    -   locks  _can_  be set to use a  **fairness policy**  -- longest waiting thread will acquire the lock. This can avoid indefinite postponement, but reduces processing efficiency.
-   When a thread owning a lock needs to wait on some condition to continue (it needs a resource from another thread, for example)...
    -   Keeping the lock (and hanging out doing nothing) wouldn't be efficient for other threads
    -   Can wait on a  _condition variable_  (created by calling Lock method  newCondition(), which returns an object that implements interface  Condition).
    -   To wait on the condition, thread calls Condition's  await()  method
    -   This automatically releases the lock and puts the thread into a  _waiting_  state
    -   When another thread determines that the condition has been satisfied, it sends a  **signal**  to the waiting thread, which can return to a  _runnable_  state (and try to regain the lock)
-   **Deadlock**  -- a common error that can occur. Example:  
    Thread A has resource X and needs resource Y.  
    Thread B has resource Y and needs resource X.  
    Both are  _waiting_, and neither can continue until the other releases a needed resource
    -   To avoid deadlock, make sure that some other thread will call  signal()  to wake up any waiting threads.
    -   One possible safeguard is to have a seperate thread (not involved in the possible deadlock) call  signalAll()  to "wake up" all waiting threads
-   NOTE: Only a thread that  **has**  the lock on a condition variable can call  await(),  signal(), or  signalAll()  for it. (If a thread without the lock tries it, an exception is thrown).

class ArrayBlockingQueue -- nice pre-packaged implementation of a circular buffer (as a shared resource) for use with producer/consumer relationships (like client/server applications, for example).

----------

### [Deitel Examples](https://www.cs.fsu.edu/~myers/cop3252/notes/deitel7/ch23/)