
## 1. What is Java. What are features of Java?
Java is a high-level programming language and is platform-independent.
+ Java is also an object-oriented language. However, everything (except fundamental types) is an object in Java
+ Platform independent: A single program works on different platforms without any modification.
+ High Performance: JIT (Just In Time compiler) enables high performance in Java. 
JIT converts the bytecode into machine language and then JVM starts the execution.
+ Multi-threaded. We can write Java programs that deal with many tasks at once by defining multiple threads.
+ Java doesn't support multiple inheritance through class. It can be achieved by interfaces in java.
+ Secured: Java is secured because it doesn't use explicit pointers.
+ Java is a strong programming language as it uses strong memory management. The concepts like Automatic garbage collection.

## 2. What are the OOPs concepts?
OOPs concepts include:
+ **Inheritance** 
    + Inheritance means one class can extend to another class. 
    So that the codes can be reused from one class to another class. 
    The existing class is known as the Super class whereas the derived class is known as a sub class.
    Inheritance is only applicable to the public and protected members only. Private members can’t be inherited.
+ **Encapsulation**
    + Protects the code from others.
      Code maintainability.
      For encapsulation, we need to make all the instance variables private and create setter and getter for those variables. 
      Which in turn will force others to call the setters rather than access the data directly.
+ **Polymorphism**
    + A single object can refer to the super-class or sub-class depending on the reference type which is called polymorphism.
    Polymorphism is applicable for overriding
+ **Abstraction**
    + Abstraction in object-oriented programming means hiding complex internals but to expose only 
    essential characteristics and behavior with respect to context.
+ **Interface**
    + Multiple inheritances cannot be achieved in java. To overcome this problem the Interface concept is introduced.
   An interface is a template which has only method declarations and not the method implementation.

## 3. What are different access modifiers in Java?
+ **Default** access modifier is without any access specifier data members, class and methods, and are accessible within the same package.
+ **Private** access modifiers are marked with the keyword private, and are accessible only within class, and not even accessible by class from the same package.
+ **Protected** access modifiers can be accessible within the same package or subclasses from different packages.
+ **Public** access modifiers are accessible from everywhere.

## 4. What is the meaning of SOLID?
Solid represents five principles of java which are:

+ **S**: Single responsibility principle. One class should have only one and only responsibility.
+ **O**: Open-closed principle. Software components should be open for extension, but closed for modification. 
Hence, the browser is a perfect example of functionality that is open for extension but is closed for modification.
+ **L**: Liskov substitution principle. Types must be completely substitutable for their base types.
+ **I**: Interface segregation principle. 
Clients should not be forced to implement unnecessary methods which they will not use.
+ **D**: Dependency inversion principle. it depends on abstractions not on concretions. 
According to it, the high-level module must never rely on any low-level module.
You go to a local store to buy something, and you decide to pay for it by using your debit card. 
So, when you give your card to the clerk for making the payment, 
the clerk doesn’t bother to check what kind of card you have given.
The type of credit card or debit card that you have for paying does not even matter; they will simply swipe it.

## 5. What are primitive data types?

+ byte - 1 byte (8 bits). Min -2^7 Max 2^7-1
+ short - 2 byte (16 bits). Min -2^15 Max 2^15-1
+ char - 2 byte (16 bits). 2^16-1
+ int - 4 byte (32 bits). Min -2^31-1 Max 2^31
+ long - 8 byte (64 bits). Min -2^63-1 Max 2^63
+ float - 4 byte (32 bits). Min -2^31-1 Max 2^31
+ double - 8 byte (64 bits). Min -2^63-1 Max 2^63
+ boolean - NA usualy 1 byte

## 6. Order of execution of Initialization blocks and Constructors in Java.

+ Static initialization blocks will run whenever the class is loaded first time in JVM
+ Initialization blocks run in the same order in which they appear in the program.
+ Instance Initialization blocks are executed whenever the class is initialized and before constructors are invoked. 
They are typically placed above the constructors within braces.

## 7. Differences between Lambda Expressions and Closures in Java.
Java supports lambda expressions but not the Closures. 
A lambda expression is an anonymous function and can be defined as a parameter. 
The Closures are like code fragments or code blocks that can be used without being a method or a class. 
It means that Closures can access variables not defined in its parameter list and also assign it to a variable.

## 8. Give the list of Java Object class methods.

+ clone() - Creates and returns a copy of this object.
+ equals() - Indicates whether some other object is "equal to" this one.
+ finalize() - Called by the garbage collector on an object when garbage collection determines that there are 
no more references to the object.
+ getClass() - Returns the runtime class of an object.
+ hashCode() - Returns a hash code value for the object.
+ notify() - Wakes up a single thread that is waiting on this object's monitor.
+ notifyAll() - Wakes up all threads that are waiting on this object's monitor.
+ toString() - Returns a string representation of the object.
+ wait() - Causes current thread to wait until another thread invokes the notify() method 
or the notifyAll() method for this object.


## 9. What is the difference between atomic, volatile, synchronized?

It basically reads value from memory, increments it and puts back to memory. 
This works in single thread but nowadays, in the era of multi-core, multi-CPU, multi-level caches it won't work correctly. 
First of all it introduces race condition (several threads can read the value at the same time), 
but also visibility problems. The value might only be stored in "local" CPU memory (some cache) and not be visible 
for other CPUs/cores (and thus - threads).
**Volatile**
Declaring a variable as volatile means that modifying its value immediately affects the actual memory storage 
for the variable. The compiler cannot optimize away any references made to the variable. 
This guarantees that when one thread modifies the variable, all other threads see the new value immediately.

