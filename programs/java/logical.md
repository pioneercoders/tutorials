<details open>
<summary>Write programs to print Armstrong Number .</summary>
<p>

```java
import java.util.Scanner;

public class ArmstrongNumber 
{
	public static void main(String[] args) 
	{
		System.out.println("Enter number to check armstrong or not:");
		Scanner scanner=new Scanner(System.in);
		int number =scanner.nextInt();
	    	armstrong(number);
	}
	private static int armstrong(int n) 
	{
		int sum=0,temp=n;
		while(n!=0)
		{		
		    int	remainder=n%10;
		    sum=sum+remainder*remainder*remainder;
		    n=n/10;
		}
		if(temp==sum)
		{
         	    System.out.println("It is armstrong number" );
		}
		else
		{
		    System.out.println("Not  an armstrong number" );	
		}
		return n;
	}
		
}
```

</p>
</details> 


<details>
<summary>Write programs to print Factorial of given number .</summary>
<p>

```java
import java.util.Scanner;

public class Factorial 
{
	public static void main(String[] args) 
	{
		System.out.println("Enter number to find factorial:");
		Scanner fact = new Scanner(System.in);
		int n=fact.nextInt();
		factorial(n);
	}
	public static int factorial(int num){
		int factorial=1;
		for (int i=1;i<=num;i++)
		{
		    factorial=factorial*i;
		}
		System.out.println("Factorial of given number is:" +factorial);
		return factorial;
		
	}

}
```

</p>
</details> 


<details>
<summary>Write programs to check Palindrome .</summary>
<p>

```java
import java.util.Scanner;

public class Palindrome{
	public static void main(String[] args)
	{
		System.out.println("Enter a number to check palindrome or not:");
		Scanner palindrome=new Scanner(System.in);
	 	int number =palindrome.nextInt();
	  	palindrome(number);
	}
	public static int palindrome(int n)
	{
		int temp=n;
		int remainder=0;
		int reverse=0;
		while(n>0)
		{
		    remainder=n%10;
		    reverse=reverse*10+remainder;
		    n=n/10;
		}
		if (temp==reverse)
		{
		     System.out.println("It is palindrome number");
		}
		else
		{
	             System.out.println("Not a palindrome");
		}
		return reverse;
	}
		
}
```

</p>
</details> 

<details>
<summary>Write programs to print StarPattern.</summary>
<p>

```java
import java.util.Scanner;

public class StarPattern
{
	public static void main(String[] args) 
	{
		Scanner in = new Scanner(System.in);
		int n;
		System.out.println("enter n value");
		n = in.nextInt();
		for (int i = 1; i <= n; i++) 
		{
			for (int j = 1; j <= i; j++) 
			{
				System.out.print("*");
			}
			System.out.println();
		}
	}

}
```

</p>
</details> 
