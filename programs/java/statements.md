<details open>
<summary>Write a program to find Simple Interst.</summary>
<p>

```java
public class SimpleIntrest {
	public static void main(String[] args) {
		int principle = 20000;
		float rate = 2;
		float time = 5;
		float SI = principle*rate*time/100 ;
		System.out.println("The Simple Interst Is "+SI);
	}
}
```

</p>
</details>

<details>
<summary>Write a program to find Compound Interst.</summary>
<p>

```java
public class CompoundIntrest {
	public static void main(String[] args) {
		int p=2000;
		int t = 5;
		double r=0.08; 
		int n = 12;
		double amount = p * Math.pow(1 + (r / n), n * t);
		double cinterest = amount - p;
		System.out.println("Compound Interest after " + t + " years: "+cinterest);
		System.out.println("Amount after " + t + " years: "+amount);
	}
}
```

</p>
</details>

<details>
<summary>Write a program to find Max between two numbers.</summary>
<p>

```java
public class MaxNumber {
	public static void main(String[] args) {
		int a = 10, b = 20;
		if (a > b) {
			System.out.println(a);
		} else {
			System.out.println(b);
		}
	}
}
```

</p>
</details>

<details>
<summary>Write a program to print given number is even or odd.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int n = 10;
        if(n % 2 == 0){
            System.out.println("Given number is even."); 
        } else {
            System.out.println("Given number is odd."); 
        } 
    }  
}
```

</p>
</details> 

<details>
<summary>Write a program to print given number divisible by 2 and 3.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int n = 6;
        if(n % 2 == 0 && n % 3 == 0){
            System.out.println("Given number is divisible by 2 and 3."); 
        } else {
            System.out.println("Given number is Not divisible by 2 and 3."); 
        } 
    }  
}  
```

</p>
</details> 


<details>
<summary>Write a program to print given number divisible by 3 or 7.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int n = 14;
        if(n % 3 == 0 || n % 7 == 0){
            System.out.println("Given number is divisible by 3 or 7."); 
        } else {
            System.out.println("Given number is Not divisible by 3 or 7."); 
        } 
    }  
}  
```

</p>
</details> 


<details>
<summary>Write a program to print given number divisible by 2 but not with 5.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int n = 14;
        if(n % 2 == 0 && n % 5 != 0){
            System.out.println("Given number is divisible by 2 but not with 5."); 
        } else {
            System.out.println("Given number is divisible by 2 or 5."); 
        } 
    }  
}  
```

</p>
</details> 


