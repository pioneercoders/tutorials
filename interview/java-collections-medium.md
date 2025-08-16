#### 1.How does HashMap handle collisions internally?

HashMap handles collisions using a LinkedList of entries in each bucket. If multiple keys map to the same index, they are linked together, and HashMap uses equals() to differentiate them. Since Java 8, if the number of collisions in a bucket becomes large (≥ 8), HashMap replaces the LinkedList with a Red-Black Tree, reducing the lookup time from O(n) to O(log n).

 --> Collisions happen when two different keys have the same hashCode() (or hash reduces to the same bucket index).

 
Before Java 8 (JDK 7 and earlier)

Each bucket is a Linked List.

If two keys map to the same bucket:

  - New entry is simply appended at the end of the list.
  - When retrieving, HashMap traverses the linked list → compares keys using equals().
    
Worst-case time complexity: O(n) (if many collisions).

Since Java 8

To improve performance, if too many collisions occur in a bucket:
  - Linked List is converted into a Balanced Tree (Red-Black Tree).
  - This reduces worst-case time complexity from O(n) → O(log n).

Conversion happens when:
  - Number of entries in a bucket exceeds 8 (TREEIFY_THRESHOLD).
  - Provided the table (HashMap capacity) is at least 64.

#### 2.Why String is recommended as a key in HashMap?
String is recommended as a key in HashMap because it is immutable, so its hashCode and equals methods are consistent and reliable. It also provides efficient and well-distributed hashCode implementations, reducing collisions. This makes retrieval and storage in HashMap safe and fast.

1. Immutable nature

String objects are immutable in Java → once created, their hashCode() and equals() values never change.

This makes them safe and reliable as HashMap keys.

If keys were mutable, changing a key’s value after putting it in the HashMap could break retrieval.

2. Well-defined hashCode() and equals()

String class in Java has a final implementation of hashCode() and equals().

It is efficient, well-tested, and ensures correct distribution in HashMap buckets.


3. Good hash distribution

Strings usually provide a good spread of hash codes because they are based on character sequences.

This minimizes collisions in HashMap buckets, improving performance.

4. Readable and Common

Strings are human-readable (easy to debug/log).

Most real-world data naturally comes in string form (like IDs, names, keys, URLs).

#### 3.Difference between fail-fast and fail-safe iterators?

Fail-Fast iterators throw ConcurrentModificationException if the collection is modified during iteration, as they work directly on the collection. Fail-Safe iterators do not throw exceptions because they work on a clone of the collection (e.g., in ConcurrentHashMap, CopyOnWriteArrayList), but they may not reflect the latest changes.

1. Fail-Fast Iterators

Belong to Java Collections Framework (like ArrayList, HashMap, HashSet).

If the collection is modified structurally (add/remove element, not via iterator) while iterating, the iterator throws ConcurrentModificationException.

Uses the collection’s modCount (modification count) to detect changes.

2. Fail-Safe Iterators

Found in concurrent collections (like ConcurrentHashMap, CopyOnWriteArrayList).

They do not throw exceptions if the collection is modified during iteration.

They work on a clone/copy of the collection → changes made during iteration are not visible to the iterator.

#### 4.What is the difference between Comparable and Comparator?

1. Comparable (java.lang.Comparable)

Interface: public interface Comparable<T> { int compareTo(T o); }

Used to define the natural ordering of objects.

A class implements Comparable when its objects have a default sorting order.

Sorting logic is inside the class itself.

2. Comparator (java.util.Comparator)

Interface: public interface Comparator<T> { int compare(T o1, T o2); }

Used to define custom sorting logic (multiple ways).

Sorting logic is outside the class.

A class can have multiple comparators for different sorting strategies.

--> Comparable is used to define natural ordering of objects by implementing compareTo inside the class. Comparator is used to define custom sorting outside the class using compare. Comparable allows only one default sorting, while Comparator can provide multiple sorting strategies.

#### 5.Explain the load factor and initial capacity in HashMap.

Initial capacity is the number of buckets a HashMap starts with (default 16). Load factor is the measure of how full the map can get before resizing (default 0.75). When the number of entries exceeds (capacity × loadFactor), HashMap resizes by doubling its capacity to maintain performance.


