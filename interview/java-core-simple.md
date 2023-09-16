### 1. New Java8 Features

Java 8 provides following features for Java Programming:
*	Lambda expressions - Adds functional processing capability to Java. 
*	Method references - Referencing functions by their names instead of invoking them directly. Using functions as parameters. 
*	Functional interfaces,
*	Stream API - New stream API to facilitate pipeline processing. 
*	Default methods,
*	Base64 Encode Decode,
*	Static methods in interface,
*	Optional class,
*	Collectors class,
*	ForEach() method,
*	+36
*	Parallel array sorting,
*	Nashorn JavaScript Engine - A Java-based engine to execute JavaScript code. 
*	Parallel Array Sorting,
*	Type and Repeating Annotations,
*	IO Enhancements,
*	Concurrency Enhancements,
*	JDBC Enhancements etc.

### 9. What is the final keyword in Java?

**Final variable:**

Once a variable is declared as final, then the value of the variable could not be changed. It is like a constant.

Example:
```java
final int = 12;
```
**Final method:**

A final keyword in a method that couldn’t be overridden. If a method is marked as a final, then it can’t be overridden by the subclass.

**Final class:**

If a class is declared as final, then the class couldn’t be subclassed. No class can extend/inherit the final class.


### 10. What is a Thread?

In Java, the flow of an execution is called Thread. Every java program has at least one thread called main thread, the Main thread is created by JVM. The user can define their own threads by extending Thread class (or) by implementing Runnable interface. Threads are executed concurrently.

Example:
```java
public static void main(String[] args){//main thread starts here

}
```

### 11.	Explain thread life cycle in Java

Thread has the following states:
*	New
*	Runnable
*	Running
*	Non-runnable (Blocked)
*	Terminated


*	**New:** In New state, Thread instance has been created but start () method is not yet invoked. Now the thread is not considered alive.
*	**Runnable:** The Thread is in runnable state after invocation of the start () method, but before the run () method is invoked. But a thread can also return to the runnable state from waiting/sleeping. In this state the thread is considered alive.
*	**Running:** The thread is in running state after it calls the run () method. Now the thread begins the execution.
*	**Non-Runnable(Blocked):** The thread is alive but it is not eligible to run. It is not in a runnable state but also, it will return to runnable state after some time. For Example: wait, sleep, block.
*	**Terminated:** Once the run method is completed then it is terminated. Now the thread is not alive.

### 12. Which methods are used during the Serialization and Deserialization process?

ObjectOutputStream and ObjectInputStream classes are higher level java.io. package. We will use them with lower level classes FileOutputStream and FileInputStream.

ObjectOutputStream.writeObject —->Serialize the object and write the serialized object to a file.

ObjectInputStream.readObject —> Reads the file and deserializes the object.

To be serialized, an object must implement the serializable interface. If a superclass implements Serializable, then the subclass will automatically be serializable.

| Serialization        | Deserialization      | 
| ------------- |-------------|
|Serialization is the process which is used to convert the objects into byte stream|Deserialization is the opposite process of serialization where we can get the objects back from the byte stream.|
|An object is serialized by writing it an ObjectOutputStream.|An object is deserialized by reading it from an ObjectInputStream.|


### 13. When to use Runnable interface Vs Thread class in Java?

If we need our class to extend some other classes other than the thread then we can go with the runnable interface because in java we can extend only one class. If we are not going to extend any class then we can extend the thread class.

### 22.	How do you read data from a flat file in java?

Buffered Reader, Scanner, Files, FileReader

### 25.	How do you prevent someone from overriding a method in a class you write?
 
private, static and final


### 28.	What does it mean if a method or field is static?

You don't need instance of class to call that method or field,the static modifier means something is directly related to a class

### 30.	What is the difference between string and string buffer?

In the Java programming language, strings are treated as objects. The Java platform provides the String class to create and manipulate strings. Whereas, StringBuffer class is a thread-safe, mutable sequence of characters. A string buffer is like a String, but can be modified.

### 67. What is an abstract class in java?

A class which is declared with the abstract keyword is known as an abstract class in Java. It can have abstract and non-abstract methods (method with the body). Abstraction is a process of hiding the implementation details and showing only functionality to the user.

### 68. What is the interface?

An interface in Java is a blueprint of a class. It has static constants and abstract methods. The interface in Java is a mechanism to achieve abstraction. There can be only abstract methods in the Java interface, not method bodies. It is used to achieve abstraction and multiple inheritance in Java. In other words, you can say that interfaces can have abstract methods and variables. It cannot have a method body. Java Interface also represents the IS-A relationship.


### 69. Use of equals in JAVA?

The equals() method compares two strings, and returns true if the strings are equal, and false if not.


