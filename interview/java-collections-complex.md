#### 1.How does ConcurrentHashMap differ from HashMap?
HashMap is not thread-safe and allows one null key and multiple null values. ConcurrentHashMap is thread-safe, does not allow null keys/values, and uses finer-grained locking (bucket level) instead of locking the whole map. Iterators of HashMap are fail-fast, while those of ConcurrentHashMap are fail-safe.

#### 2.Why HashMap performance degraded in Java 8 before they introduced balanced trees for buckets?

Before Java 8, HashMap handled collisions using linked lists. In worst cases where many keys fell into the same bucket, operations degraded from O(1) to O(n). This not only hurt performance but also exposed HashMap to hash collision attacks. In Java 8, to solve this, buckets with many collisions are converted into Red-Black Trees, improving worst-case performance to O(log n).

#### 3.Difference between CopyOnWriteArrayList and ArrayList?

ArrayList is not thread-safe, and its iterators are fail-fast. CopyOnWriteArrayList is thread-safe, and it achieves this by creating a new copy of the array on every write, making iteration fail-safe. It’s best suited for scenarios with many reads and few writes, because writes are expensive due to array copying.

#### 4.How TreeMap stores elements internally (Red-Black Tree)?
TreeMap stores key-value pairs in a Red-Black Tree, which is a self-balancing binary search tree. This ensures that insertion, deletion, and search all take O(log n) time. Unlike HashMap, which uses hashing, TreeMap maintains elements in sorted order based on keys, either by natural ordering or a custom Comparator.

#### 5.Can we store a null key in HashMap? What about HashTable and TreeMap?

HashMap allows one null key and multiple null values. Hashtable does not allow null keys or values at all. TreeMap does not allow null keys (because they can’t be compared), but it allows null values.