**AtomicInteger** 
```java
private AtomicInteger counter = new AtomicInteger();

public int getNextUniqueIndex() {
  return counter.getAndIncrement();
}
```
The AtomicInteger class uses CAS (compare-and-swap) low-level CPU operations (no synchronization needed!) 
Declaring an atomic variable guarantees that operations made on the variable occur in an atomic fashion, 
i.e., that all of the substeps of the operation are completed within the thread they are executed and 
are not interrupted by other threads.

**Synchronizing**
all accesses to a variable allows only a single thread at a time to access the variable, 
and forces all other threads to wait for that accessing thread to release its access to the variable.

Synchronization occurs on an object. This means that calling a synchronized method of a class will lock the this object of the call. Static synchronized methods will lock the Class object itself.

Likewise, entering a synchronized block requires locking the this object of the method.

Synchronized access to a variable is usually implemented using a monitor or semaphore. 
These are low-level mutex (mutual exclusion) mechanisms that allow a thread to acquire control 
of a variable or block of code exclusively, forcing all other threads to wait if they also attempt to acquire the same mutex.

This means that a synchronized method (or block) can be executing in multiple threads at the same time if they are 
locking on different objects, but only one thread can execute a synchronized method (or block) 
at a time for any given single object.


## 10. Explain object finalization

Called by the garbage collector on an object when garbage collection determines that 
there are no more references to the object. If an object can not be accessed from any live object, 
this means that it can be safely garbage collected.


## 11. What is Serialization in Java?

Object Serialization in Java is a process used to convert Object into a binary format which can be persisted into 
a disk or sent over the network to any other running Java virtual machine; 
the reverse process of creating object from the binary stream is called deserialization in Java. 
Java provides Serialization API for serializing and deserializing object which includes java.io.Serializable, 
java.io.Externalizable, ObjectInputStream and ObjectOutputStream etc. 

Serializable is marker interface.Marker interface in Java is interfaces with no field or methods or in 
simple word empty interface in java is called marker interface.

Making a class Serializable in Java is very easy, Your Java class just needs to implements java.io.Serializable 
interface and JVM will take care of serializing objects in the default format.

If you don't explicitly declare SerialVersionUID then JVM generates it based upon the structure of class 
which depends upon interfaces a class implements and several other factors which is subject to change

serialVersionUID is used to ensure that same class(That was used during Serialization) is loaded during 
Deserialization.serialVersionUID is used for version control of object.

You can customize Serialization process by defining writeObject and readObject method.

To avoid serialization some variable, you can mark that variable as either static or transient.

Externalizable interface has more control over serialization process and it is mandatory 
to override writeExternal and readExternal.


## 12. Concept Of Java Cloning

Java supports two type of cloning: - Deep and shallow cloning. By default shallow clone is used in Java. 
Object class has a method clone() which does shallow cloning. Shallow copies duplicate as little as possible. 
The memory usage is lower.
1) If the class has only primitive data type members then a completely new copy of the object will be created 
and the reference to the new object copy will be returned.
2) If the class contains members of any class type then only the object references to those members are copied 
and hence the member references in both the original object as well as the cloned object refer to the same object.

In deep copy is the copy of object itself. A new memory is allocated for the object and contents are copied.
When a deep copy of the object is done new references are created.
One solution is to simply implement your own custom method (e.g., deepCopy()) that returns 
a deep copy of an instance of one of your classes. 
Other common solution to the deep copy problem is to use Java Object Serialization.


## 13. StringBuffer vs StringBuilder

StringBuffer is synchronized, StringBuilder is not. 
StringBuilder is faster than StringBuffer because it's not synchronized.


## 14. Name some of the parsers which are commonly used to parse XML documents.

+ **Dom** Parser - Parses the document by loading the complete contents of the document and creating its complete 
hiearchical tree in memory. Using DOM parser, we can parse, modify or create a XML document.                           
+ **SAX** Parser - Parses the document on event based triggers. 
Does not load the complete document into the memory. You are processing a very large XML document 
whose DOM tree would consume too much memory. We have no random access to an XML document since it is processed 
in a forward-only manner. Using SAX parser, we can only parse or modify a XML document.
+ **StAX** Parser - Parses the document in similar fashion to SAX parser does,
but StAX is a PULL API where as SAX is a PUSH API. It means in case of StAX parser, 
client application need to ask StAX parser to get information from XML whenever 
it needs but in case of SAX parser, client application is required to get information 
when SAX parser notifies the client application that information is available.
Using StAX parser, we can parse, modify and create a XML document.


## 15. What New Features Were Added in Java 8?

Java 8 ships with several new features, but the most significant are the following:

+ Lambda Expressions − a new language feature allowing us to treat actions as objects
+ Method References − enable us to define Lambda Expressions by referring to methods directly using their names
+ Optional − special wrapper class used for expressing optionality
+ Functional Interface – an interface with maximum one abstract method; implementation can be provided using a Lambda Expression
+ Default methods − give us the ability to add full implementations in interfaces besides abstract methods
+ Nashorn, JavaScript Engine − Java-based engine for executing and evaluating JavaScript code
+ Stream API − a special iterator class that allows us to process collections of objects in a functional manner
+ Date API − an improved, immutable JodaTime-inspired Date API


## 16. What New Features Were Added in Java 11?

Java 11 ships with several new features, but the most significant are the following:

+ New methods to the String class: isBlank, lines, strip, stripLeading, stripTrailing, and repeat.
+ New File Methods − readString and writeString static methods from the Files class.
+ The new HTTP client − improves overall performance and provides support for both HTTP/1.1 and HTTP/2
+ Modular System – since Java 9


## 17. What Is a Lambda Expression and What Is It Used For?

In very simple terms, a lambda expression is a function that we can reference and pass around as an object.

Moreover, lambda expressions introduce functional style processing in Java, and facilitate 
the writing of compact and easy-to-read code.

