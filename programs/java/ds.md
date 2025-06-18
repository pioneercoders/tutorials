<details open>
<summary>1️⃣ Stack Implementation using Array</summary>
<p>

```java
public class StackArray {
    private static final int CAPACITY = 3;
    private int[] stack = new int[CAPACITY];
    private int top = -1;

    public void push(int element) {
        if (top < CAPACITY - 1) {
            stack[++top] = element;
            System.out.println("Pushed: " + element);
            printStack();
        } else {
            System.out.println("Stack Overflow!");
        }
    }

    public void pop() {
        if (top >= 0) {
            System.out.println("Popped: " + stack[top--]);
        } else {
            System.out.println("Stack Underflow!");
        }
    }

    public void printStack() {
        if (top >= 0) {
            System.out.println("Stack Elements:");
            for (int i = 0; i <= top; i++) {
                System.out.println(stack[i]);
            }
        } else {
            System.out.println("Stack is empty.");
        }
    }

    public static void main(String[] args) {
        StackArray stack = new StackArray();
        stack.pop();
        stack.push(10);
        stack.push(20);
        stack.push(30);
        stack.push(40);
        stack.pop();
        stack.pop();
    }
}
```

</p>
</details>

<details>
<summary>2️⃣ Queue Implementation using Array</summary>
<p>

```java
import java.util.*;

class ArrayQueue {
    private int[] queue;
    private int front, rear, size, capacity;

    public ArrayQueue(int capacity) {
        this.capacity = capacity;
        queue = new int[capacity];
        front = rear = -1;
        size = 0;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public int peek() {
        if (isEmpty()) throw new NoSuchElementException("Queue Underflow");
        return queue[front];
    }

    public void enqueue(int element) {
        if (isFull()) throw new IllegalStateException("Queue Overflow");
        if (rear == -1) {
            front = rear = 0;
        } else {
            rear++;
        }
        queue[rear] = element;
        size++;
    }

    public int dequeue() {
        if (isEmpty()) throw new NoSuchElementException("Queue Underflow");
        int removed = queue[front];
        if (front == rear) {
            front = rear = -1;
        } else {
            front++;
        }
        size--;
        return removed;
    }

    public int getSize() {
        return size;
    }

    public void display() {
        System.out.print("Queue: ");
        if (isEmpty()) {
            System.out.println("Empty");
        } else {
            for (int i = front; i <= rear; i++) {
                System.out.print(queue[i] + " ");
            }
            System.out.println();
        }
    }
}

public class QueueDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter size of queue: ");
        int n = scanner.nextInt();
        ArrayQueue q = new ArrayQueue(n);

        char ch;
        do {
            System.out.println("\nQueue Operations:");
            System.out.println("1. Enqueue");
            System.out.println("2. Dequeue");
            System.out.println("3. Peek");
            System.out.println("4. Is Empty?");
            System.out.println("5. Is Full?");
            System.out.println("6. Size");

            int choice = scanner.nextInt();
            try {
                switch (choice) {
                    case 1:
                        System.out.print("Enter element to enqueue: ");
                        q.enqueue(scanner.nextInt());
                        break;
                    case 2:
                        System.out.println("Dequeued: " + q.dequeue());
                        break;
                    case 3:
                        System.out.println("Front: " + q.peek());
                        break;
                    case 4:
                        System.out.println("Is Empty: " + q.isEmpty());
                        break;
                    case 5:
                        System.out.println("Is Full: " + q.isFull());
                        break;
                    case 6:
                        System.out.println("Size: " + q.getSize());
                        break;
                    default:
                        System.out.println("Invalid choice.");
                }
            } catch (Exception e) {
                System.out.println("Error: " + e.getMessage());
            }

            q.display();
            System.out.print("Continue? (y/n): ");
            ch = scanner.next().charAt(0);

        } while (ch == 'y' || ch == 'Y');
        scanner.close();
    }
}
```

</p>
</details>

<details>
<summary>3️⃣ Singly Linked List Implementation</summary>
<p>

```java
public class SinglyLinkedList {
    Node head;

    class Node {
        int data;
        Node next;
        Node(int d) {
            data = d;
        }
    }

    public void push(int newData) {
        Node newNode = new Node(newData);
        newNode.next = head;
        head = newNode;
    }

    public void printList() {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " -> ");
            curr = curr.next;
        }
        System.out.println("NULL");
    }

    public void printMiddle() {
        Node slow = head, fast = head;
        if (head != null) {
            while (fast != null && fast.next != null) {
                slow = slow.next;
                fast = fast.next.next;
            }
            System.out.println("Middle element: " + slow.data);
        }
    }

    public static void main(String[] args) {
        SinglyLinkedList list = new SinglyLinkedList();
        for (int i = 5; i > 0; i--) {
            list.push(i);
            list.printList();
            list.printMiddle();
        }
    }
}
```

</p>
</details>
