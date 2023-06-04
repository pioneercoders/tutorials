<details open>
<summary>Java program that counts the number of prime numbers less than a given non-negative integer N.</summary>
<p>

```java
public class PrimeCount {

    public static void main(String[] args) {
        int N = 100; // The given non-negative integer
        
        int count = countPrimes(N);
        
        System.out.println("Number of prime numbers less than " + N + ": " + count);
    }
    
    public static int countPrimes(int N) {
        int count = 0;
        
        for (int i = 2; i < N; i++) {
            if (isPrime(i)) {
                count++;
            }
        }
        
        return count;
    }
    
    public static boolean isPrime(int number) {
        if (number <= 1) {
            return false;
        }
        
        for (int i = 2; i <= Math.sqrt(number); i++) {
            if (number % i == 0) {
                return false;
            }
        }
        
        return true;
    }
}

```

</p>
</details>


<details >
<summary>Design a data structure that follows the constraints of a Least Recently Used (LRU) cache, we can combine the features of a doubly linked list and a hash map..</summary>
<p>

```java
import java.util.HashMap;
import java.util.Map;

class LRUCache {
    private class Node {
        int key;
        int value;
        Node prev;
        Node next;
    }

    private int capacity;
    private Map<Integer, Node> cache;
    private Node head;
    private Node tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        cache = new HashMap<>();
        head = new Node();
        tail = new Node();
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        Node node = cache.get(key);
        if (node != null) {
            moveToHead(node);
            return node.value;
        }
        return -1;
    }

    public void put(int key, int value) {
        Node node = cache.get(key);
        if (node != null) {
            node.value = value;
            moveToHead(node);
        } else {
            if (cache.size() == capacity) {
                Node tailNode = removeTail();
                cache.remove(tailNode.key);
            }
            Node newNode = new Node();
            newNode.key = key;
            newNode.value = value;
            cache.put(key, newNode);
            addToHead(newNode);
        }
    }

    private void addToHead(Node node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void moveToHead(Node node) {
        removeNode(node);
        addToHead(node);
    }

    private Node removeTail() {
        Node tailNode = tail.prev;
        removeNode(tailNode);
        return tailNode;
    }
}
```

</p>
</details>