As a result, lambda expressions are a natural replacement for anonymous classes such as method arguments. 
One of their main uses is to define inline implementations of functional interfaces.


## 18. What Is an Exception?

An exception is an abnormal event that occurs during the execution of a program 
and disrupts the normal flow of the program's instructions.
The throws keyword is used to specify that a method may raise an exception during its execution.
The throw keyword allows us to throw an exception object to interrupt the normal flow of the program.
We can handle exception by using a try-catch-finally statement.
The block of code in which an exception may occur is enclosed in a try block. This block is also called “protected” or “guarded” code.
If an exception occurs, the catch block that matches the exception being thrown is executed, if not, all catch blocks are ignored.
The finally block is always executed after the try block exits, whether an exception was thrown or not inside it.
A checked exception must be handled within a try-catch block or declared in a throws clause; 
whereas an unchecked exception is not required to be handled nor declared.
An exception is an event that represents a condition from which is possible to recover, 
whereas error represents an external situation usually impossible to recover from.


## 19. How to Generate OutOfMemoryError and StackOverflowException?

OutOfMemoryError
```java
List<long[]> list = new LinkedList<long[]>();
while (true) {
  list.add(new long[65536]); // an arbitrary number
  // sleep(1) perhaps?
}
```
StackOverflowException
```java
public class StackOverflowErrorExample {

    public static void recursivePrint(int num) {
        System.out.println("Number: " + num);

        if(num == 0)
            return;
        else
            recursivePrint(++num);
    }

    public static void main(String[] args) {
        StackOverflowErrorExample.recursivePrint(1);
    }
}
```


## 20. What Are Annotations? What Are Their Typical Use Cases?

Annotations are metadata bound to elements of the source code of a program and have no effect on the operation of the code they operate.

Their typical uses cases are:
+ Information for the compiler – with annotations, the compiler can detect errors or suppress warnings
+ Compile-time and deployment-time processing – software tools can process annotations and generate code, configuration files, etc.
+ Runtime processing – annotations can be examined at runtime to customize the behavior of a program

Annotations are a form of an interface where the keyword interface is preceded by @, and whose body contains annotation type element declarations that look very similar to methods:
```java
public @interface SimpleAnnotation {
    String value();

    int[] types();
}
```
After the annotation is defined, yon can start using it in through your code:
```java
@SimpleAnnotation(value = "an element", types = 1)
public class Element {
    @SimpleAnnotation(value = "an attribute", types = { 1, 2 })
    public Element nextElement;
}
```

## 21. What is immutable class?

Immutable objects are those objects whose state can not be changed once created. 
Class whose objects possess this characteristic can be termed as immutable class.
For example : String , Integer.
Immutable classes are thread safe because you can not change state of immutable objects, 
so even if two thread access immutable object in parallel, it won’t create any issue.

To create an immutable class in java, you have to do following steps.
+ Declare the class as final so it can’t be extended.
+ Make all fields private so that direct access is not allowed.
+ Don’t provide setter methods for variables
+ Make all mutable fields final so that it’s value can be assigned only once.
+ Initialize all the fields via a constructor performing deep copy.
+ Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.


1. ****What is the difference between an Interface and an Abstract class?****

    Both define an interface that has to be implemented. Abstract class can contain concrete methods as well as abstract. Abstract class can contain regular class fields. Interface can contain only public static final fields.

2. **What is the purpose of garbage collection in Java, and when is it used?**

    GC in Java is the mechanism that keeps track of memory and objects residing in memory. GC collects the object when it is no longer needed (usually when no references to the object are available).

3. **What is the difference between a constructor and a method?**

    We can say that constructor is a special kind of method that instantiates the object. The main differences are

    * Special treatment of constructors when they are called (memory allocation, superclass constructors chain)
    * More caution is required when writing a constructor

4. **State the significance of public, private, protected, default modifiers both singly and in combination and state the effect of package relationships on declared items qualified by these modifiers.**

    * public  
        class -- accessible from anywhere. Can be subclassed by anyone (if not declared final)  
        method -- accessible from anywhere. Can be overriden in subclasses.  
        variable -- accessible from anywhere. Usually not a good practice except for the constants  
        inner class -- accessible from anywhere.  
        nested class -- accessible from anywhere.  
    * private  
        class -- only for inner classes.  
        method -- accessible only from the class where it is declared. Cannot be overridden  
        variable -- accessible only from the class where it is declared  
        inner class -- same  
        nested class -- same  
    * protected  
        class -- only for inner classes  
        method -- accessible from the same package or from any subclass  
        variable -- same  
        inner class -- same  
        nested class -- can be written but doesn't make sense (protected static!?)  
    * default (no access modifier)  
        class -- only this package and subclasses in this package  
        method -- same  
        variable -- same  
        inner class -- same  
        nested class -- same 

5. **What is an abstract class?**

    An abstract class is a java class that has one or more abstract methods (no body). Abstract classes cannot be instantiated. Abstract class defines an interface that has to be implemented by all its subclasses.

6. **What is static in java?**

    static is Java Language keyword.  
    a) When used with a method defines a method of a class.  
    b) When used with a field defines a class field.  
    c) When used on an nested class declaration defines a static nested class.  
    d) Also can be used for static initialization block.  
    e) Can be used as a static initialization block

7. **What is final?**

    final is Java Language keyword.  
    a) When used with a method protects it from being overridden in subclasses. Done for security and/or performance reasons.  
    b) When used with a field means that the value stored in the field cannon be changed after initialization. Not to be confused with immutability of the object.  
    c) When used with a class declaration protects it from being subclassed. Done for security and/or performance reasons. Also for immutability. Many of Java core classes are final (e.g. String)

