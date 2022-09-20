<details>
<summary>Print program for Stack implementation.</summary>
<p>

```java
import java.util.*;

public class StackArrays {
	private static final int capacity = 3;  
	 int arr[] = new int[capacity];  
	 int top = -1;  
	  
	 public void push(int pushedElement) {  
	  if (top < capacity - 1) {  
	   top++;  
	   arr[top] = pushedElement;  
	   System.out.println("Element " + pushedElement  
	     + " is pushed to Stack !");  
	   printElements();  
	  } else {  
	   System.out.println("Stack Overflow !");  
	  }  
	 }  
	  
	 public void pop() {  
	  if (top >= 0) {  
	   top--;  
	   System.out.println("Pop operation done !");  
	  } else {  
	   System.out.println("Stack Underflow !");  
	  }  
	 }  
	  
	 public void printElements() {  
	  if (top >= 0) {  
	   System.out.println("Elements in stack :");  
	   for (int i = 0; i <= top; i++) {  
	    System.out.println(arr[i]);  
	   }  
	  }  
	 }  
	  
	 public static void main(String[] args) {  
	StackArrays stackDemo = new StackArrays();  
	  
	  stackDemo.pop();  
	  stackDemo.push(23);  
	  stackDemo.push(2);  
	  stackDemo.push(73);  
	  stackDemo.push(21);  
	  stackDemo.pop();  
	  stackDemo.pop();  
	  
	 }  
	  
}
```

</p>
</details> 


	
<details>
<summary>Print program for Queue implementation.</summary>
<p>

```java
import java.util.*;

 class Queue {
	 protected int Queue[] ;
	    protected int front, rear, size, len;
	 
	    /* Constructor */
	    public Queue(int n) 
	    {
	        size = n;
	        len = 0;
	        Queue = new int[size];
	        front = -1;
	        rear = -1;
	    }    
	    /*  Function to check if queue is empty */
	    public boolean isEmpty() 
	    {
	        return front == -1;
	    }    
	    /*  Function to check if queue is full */
	    public boolean isFull() 
	    {
	        return front==0 && rear == size -1 ;
	    }    
	    /*  Function to get the size of the queue */
	    public int getSize()
	    {
	        return len ;
	    }    
	    /*  Function to check the front element of the queue */
	    public int peek() 
	    {
	        if (isEmpty())
	           throw new NoSuchElementException("Underflow Exception");
	        return Queue[front];
	    }    
	    /*  Function to insert an element to the queue */
	    public void insert(int i) 
	    {
	        if (rear == -1) 
	        {
	            front = 0;
	            rear = 0;
	            Queue[rear] = i;
	        }
	        else if (rear + 1 >= size)
	            throw new IndexOutOfBoundsException("Overflow Exception");
	        else if ( rear + 1 < size)
	            Queue[++rear] = i;    
	        len++ ;    
	    }    
	    /*  Function to remove front element from the queue */
	    public int remove() 
	    {
	        if (isEmpty())
	           throw new NoSuchElementException("Underflow Exception");
	        else 
	        {
	            len-- ;
	            int ele = Queue[front];
	            if ( front == rear) 
	            {
	                front = -1;
	                rear = -1;
	            }
	            else
	                front++;                
	            return ele;
	        }        
	    }
	    /*  Function to display the status of the queue */
	    public void display()
	    {
	        System.out.print("\nQueue = ");
	        if (len == 0)
	        {
	            System.out.print("Empty\n");
	            return ;
	        }
	        for (int i = front; i <= rear; i++)
	            System.out.print(Queue[i]+" ");
	        System.out.println();        
	    }
	}
	 
	/* Class QueueImplement  */
	public class arrayQueue
	{
	    public static void main(String[] args)
	    {
	        Scanner scan = new Scanner(System.in);
	 
	        System.out.println("Array Queue Test\n");
	        System.out.println("Enter Size of Integer Queue ");
	        int n = scan.nextInt();
	        /* creating object of class arrayQueue */
	        Queue q = new Queue(n);        
	        /* Perform Queue Operations */        
	        char ch;
	        do{
	            System.out.println("\nQueue Operations");
	            System.out.println("1. insert");
	            System.out.println("2. remove");
	            System.out.println("3. peek");
	            System.out.println("4. check empty");
	            System.out.println("5. check full");
	            System.out.println("6. size");
	            int choice = scan.nextInt();
	            switch (choice)
	            {
	            case 1 : 
	                System.out.println("Enter integer element to insert");
	                try
	                {
	                    q.insert( scan.nextInt() );
	                }
	                catch(Exception e)
	                {
	                    System.out.println("Error : " +e.getMessage());
	                }                         
	                break;                         
	            case 2 : 
	                try
	                {
	                    System.out.println("Removed Element = "+q.remove());
	                }
	                catch(Exception e)
	                {
	                    System.out.println("Error : " +e.getMessage());
	                }
	                break;                         
	            case 3 : 
	                try
	                {
	                    System.out.println("Peek Element = "+q.peek());
	                }
	                catch(Exception e)
	                {
	                    System.out.println("Error : "+e.getMessage());
	                }
	                break;                            
	            case 4 : 
	                System.out.println("Empty status = "+q.isEmpty());
	                break;                
	            case 5 : 
	                System.out.println("Full status = "+q.isFull());
	                break;                          
	            case 6 : 
	                System.out.println("Size = "+ q.getSize());
	                break;                         
	            default : System.out.println("Wrong Entry \n ");
	                break;
	            }
	            /* display Queue */
	            q.display();            
	            System.out.println("\nDo you want to continue (Type y or n) \n");
	            ch = scan.next().charAt(0);
	 
	        } while (ch == 'Y'|| ch == 'y');                                                        
	    }    
}
```

