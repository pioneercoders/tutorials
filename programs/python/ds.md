<details open>
<summary>1️⃣ Stack Implementation</summary>

```python
class Stack:
    def __init__(self):
        self.stack = []

    def is_empty(self):
        return len(self.stack) == 0

    def push(self, item):
        self.stack.append(item)
        print(f"Pushed: {item}")

    def pop(self):
        if self.is_empty():
            print("Stack is empty. Cannot pop.")
            return None
        popped = self.stack.pop()
        print(f"Popped: {popped}")
        return popped

    def peek(self):
        if self.is_empty():
            print("Stack is empty. Nothing to peek.")
            return None
        return self.stack[-1]

    def size(self):
        return len(self.stack)

    def display(self):
        print("Stack:", self.stack)

if __name__ == "__main__":
    s = Stack()
    s.push(10)
    s.push(20)
    s.push(30)
    s.display()
    print("Top element is:", s.peek())
    s.pop()
    s.display()
    print("Stack size:", s.size())
```

</details>

<details>
<summary>2️⃣ Queue Implementation</summary>

```python
class Queue:
    def __init__(self):
        self.queue = []

    def is_empty(self):
        return len(self.queue) == 0

    def enqueue(self, item):
        self.queue.append(item)
        print(f"Enqueued: {item}")

    def dequeue(self):
        if self.is_empty():
            print("Queue is empty. Cannot dequeue.")
            return None
        dequeued = self.queue.pop(0)
        print(f"Dequeued: {dequeued}")
        return dequeued

    def peek(self):
        if self.is_empty():
            print("Queue is empty. Nothing to peek.")
            return None
        return self.queue[0]

    def size(self):
        return len(self.queue)

    def display(self):
        print("Queue:", self.queue)

if __name__ == "__main__":
    q = Queue()
    q.enqueue(10)
    q.enqueue(20)
    q.enqueue(30)
    q.display()
    print("Front element is:", q.peek())
    q.dequeue()
    q.display()
    print("Queue size:", q.size())
```

</details>

<details>
<summary>3️⃣ Linked List Implementation</summary>

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            print(f"Appended: {data} as head")
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node
        print(f"Appended: {data}")

    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        print(f"Prepended: {data}")

    def delete(self, key):
        current = self.head

        if current and current.data == key:
            self.head = current.next
            print(f"Deleted head node: {key}")
            return

        prev = None
        while current and current.data != key:
            prev = current
            current = current.next

        if not current:
            print(f"Value {key} not found in the list.")
            return

        prev.next = current.next
        print(f"Deleted: {key}")

    def display(self):
        current = self.head
        if not current:
            print("Linked list is empty.")
            return
        print("Linked List:", end=" ")
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

if __name__ == "__main__":
    ll = LinkedList()
    ll.append(10)
    ll.append(20)
    ll.append(30)
    ll.display()
    ll.prepend(5)
    ll.display()
    ll.delete(20)
    ll.display()
```

</details>