8. **How can one prove that the array is not null but empty using one line of code?**

    array == null ? xx : array.length == 0
    if the array is instance field it's initialized to null. And this code works.
    if the array is local variable the compiler will generate an error if it has not been initialized

9. **What environment variables do I need to set on my machine in order to be able to run Java programs?**

    CLASSPATH, PATH and/or JAVA_HOME

10. **Do I need to import java.lang package any time? Why ?**

    No. It is imported by default

11. **Can I import same package/class twice? Will the JVM load the package twice at runtime?**

    Yes you can declare import twice in the import section.
    No it will not be loaded twice at runtime.

12. **What is Overriding?**

    Changing method behavior in the subclasses.

13. **What are different types of inner classes?**

    if declared with static -- it's nested class. Nested classes are fairly independent and treated as top-level classes. But the constructor call is different.
    To construct one: new OuterClassNeme.InnerClassName().

    if declared without static -- inner class. Each instance of inner class can only exist within an instance of the outer class.
    To construct one: instanceOfOuterClass.new InnerClassName()

    local class -- declared and visible only within a block of code
    anonymous -- same, but they don't even have a name.

14. **Are the imports checked for validity at compile time? e.g. will the code containing an import such as java.lang.ABCD compile?**

    Yes, they are checked. No it won't compile.

15. **Does importing a package imports the sub-packages as well? e.g. Does importing com.MyTest.* also** import com.MyTest.UnitTests.*?

    No. This declaration will only import classes located directly in com.MyTest package.

16. **What is the difference between declaring a variable and defining a variable?**

    Declaring is declaring. Defining is assigning some value to the declared vaiable.

17. **What is the default value of an object reference declared as an instance variable?**

    null

18. **Can a top level class be private or protected?**

    No. It is only allowed to be public or to have default access modifier.

19. **What type of parameter passing does Java support?**

    Java passes all parameters by values. The references to objects are passed by values.

20. **Primitive data types are passed by reference or pass by value?**

    See above

21. **Objects are passed by value or by reference?**

    See above

22. **What are pass by reference and pass by value?**

    Pass by reference -- a reference to the Object is passed to the method.
    Pass by value -- a copy of the actual value of the Object is passed to the method. The method is then unable to modify the original Object. (Not true in Java. In Java references to objects are passed by value)

23. **Give a simplest way to find out the time a method takes for execution without using any profiling tool?**

    System.currentTimeMillis() in the beginning and end of the method

24. **Is Empty .java file a valid source file?**

    Yes it is.

25. **Can a .java file contain more than one java classes?**

    Yes it can. It has to contain only one top level public java class but it can contain any number of inner, anonymous and top level classes with default access modifier.

26. **Is String a primitive data type in Java?**

    No. String is an Object. An immutable one.

27. **Is main a keyword in Java?**

    No. main is the name of the method that is treated in special way if declared properly.

28. **Is next a keyword in Java?**

    No. next() is method of Iterator or Enumeration interface.

29. **Is delete a keyword in Java?**

    No. delete is not a keyword. And I cannot even remember a class that has a method called delete(). Rather remove()

30. **Is exit a keyword in Java?**

    No. exit() is a method of java.lang.System class

31. **What happens if you dont initialize an instance variable of any of the primitive types in Java?**

    It gets assigned the default value. 0 for int and long, 0.0 for float and double, false for boolean. Though I tried to compile a class where variables were not initialized and it didn't compile.

32. **What are the different scopes for Java variables?**

    static fields, instance fields, method parameters, local variables

33. **What is the default value of the local variables?**

    No default value. Default values are assigned to instance fields. Local variables have to be explicitly initialized.

34. **Does garbage collection guarantee that a program will not run out of memory?**

    No. Not at all. Example: recursive call. Or just create lots of objects until you get OutOfMemoryError (or is it an exception?)

35. **What is the purpose of finalization?**

    Free up the resources. (e.g. close connections and streams, release a lock etc)

36. **Can a public class MyClass be defined in a source file named YourClass.java?**

    no. Unless it is a nested class public class.

37. **What will be the output of the following statement? System.out.println ("1" **+ 3);**

    13

38. **What will be the default values of all the elements of an array defined as an instance variable?**

    All elements will be initialized to default value of corresponding type.

39. **Length in bytes for primitive types**

    | Primitive type| length in bytes  | Comment                                 |
    | :------------ |:----------------:| ---------------------------------------:|
    | boolean       | 1 bit            |  saved as 4 bytes; 1 byte in an array   |
    | char          | 2 bytes          |  unsigned                               |
    | byte          | 1 byte           |                                         |
    | short         | 2 bytes          |                                         |
    | int           | 4 bytes          |                                         |
    | long          | 8 bytes          |                                         |
    | float         | 4 bytes          |                                         |
    | double        | 8 bytes          |                                         |


40. **Contract between equals() and hashCode()**

    if a.equals(b) returns true then a.hashCode() == b.hashCode() is also true. Note that equal hashCode doesn't mean anything.

41. **What different between StringBuffer and StringBuilder?**

    StringBuilder -- new. StringBuffer -- old. StringBuffer -- synchronized. Where possible use StringBuilder.
    Both represent mutable sequence of characters.

42. **What internal methods of String do you know?**

    static methods of String class: valueOf
    indexOf, lastIndexOf, replace, contains, startsWith, endsWith, substring
    matches, split
    equals, isEmpty

