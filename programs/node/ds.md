<details open>
<summary>1️⃣ Write a program to implement a Stack in JavaScript.</summary>
<p>

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  // Add element to the stack
  push(element) {
    this.items[this.items.length] = element;
  }

  // Remove and return top element
  pop() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    let top = this.items[this.items.length - 1];
    this.items.length = this.items.length - 1;
    return top;
  }

  // Peek the top element
  peek() {
    if (this.isEmpty()) return "Empty Stack";
    return this.items[this.items.length - 1];
  }

  // Stack size
  size() {
    return this.items.length;
  }

  // Check if stack is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Print stack
  print() {
    let str = "";
    for (let i = 0; i < this.items.length; i++) {
      str += this.items[i] + " ";
    }
    console.log(str.trim());
  }
}

// Usage
const stack = new Stack();
stack.push(10);
stack.push(20);
stack.push(30);
console.log("Top:", stack.peek()); // 30
console.log("Popped:", stack.pop()); // 30
console.log("Size:", stack.size()); // 2
stack.print(); // 10 20
```

</p>
</details>

<details>
<summary>2️⃣ Write a program to implement a Queue in JavaScript.</summary>
<p>

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // Add element to rear
  enqueue(element) {
    this.items[this.items.length] = element;
  }

  // Remove and return front
  dequeue() {
    if (this.isEmpty()) return "Underflow";
    let front = this.items[0];
    for (let i = 0; i < this.items.length - 1; i++) {
      this.items[i] = this.items[i + 1];
    }
    this.items.length = this.items.length - 1;
    return front;
  }

  // Peek front
  front() {
    if (this.isEmpty()) return "Empty Queue";
    return this.items[0];
  }

  // Size of queue
  size() {
    return this.items.length;
  }

  // Check if empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Print queue
  print() {
    let str = "";
    for (let i = 0; i < this.items.length; i++) {
      str += this.items[i] + " ";
    }
    console.log(str.trim());
  }
}

// Usage
const queue = new Queue();
queue.enqueue(5);
queue.enqueue(15);
queue.enqueue(25);
console.log("Front:", queue.front()); // 5
console.log("Dequeued:", queue.dequeue()); // 5
console.log("Size:", queue.size()); // 2
queue.print(); // 15 25
```

</p>
</details>

<details>
<summary>3️⃣ Write a program to implement a Singly Linked List in JavaScript.</summary>
<p>

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  // Add node at end
  append(value) {
    let newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
      return;
    }
    let current = this.head;
    while (current.next !== null) {
      current = current.next;
    }
    current.next = newNode;
  }

  // Print list
  print() {
    let current = this.head;
    let result = "";
    while (current !== null) {
      result += current.value + " -> ";
      current = current.next;
    }
    result += "null";
    console.log(result);
  }

  // Remove a value
  remove(value) {
    if (this.head === null) return;

    if (this.head.value === value) {
      this.head = this.head.next;
      return;
    }

    let current = this.head;
    while (current.next !== null && current.next.value !== value) {
      current = current.next;
    }

    if (current.next !== null) {
      current.next = current.next.next;
    }
  }
}

// Usage
const list = new LinkedList();
list.append(100);
list.append(200);
list.append(300);
list.print(); // 100 -> 200 -> 300 -> null
list.remove(200);
list.print(); // 100 -> 300 -> null
```

</p>
</details>

