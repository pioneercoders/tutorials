<details open>
<summary>Write a program to implement stack in javascript.</summary>
<p>

```javascript
    class Stack {
    constructor() {
      this.items = [];
    }
  
    // Push element to the top of the stack
    push(element) {
      this.items.push(element);
    }
  
    // Remove and return the top element from the stack
    pop() {
      if (this.isEmpty()) {
        return "Underflow";
      }
      return this.items.pop();
    }
  
    // Return the top element of the stack without removing it
    peek() {
      if (this.isEmpty()) {
        return "No elements in the stack";
      }
      return this.items[this.items.length - 1];
    }
  
    // Check if the stack is empty
    isEmpty() {
      return this.items.length === 0;
    }
  
    // Return the number of elements in the stack
    size() {
      return this.items.length;
    }
  
    // Print the elements in the stack
    printStack() {
      let stackStr = "";
      for (let i = 0; i < this.items.length; i++) {
        stackStr += this.items[i] + " ";
      }
      console.log(stackStr);
    }
  }
  
  // Example usage
  const stack = new Stack();
  
  console.log(stack.isEmpty()); // Output: true
  
  stack.push(11);
  stack.push(23);
  stack.push(32);
  stack.push(45);
  stack.push(60);
  
  console.log(stack.peek()); // Output: 60
  
  console.log(stack.pop()); // Output: 60
  
  console.log(stack.size()); // Output: 4
  
  console.log(stack.isEmpty()); // Output: false
  
  stack.printStack(); // Output 11 23 32 45
  
```

</p>
</details>