43. **Purpose, types and creation of nested classes**

    Types of nested classes see above.
    Purpose:
    If a package-private top-level class (or interface) is used by only one class, consider making the top-level class a private nested class of the sole class that uses. This reduces its accessibility from all the classes in its package to the one class that uses it. But it is far more important to reduce the accessibility of a gratuitously public class than of a package-private top-level class: the public class is part of the package’s API, while the package-private top-level class is already part of its implementation.
    One common use of a static member class is as a public helper class, useful only in conjunction with its outer class
    If an instance of a nested class can exist in isolation from an instance of its enclosing class, then the nested class must be a static member class: it is impossible to create an instance of a nonstatic member class without an enclosing instance.
    One common use of a nonstatic member class is to define an Adapter that allows an instance of the outer class to be viewed as an instance of some unrelated class.
    For example, implementations of the Map interface typically use nonstatic member classes to implement their collection views, which are returned by Map’s keySet, entrySet, and values methods. Similarly, implementations of the collection interfaces, such as Set and List, typically use nonstatic member classes to implement their iterators.[Effective Java]
    A common use of private static member classes is to represent components of the object represented by their enclosing class. For example, consider a Map instance, which associates keys with values. Many Map implementations have an internal Entry object for each key-value pair in the map.
    One common use of anonymous classes is to create function objects on the fly. For example, the sort method invocation sorts an array of strings according to their length using an anonymous Comparator instance.
    To recap, there are four different kinds of nested classes, and each has its place. If a nested class needs to be visible outside of a single method or is too long to fit comfortably inside a method, use a member class. If each instance of the member class needs a reference to its enclosing instance, make it nonstatic; otherwise, make it static. Assuming the class belongs inside a method, if you need to create instances from only one location and there is a preexisting type that characterizes the class, make it an anonymous class; otherwise, make it a local class.

44. **What does it mean that an object or a class is mutable or immutable?**

    Immutability: the state of the object doesn't change

45. **Is it enough to define this class as final? To make this class immutable?**

    No. If the class is declared final it only means that it cannot be subclassed. If the instance of the class is declared to be final it only means that the reference will not change. The inner state of the object in both cases can change.

46. **Besides “String” do you know any other immutable classes?**

    BigDecimal, BigInteger all classes that correspond to primitive types
    java.awt.Color

47. **Increasing/descreasing of methods visibility (inheritence)**

    The main rule is that visibility cannot be reduced in the subclass

48. **You need to create the string, which contains 1,000,000 **random numbers, comma separated. How would** you do that, considering performance?

    I would use StringBuilder class

49. **Garbage collection principles**

    The garbage collector first performs a task called marking. The garbage collector traverses the application graph, starting with the root objects; those are objects that are represented by all active stack frames and all the static variables loaded into the system. Each object the garbage collector meets is marked as being used, and will not be deleted in the sweeping stage. The sweeping stage is where the deletion of objects take place.

50. **Java de-compiler, when it could be helpful except studying, learning, stealing**

    Recovering lost sources?TODO????????

51. **How is the virtual space divided in Java?**

    http://stackoverflow.com/questions/1262328/how-is-the-java-memory-pool-divided
    http://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html

52. **What difference between float and BigDecimal. How they store the data?**

    float is floating point number and can loose precision during the computations.
    BigDeciamal is fixed point number. The computations (which type of computations?) are guaranteed to maintain the needed precision.
    Internally BigDecimal consists of an arbitrary precision integer unscaled value and a 32-bit integer scale
    If no rounding mode is specified and the exact result cannot be represented, an exception is thrown

53. **What is deep copy of a Java object?**

    Deep copy creates a copy of the object including deep copies of all its fields.

