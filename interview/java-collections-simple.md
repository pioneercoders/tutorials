#### 1. What is Java Collections Framework?

A collection is a group of objects (like a container).

Java provides the Collections Framework (JCF) to handle groups of objects efficiently (storing, searching, sorting, etc.).

It includes:

  - Interfaces → List, Set, Queue, Map

  - Classes → ArrayList, HashSet, HashMap, LinkedList, etc.

  - Algorithms → Sorting, Searching (Collections utility class)

#### 2.What is the difference between Collection and Collections in Java?

1. Collection (Interface)

  - Package: java.util
  - Type: Interface
  - Meaning: It is the root interface of the Java Collection Framework.
  - Purpose: Represents a group of objects (like a container).
  - Implemented by: List, Set, Queue and their subtypes. 

2. Collections (Class)
   
  - Package: java.util
  - Type: Utility Class (final class)
  - Purpose: Contains static methods that operate on collections (like sorting, searching, synchronizing).
  - Methods: sort(), reverse(), shuffle(), min(), max(), binarySearch(), etc.

#### 3.Difference between List, Set, and Map?

1. List

  - Interface in java.util
  - Stores elements in order (index-based)
  - Allows duplicates
  - Can contain null values (multiple nulls are allowed).

Implementations: ArrayList, LinkedList, Vector, Stack.

2. Set

   - Interface in java.util
   - Does NOT allow duplicates
   - No guaranteed order (depends on implementation).
   - Allows at most one null value.
     
Implementations:

  - HashSet (no order, fastest)
  - LinkedHashSet (insertion order maintained)
  - TreeSet (sorted order, no nulls allowed).
     
3.Map

  - Interface in java.util
  - Stores data as key–value pairs
  - Keys are unique (cannot duplicate)
  - Values can be duplicated
  - Allows one null key (in HashMap) and multiple null values.

Implementations:

  - HashMap (unordered, fastest)
  - LinkedHashMap (insertion order maintained)
  - TreeMap (sorted by keys, no null key).

#### 4.Why ArrayList is better than arrays?

Array vs ArrayList
 1. Size
    - Array: Fixed size. Once you create it, you cannot change the length.
    - ArrayList: Dynamic size. It grows/shrinks automatically when you add/remove elements.
   
 2. Ease of Use
    - Array: No built-in methods except length. You need loops for search, sort, etc.
    - ArrayList: Rich API with methods like add(), remove(), contains(), indexOf(), sort(), etc.

 3. Type Safety
    - Array: Can store both primitives (int, double) and objects.
    - ArrayList: Only objects (but with generics, ensures type safety). For primitives, use wrapper classes (Integer, Double) or collections like IntStream.
   
 4. Performance
    - Array: Slightly faster because it’s lower-level (no overhead).
    - ArrayList: A little slower because it resizes dynamically and offers extra functionality.
   
5.Flexibility
    - Array: Better if you know the exact size and need performance.
    - ArrayList: Better if size changes frequently or you need lots of add/remove/search operations.

#### 5.How HashSet internally works?

HashSet is implemented internally using a HashMap. When we add an element, it’s stored as the key in the HashMap with a dummy value. HashSet uses the element’s hashCode() to find the bucket and equals() to avoid duplicates. That’s why HashSet does not allow duplicates and does not maintain order.

#### 6.Difference between HashMap and Hashtable?

HashMap is non-synchronized, allows one null key and multiple null values, and is faster. Hashtable is synchronized, does not allow any null key or value, and is slower. Hashtable is a legacy class; nowadays, HashMap or ConcurrentHashMap is preferred.

1. Thread Safety
   
   - HashMap: Not synchronized (not thread-safe). Multiple threads can modify it at the same time → risk of data inconsistency.
   - Hashtable: Synchronized (thread-safe). Only one thread can access it at a time.

But because of synchronization, Hashtable is slower.

2.Null keys and values

HashMap:

  - Allows one null key.

  - Allows multiple null values.

Hashtable:

  - Does not allow null key.

  - Does not allow null values.

3. Performance

  - HashMap: Faster (no synchronization overhead).
  
  - Hashtable: Slower (synchronized methods).

4. Legacy vs Modern

  - HashMap: Introduced in Java 1.2 (part of Collections Framework).

  - Hashtable: Older, introduced in Java 1.0 (legacy class).

Nowadays, HashMap is preferred. For thread safety, we use ConcurrentHashMap instead of Hashtable.