</p>
</details> 


	
<details>
<summary>Print program for Linked List implementation.</summary>
<p>

```java
public class LinkedList {
	Node head; // head of linked list

	/* Linked list node */
	class Node {
		int data;
		Node next;

		Node(int d) {
			data = d;
			next = null;
		}
	}

	/* Function to print middle of linked list */
	void printMiddle() {
		Node slow_ptr = head;
		Node fast_ptr = head;
		if (head != null) {
			while (fast_ptr != null && fast_ptr.next != null) {
				fast_ptr = fast_ptr.next.next;
				slow_ptr = slow_ptr.next;
			}
			System.out.println("The middle element is [" + slow_ptr.data
					+ "] \n");
		}
	}

	/* Inserts a new Node at front of the list. */
	public void push(int new_data) {
		/*
		 * 1 & 2: Allocate the Node & Put in the data
		 */
		Node new_node = new Node(new_data);

		/* 3. Make next of new Node as head */
		new_node.next = head;

		/* 4. Move the head to point to new Node */
		head = new_node;
	}

	/*
	 * This function prints contents of linked list starting from the given node
	 */
	public void printList() {
		Node tnode = head;
		while (tnode != null) {
			System.out.print(tnode.data + "->");
			tnode = tnode.next;
		}
		System.out.println("NULL");
	}

	public static void main(String[] args) {
		LinkedList llist = new LinkedList();
		for (int i = 5; i > 0; --i) {
			llist.push(i);
			llist.printList();
			llist.printMiddle();
		}
	}
}
```

</p>
</details> 


	
<details>
<summary>Print program for Stort implementation.</summary>
<p>

```java

import java.util.Scanner;

public class SortAnArray {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		 int size, temp;
	        Scanner s = new Scanner(System.in);
	        /*Declaring size of any Array*/
	        
	        System.out.print("Enter the Size of array:");
	        size= s.nextInt();
	        int arr[] = new int[size];
	        /*Enter elements of Array*/
	        
	        System.out.println("Enter all the elements:");
	        for (int i = 0; i < size; i++) {
	            arr[i] = s.nextInt();
	        }
	        /*Accessing each element in an array and sorting using temp variable*/
	        
	        for (int i = 0; i < size; i++) {
	            for (int j = i + 1; j < size; j++) 
	            {
	                if (arr[i] > arr[j]){
	                    temp = arr[i];
	                    arr[i] = arr[j];
	                    arr[j] = temp;
	                }
	            }
	        }
	        /*printing the sorted Array*/
	        
	        System.out.print("Ascending Order:");
	        for (int i = 0; i < size - 1; i++) {
	            System.out.print(arr[i] + ",");
	        }
	        System.out.print(arr[size - 1]);
	    }
	}
```

</p>
</details> 