54. **What are utilities for JVM monitoring? What is Jconsole?**

    From http://docs.oracle.com/javase/6/docs/technotes/tools/

    jvisualvm --  A graphical tool that provides detailed information about the Java technology-based applications (Java applications) while they are running in a Java Virtual Machine. Java VisualVM provides memory and CPU profiling, heap dump analysis, memory leak detection, access to MBeans, and garbage collection.See Java VisualVM for more information.

    jconsole --    A JMX-compliant graphical tool for monitoring a Java virtual machine. It can monitor both local and remote JVMs. It can also monitor and manage an application.

    jps --    Experimental: JVM Process Status Tool - Lists instrumented HotSpot Java virtual machines on a target system.

    jstat -- Experimental: JVM Statistics Monitoring Tool - Attaches to an instrumented HotSpot Java virtual machine and collects and logs performance statistics as specified by the command line options.

    jstatd -- Experimental: JVM jstat Daemon - Launches an RMI server application that monitors for the creation and termination of instrumented HotSpot Java virtual machines and provides a interface to allow remote monitoring tools to attach to Java virtual machines running on the local system.

    jhat -- Experimental - Heap Dump Browser - Starts a web server on a heap dump file (eg, produced by jmap -dump), allowing the heap to be browsed.

    jmap -- Experimental - Memory Map for Java - Prints shared object memory maps or heap memory details of a given process or core file or a remote debug server.

    jsadebugd -- Experimental - Serviceability Agent Debug Daemon for Java - Attaches to a process or core file and acts as a debug server.

    jstack -- Experimental - Stack Trace for Java - Prints a stack trace of threads for a given process or core file or remote debug server.

    Never used any of these tools yet. :(

55. **How and in what cases we need to configure sizes of memory areas in Java?**

    In case of getting OutOfMemoryError: Java heap space. What other cases?
    JVM parameter -Xmx###m where ### is number of megabytes you need for the JVM.
    -Xms###m to set the initial heap size
    More info on this topic can be found here: http://blog.codecentric.de/en/2011/03/java-memory-configuration-and-monitoring-3rd-act/

56. **What is an Object and how do you allocate memory to it?**

    Object is the base class in Java. Object in general case is an instance of a class. The memory is allocated when new operator is executed. The minimum size is 8 bytes (thats what you get if you call new Object). Each primitive data type takes 4 bytes, except double and long, which take 8 bytes.

58. **What are methods and how are they defined?**

    Method is an abstraction that defines how a specific computation has to be carried out. Method "abstracts away" the code it contains.

59. **What is the use of bin and lib in JDK?**

    bin -- all java binaries: javac, java, appletviewer, jconsole...
    lib -- java libraries

60. **What is casting?**

    changing the type of the object.

61. **In how many ways can an argument be passed to a subroutine and explain them?**

    only one. By value. See above

62. **What is the difference between an argument and a parameter?**

    parameter -- abstract. argument -- concrete value of the parameter.
    parameters of the function are defined when the function is declared
    arguments of the funciton are defined when it is called

63. **What is final, finalize() and finally?**

    final -- Java keyword, see above
    finalize() -- gets called before the object is GC-ed
    finally -- Java keyword used in exception handling.

64. **What is UNICODE?**

    See info on Unicode here http://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Character.html

65. **What is finalize() method?**

    See above.

66. **What are Transient and Volatile Modifiers?**

    Transient signifies that the field is not part of the object state (e.g. it's some derieved value or some cache). Transient fields are not present in serialized representation of the object.
    If field is declared with volatile keyword then any thread that reads the field will see the most recently written value [Effective Java Item 66]

67. **What is difference between overloading and overriding?**

    overloading -- adding a method with the same name but different signature
    overriding -- changing the method implementation in the subclass

68. **What is meant by Inheritance and what are its advantages?**

    Inheritance is one of principles of OOP. It allows to create class hierarchies. Classes can inherit methods and properties from the base classes thus increasing code reuse.

69. **What is the difference between this() and super()?**

    this() calls the constructor of current class.
    super() calls the superclass constructor
    super() has to be the first statement of subclass constructor;
    this and super are references to the current object and to current object treated as superclass.
    this.new Something() has to be used to create inner classes

70. **What is the difference between superclass and subclass?**

    Obvious.

71. **What modifiers may be used with top-level class?**

    only public or default (package-private)

72. **What is a package?**

    In Java package is a mechanism to oragnize classes into modules.

73. **What is a reflection package?**

    Not sure the question is clearly stated. What I would answer is pasted from javadoc of java.lang.reflect
    Provides classes and interfaces for obtaining reflective information about classes and objects. Reflection allows programmatic access to information about the fields, methods and constructors of loaded classes, and the use reflected fields, methods, and constructors to operate on their underlying counterparts on objects, within security restrictions.

74. **What is the difference between Integer and int?**

    Integer is a wrapper class for int primitive type. Integer can be used in generic collections whereas int cannot. Also contains a number of utility methods.

75. **What is a cloneable interface and how many methods does it contain?**

    Cloneable -- is a marker interface and it doesn't contain any methods. It determines the behavior of Object’s protected clone implementation: if a class implements Cloneable, Object’s clone method returns a field-by-field copy of the object; otherwise it throws CloneNotSupportedException

76. **Can you have an inner class inside a method and what variables can you access?**

    You can create a local or anonymous class inside the method. It can access only final variables.

77. **What is the difference between String and StringBuffer?**

78. **What is the difference between a while statement and a do statement?**

    do is guaranteed to execute at least once.

79. **What is the difference between static and non-static variables?**

    a) The way they are initialized. Static are initalized when the class is loaded. Non-static -- when it's instantiated.
    b) Non-static belong to the instance of an object while static are class variables.
    c) Static are accessed using ClassName.varName

80. **How does Java handle integer overflows and underflows?**

    It goes down to the MIN_INT value in case of overflow and to MAX_INT in case of overflow

Main method
---------------
1. **Can an application have multiple classes having main method?**

    Yes it can. But only one main method will be used as the entrance point for the program.

2. **Can I have multiple main methods in the same class?**

    No, if you mean public static void main(String[] args).
    Yes, if you mean a method with a name "main" and any other signature

3. **What if the main method is declared as private?**

    The class will compile. But the method cannot be used as the entrance point

4. **What if the static modifier is removed from the signature of the main method?**

    It becomes an instance method. No longer an entrance point but just a valid regular method.

5. **What if I write static public void instead of public static void?**

    Nothing happens. Class compiles. Method runs.

6. **What if I do not provide the String array as the argument to the method?**

    You just define a static method called "main" with no parameters. It cannot be used as entrance point.

7. **What is the first argument of the String array in main method?**

    These are the parameters passed to the program from command line.

8. **If I do not provide any arguments on the command line, then the String array of Main method will be** empty or null?

    Array of size 0

9. **Can main method be declared final?**

    Yes it can be declared as final.

# Java Collections

