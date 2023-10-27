<details open>
<summary>Write a program to print Arithmetic Operators:</summary>
<p>

```java
import java.util.Scanner;

public class ArithmeticOperators {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		System.out.print("Enter the first number: ");
		double num1 = sc.nextDouble();

		System.out.print("Enter the second number: ");
		double num2 = sc.nextDouble();

		double sum = num1 + num2;
		double difference = num1 - num2;
		double product = num1 * num2;
		double quotient = num1 / num2;

		System.out.println("The sum of the two numbers is: " + sum);
		System.out.println("The difference of the two numbers is: " + difference);
		System.out.println("The product of the two numbers is: " + product);
		System.out.println("The quotient of the two numbers is: " + quotient);
	}
} 
```

</p>
</details>

<details open>
<summary>Write a program to print Relational Operators:</summary>
<p>
	
```java
import java.util.Scanner;

public class RelationalOperators {
  public static void main(String[] args) {
   Scanner scan = new Scanner(System.in);
     
   //System.out.println("Enter first number: ");
   // int num1 = scan.nextInt();
     
   // System.out.println("Enter second number: ");
   // int num2 = scan.nextInt();
     
   int num1 =1;
   int num2 = 2;
     
     
   System.out.println("num1 > num2 is " + (num1 > num2));
   System.out.println("num1 < num2 is " + (num1 < num2));
   System.out.println("num1 >= num2 is " + (num1 >= num2));
   System.out.println("num1 <= num2 is " + (num1 <= num2));
   System.out.println("num1 == num2 is " + (num1 == num2));
   System.out.println("num1 != num2 is " + (num1 != num2));
  }
}
```
</p>
</details>

<details>
<summary>Write a program to print Logiacal Operators</summary>
<p>
	
```java
import java.io.*;

public class LogicalOperators {
  public static void main(String[] args) {
	boolean a = true;
	boolean b = false;

	System.out.println("a: " + a);
	System.out.println("b: " + b);
	System.out.println("a && b: " + (a && b));
	System.out.println("a || b: " + (a || b));
	System.out.println("!a: " + !a);
	System.out.println("!b: " + !b);
	}
}
```
</p>
</details>

<details>
<summary>Write a program to print Bitwise Operators</summary>
<p>
	
```java
import java.util.Scanner;
   public class operators {
     public static void main(String[] args)
	{
	// Initial values
	int a = 5;
	int b = 7;

	// bitwise and
	// 0101 & 0111=0101 = 5
	System.out.println("a&b = " + (a & b));

	// bitwise or
	// 0101 | 0111=0111 = 7
	System.out.println("a|b = " + (a | b));

	// bitwise xor
	// 0101 ^ 0111=0010 = 2
	System.out.println("a^b = " + (a ^ b));

	// bitwise not
	// ~00000000 00000000 00000000 00000101=11111111 11111111 11111111 11111010
	// will give 2's complement (32 bit) of 5 = -6
	System.out.println("~a = " + ~a);

	// can also be combined with
	// assignment operator to provide shorthand
	// assignment
	// a=a&b
	a &= b;
		System.out.println("a= " + a);
	}
}
```
</p>
</details>
