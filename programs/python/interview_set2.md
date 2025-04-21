<details open>
<summary>Java program that counts the number of prime numbers less than a given non-negative integer N.</summary>
<p>

```python
    def count_primes(n):
    if n <= 2:
        return 0

    # Create a boolean array "is_prime[0..n-1]" and initialize all entries as true
    is_prime = [True] * n
    is_prime[0] = is_prime[1] = False  # 0 and 1 are not prime

    for i in range(2, int(n ** 0.5) + 1):
        if is_prime[i]:
            print(f"Marking multiples of {i} as non-prime.")
            for j in range(i * i, n, i):
                is_prime[j] = False

    prime_count = sum(is_prime)
    print(f"Total primes less than {n}: {prime_count}")
    return prime_count

# Example usage
if __name__ == "__main__":
    N = 20
    count_primes(N)

```

</p>
</details>

<details>
<summary>Design a data structure that follows the constraints of a Least Recently Used (LRU) cache, we can combine the features of a doubly linked list and a hash map..</summary>
<p>

```python
 class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}  # key -> node

        # Create dummy head and tail for easy operations
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    # Add node right after head
    def _add_node(self, node):
        print(f"Adding node: {node.key}")
        node.prev = self.head
        node.next = self.head.next

        self.head.next.prev = node
        self.head.next = node

    # Remove a node from the list
    def _remove_node(self, node):
        print(f"Removing node: {node.key}")
        prev = node.prev
        next = node.next
        prev.next = next
        next.prev = prev

    # Move existing node to the front (most recently used)
    def _move_to_front(self, node):
        self._remove_node(node)
        self._add_node(node)

    # Pop the least recently used item (before tail)
    def _pop_tail(self):
        node = self.tail.prev
        self._remove_node(node)
        print(f"Popping tail: {node.key}")
        return node

    def get(self, key: int) -> int:
        if key in self.cache:
            node = self.cache[key]
            self._move_to_front(node)
            print(f"GET {key}: {node.value}")
            return node.value
        print(f"GET {key}: -1 (not found)")
        return -1

    def put(self, key: int, value: int):
        print(f"PUT {key} = {value}")
        if key in self.cache:
            node = self.cache[key]
            node.value = value
            self._move_to_front(node)
        else:
            new_node = Node(key, value)
            self.cache[key] = new_node
            self._add_node(new_node)

            if len(self.cache) > self.capacity:
                tail = self._pop_tail()
                del self.cache[tail.key]

# Example usage
if __name__ == "__main__":
    lru = LRUCache(2)
    lru.put(1, 1)
    lru.put(2, 2)
    lru.get(1)
    lru.put(3, 3)  # Evicts key 2
    lru.get(2)
    lru.put(4, 4)  # Evicts key 1
    lru.get(1)
    lru.get(3)
    lru.get(4)
   
```

</p>
</details>
<details>
<summary>To determine if a given word can be segmented into a space-separated sequence of one or more words from a dictionary, you can use dynamic programming.</summary>
<p>

```python
    def word_break(s, word_dict):
    # Create a dp array of length len(s) + 1, initialized to False
    dp = [False] * (len(s) + 1)
    
    # Base case: an empty string can always be segmented
    dp[0] = True
    
    # Iterate through each position in the string
    for i in range(1, len(s) + 1):
        for j in range(i):
            # Check if the substring s[j:i] is in the dictionary and if dp[j] is True
            if dp[j] and s[j:i] in word_dict:
                dp[i] = True
                break
    
    # Return whether the entire string can be segmented or not
    return dp[len(s)]

# Example usage
if __name__ == "__main__":
    s = "applepenapple"
    word_dict = {"apple", "pen"}
    result = word_break(s, word_dict)
    print(f"Can the string '{s}' be segmented? {result}")

```

</p>
</details>

<details>
<summary>To add two binary strings and return their sum as a binary string.</summary>
<p>

```python
  def add_binary(a: str, b: str) -> str:
    # Initialize result and carry
    result = []
    carry = 0
    
    # Reverse both strings to simplify the addition process
    a = a[::-1]
    b = b[::-1]
    
    # Iterate through both strings
    max_length = max(len(a), len(b))
    
    for i in range(max_length):
        # Get the current bits from a and b (0 if out of range)
        bit_a = int(a[i]) if i < len(a) else 0
        bit_b = int(b[i]) if i < len(b) else 0
        
        # Sum the bits and carry
        total = bit_a + bit_b + carry
        
        # Append the result bit (0 or 1)
        result.append(str(total % 2))
        
        # Update the carry (1 or 0)
        carry = total // 2
    
    # If there's a remaining carry, append it
    if carry:
        result.append('1')
    
    # Reverse the result to match the correct order and join as a string
    return ''.join(result[::-1])

# Example usage
if __name__ == "__main__":
    a = "1010"
    b = "1011"
    print(f"Sum of {a} and {b} is {add_binary(a, b)}")
  
```

</p>
</details>

<details>
<summary>To move all the zeros in a given array to the end while preserving the order of the other elements.</summary>
<p>

```python

def move_zeros_to_end(arr):
    # Pointer to keep track of the position for next non-zero element
    non_zero_index = 0
    
    # Traverse the array
    for i in range(len(arr)):
        if arr[i] != 0:
            # Swap elements to move non-zero element to the "non_zero_index" position
            arr[non_zero_index], arr[i] = arr[i], arr[non_zero_index]
            non_zero_index += 1
    
    return arr

# Example usage
if __name__ == "__main__":
    arr = [0, 1, 9, 0, 3, 12, 0]
    result = move_zeros_to_end(arr)
    print(f"Array after moving zeros to the end: {result}")
 
```

</p>
</details>