#### 18. What are the basic interfaces of Java Collections Framework ?  
[Java Collections Framework](http://docs.oracle.com/javase/7/docs/technotes/guides/collections/overview.html) provides a well designed set of interfaces and classes that support operations on a collections of objects. The most basic interfaces that reside in the Java Collections Framework are:

* [Collection](http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html), which represents a group of objects known as its elements.
* [Set](http://docs.oracle.com/javase/7/docs/api/java/util/Set.html), which is a collection that cannot contain duplicate elements.
* [List](http://docs.oracle.com/javase/7/docs/api/java/util/List.html), which is an ordered collection and can contain duplicate elements.
* [Map](http://docs.oracle.com/javase/7/docs/api/java/util/Map.html), which is an object that maps keys to values and cannot contain duplicate keys.

#### 19. Why Collection doesn’t extend Cloneable and Serializable interfaces ? 
The [Collection](http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html) interface specifies groups of objects known as elements. Each concrete implementation of a [Collection](http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html) can choose its own way of how to maintain and order its elements. Some collections allow duplicate keys, while some other collections don’t. The semantics and the implications of either cloning or serialization come into play when dealing with actual implementations. Thus, the concrete implementations of collections should decide how they can be cloned or serialized.

#### 20. What is an Iterator ? 
The [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html) interface provides a number of methods that are able to iterate over any [Collection](http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html). Each Java [Collection](http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html) contains the [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)  method that returns an [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)  instance. Iterators are capable of removing elements from the underlying collection during the iteration.

#### 21. What differences exist between Iterator and ListIterator ? 
The differences of these elements are listed below:

* An [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)  can be used to traverse the [Set](http://docs.oracle.com/javase/7/docs/api/java/util/Set.html) and [List](http://docs.oracle.com/javase/7/docs/api/java/util/List.html)  collections, while the [ListIterator](http://docs.oracle.com/javase/7/docs/api/java/util/ListIterator.html) can be used to iterate only over [List](http://docs.oracle.com/javase/7/docs/api/java/util/List.html) .
* The [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)  can traverse a collection only in forward direction, while the [ListIterator](http://docs.oracle.com/javase/7/docs/api/java/util/ListIterator.html) can traverse a [List](http://docs.oracle.com/javase/7/docs/api/java/util/List.html) in both directions.
* The [ListIterator](http://docs.oracle.com/javase/7/docs/api/java/util/ListIterator.html) implements the [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)  interface and contains extra functionality, such as adding an element, replacing an element, getting the index position for previous and next elements, etc.

#### 22. What is difference between fail-fast and fail-safe ? 
The [Iterator's](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)  fail-safe property works with the clone of the underlying collection and thus, it is not affected by any modification in the collection. All the collection classes in java.util package are fail-fast, while the collection classes in java.util.concurrent are fail-safe. Fail-fast iterators throw a [ConcurrentModificationException](http://examples.javacodegeeks.com/java-basics/exceptions/java-util-concurrentmodificationexception-how-to-handle-concurrent-modification-exception/), while fail-safe iterator never throws such an exception.

#### 23. How HashMap works in Java ? 
[A HashMap in Java stores key-value pairs](http://www.javacodegeeks.com/2014/03/how-hashmap-works-in-java.html). The [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) requires a hash function and uses hashCode and equals methods, in order to put and retrieve elements to and from the collection respectively. When the put method is invoked, the [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) calculates the hash value of the key and stores the pair in the appropriate index inside the collection. If the key exists, its value is updated with the new value. Some important characteristics of a [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) are its capacity, its load factor and the threshold resizing.

####24. What is the importance of hashCode() and equals() methods ? 
A [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) in Java uses the hashCode and equals methods to determine the index of the key-value pair. These methods are also used when we request the value of a specific key. If these methods are not implemented correctly, two different keys might produce the same hash value and thus, will be considered as equal by the collection. Furthermore, these methods are also used to detect duplicates. Thus, the implementation of both methods is crucial to the accuracy and correctness of the [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html).

#### 25. What differences exist between HashMap and Hashtable ? 
Both the [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) and [Hashtable](http://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html) classes implement the Map interface and thus, have very similar characteristics. However, they differ in the following features:

* A [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) allows the existence of null keys and values, while a [Hashtable](http://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html) doesn’t allow neither null keys, nor null values.
* A [Hashtable](http://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html) is synchronized, while a [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) is not. Thus, [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) is preferred in single-threaded environments, while a [Hashtable](http://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html) is suitable for multi-threaded environments.
* A [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) provides its set of keys and a Java application can iterate over them. Thus, a [HashMap](http://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html) is fail-fast. On the other hand, a [Hashtable](http://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html) provides an [Enumeration](http://docs.oracle.com/javase/7/docs/api/java/util/Enumeration.html) of its keys.
* The [Hashtable](http://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html) class is considered to be a legacy class.

#### 26. What is difference between Array and ArrayList ? When will you use Array over ArrayList ?
The Array and ArrayList classes differ on the following features:

* [Arrays](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html) can contain primitive or objects, while an [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html) can contain only objects.
* [Arrays](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html) have fixed size, while an [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html) is dynamic.
* An [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html) provides more methods and features, such as addAll, removeAll, iterator, etc.
* For a list of primitive data types, the collections use autoboxing to reduce the coding effort. However, this approach makes them slower when working on fixed size primitive data types.

#### 27. What is difference between ArrayList and LinkedList ? 
Both the [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html) and [LinkedList](http://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html) classes implement the List interface, but they differ on the following features:

* An [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html) is an index based data structure backed by an [Array](http://docs.oracle.com/javase/7/docs/api/java/lang/reflect/Array.html). It provides random access to its elements with a performance equal to O(1). On the other hand, a [LinkedList](http://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html) stores its data as list of elements and every element is linked to its previous and next element. In this case, the search operation for an element has execution time equal to O(n).
* The Insertion, addition and removal operations of an element are faster in a [LinkedList](http://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html) compared to an [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html), because there is no need of resizing an array or updating the index when an element is added in some arbitrary position inside the collection.
* A [LinkedList](http://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html) consumes more memory than an [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html), because every node in a [LinkedList](http://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html) stores two references, one for its previous element and one for its next element.
Check also our article [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html) vs. [LinkedList](http://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html).

#### 28. What is Comparable and Comparator interface ?
List their differences. Java provides the [Comparable](http://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html) interface, which contains only one method, called [compareTo](http://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html#compareTo(T)). This method compares two objects, in order to impose an order between them. Specifically, it returns a negative integer, zero, or a positive integer to indicate that the input object is less than, equal or greater than the existing object. Java provides the [Comparator](http://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html) interface, which contains two methods, called [compare](http://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html#compare(T,%20T)) and [equals](http://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html#equals(java.lang.Object)). The first method compares its two input arguments and imposes an order between them. It returns a negative integer, zero, or a positive integer to indicate that the first argument is less than, equal to, or greater than the second. The second method requires an object as a parameter and aims to decide whether the input object is equal to the comparator. The method returns true, only if the specified object is also a comparator and it imposes the same ordering as the comparator.

#### 29. What is Java Priority Queue ? 
The [PriorityQueue](http://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html) is an unbounded queue, based on a priority heap and its elements are ordered in their natural order. At the time of its creation, we can provide a Comparator that is responsible for ordering the elements of the [PriorityQueue](http://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html). A [PriorityQueue](http://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html) doesn’t allow null values, those objects that doesn’t provide natural ordering, or those objects that don’t have any comparator associated with them. Finally, the Java [PriorityQueue](http://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html) is not thread-safe and it requires O(log(n)) time for its enqueing and dequeing operations.

#### 30. What do you know about the big-O notation and can you give some examples with respect to different data structures ?
The Big-O notation simply describes how well an algorithm scales or performs in the worst case scenario as the number of elements in a data structure increases. The Big-O notation can also be used to describe other behavior such as memory consumption. Since the collection classes are actually data structures, we usually use the Big-O notation to chose the best implementation to use, based on time, memory and performance. Big-O notation can give a good indication about performance for large amounts of data.

#### 31. What is the tradeoff between using an unordered array versus an ordered array ? 
The major advantage of an ordered array is that the search times have time complexity of O(log n), compared to that of an unordered array, which is O (n). The disadvantage of an ordered array is that the insertion operation has a time complexity of O(n), because the elements with higher values must be moved to make room for the new element. Instead, the insertion operation for an unordered array takes constant time of O(1).

#### 32. What are some of the best practices relating to the Java Collection framework ?

* Choosing the right type of the collection to use, based on the application’s needs, is very crucial for its performance. For example if the size of the elements is fixed and know a priori, we shall use an [Array](http://docs.oracle.com/javase/7/docs/api/java/lang/reflect/Array.html), instead of an [ArrayList](http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html).
* Some collection classes allow us to specify their initial capacity. Thus, if we have an estimation on the number of elements that will be stored, we can use it to avoid rehashing or resizing.
* Always use Generics for type-safety, readability, and robustness. Also, by using Generics you avoid the [ClassCastException](http://docs.oracle.com/javase/7/docs/api/java/lang/ClassCastException.html) during runtime.
* Use immutable classes provided by the Java Development Kit (JDK) as a key in a Map, in order to avoid the implementation of the [hashCode](http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode%28%29) and equals methods for our custom class.
* Program in terms of interface not implementation.
* Return zero-length collections or arrays as opposed to returning a null in case the underlying collection is actually empty.

#### 33. What’s the difference between Enumeration and Iterator interfaces ? 
[Enumeration](http://docs.oracle.com/javase/7/docs/api/java/util/Enumeration.html) is twice as fast as compared to an Iterator and uses very less memory. However, the [Iterator](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html) is much safer compared to [Enumeration](http://docs.oracle.com/javase/7/docs/api/java/util/Enumeration.html), because other threads are not able to modify the collection object that is currently traversed by the iterator. Also, [Iterators](http://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html) allow the caller to remove elements from the underlying collection, something which is not possible with [Enumeration](http://docs.oracle.com/javase/7/docs/api/java/util/Enumeration.html).

#### 34. What is the difference between HashSet and TreeSet ? 
The [HashSet](http://docs.oracle.com/javase/7/docs/api/java/util/HashSet.html) is Implemented using a hash table and thus, its elements are not ordered. The add, remove, and contains methods of a [HashSet](http://docs.oracle.com/javase/7/docs/api/java/util/HashSet.html)  have constant time complexity O(1). On the other hand, a [TreeSet](http://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html) is implemented using a tree structure. The elements in a [TreeSet](http://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html) are sorted, and thus, the add, remove, and contains methods have time complexity of O(logn).


# Exception Handling

#### 1. What are the two types of Exceptions in Java ? Which are the differences between them ? 
Java has two types of exceptions: checked exceptions and unchecked exceptions. Unchecked exceptions do not need to be declared in a method or a constructor’s throws clause, if they can be thrown by the execution of the method or the constructor, and propagate outside the method or constructor boundary. On the other hand, checked exceptions must be declared in a method or a constructor’s throws clause. See here for tips on [Java exception handling](http://www.javacodegeeks.com/2013/07/java-exception-handling-tutorial-with-examples-and-best-practices.html).

#### 2. What is the difference between Exception and Error in java ? 
[Exception](http://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html) and [Error](http://docs.oracle.com/javase/7/docs/api/java/lang/Error.html) classes are both subclasses of the [Throwable](http://docs.oracle.com/javase/7/docs/api/java/lang/Throwable.html) class. The [Exception](http://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html)  class is used for exceptional conditions that a user’s program should catch. The [Error](http://docs.oracle.com/javase/7/docs/api/java/lang/Error.html)  class defines exceptions that are not excepted to be caught by the user program.

#### 3. What is the difference between throw and throws ? 
The throw keyword is used to explicitly raise a exception within the program. On the contrary, the throws clause is used to indicate those exceptions that are not handled by a method. Each method must explicitly specify which exceptions does not handle, so the callers of that method can guard against possible exceptions. Finally, multiple exceptions are separated by a comma.

#### 4. What is the importance of finally block in exception handling ?
A finally block will always be executed, whether or not an exception is actually thrown. Even in the case where the catch statement is missing and an exception is thrown, the finally block will still be executed. Last thing to mention is that the finally block is used to release resources like I/O buffers, database connections, etc.

#### 5. What will happen to the Exception object after exception handling ? 
The [Exception](http://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html) object will be garbage collected in the next garbage collection.

#### 6. How does finally block differ from finalize() method ?
A finally block will be executed whether or not an exception is thrown and is used to release those resources held by the application. Finalize is a protected method of the Object class, which is called by the Java Virtual Machine (JVM) just before an object is garbage collected.
