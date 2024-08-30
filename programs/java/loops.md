<details>
<summary>Write a program to print 1 to 10 numbers?</summary>
<p>

```java
public class PrintNumbers{  
    public static void main(String args[]){  
        for(int i=1; i <= 10; i++){//loop for iterating an list upto 10 numbers
            System.out.println("The numbers are :"+i);
        }
    }  
}  
```

</p>
</details> 

<details> 		
<summary>Write a program to print given number is amstrong.</summary>
<p>

```java
public class Amstrong{  
    public static void main(String args[]){  
        int number , originalNumber= 371, remainder, result = 0;

        number=originalNumber ;//storing the original number in another variable

        while ( number != 0)//checking that number is equal to zero or not
        {
            remainder =  number % 10;//calculating modulus value
            result += Math.pow(remainder, 3);//calculation result
            number /= 10;//performing division
        }

        if(result == originalNumber)//checking whether the given result is equal to original number or not 
            System.out.println(originalNumber + " is an Armstrong number.");//printing if the given number is amstrong 
        else
            System.out.println(originalNumber + " is not an Armstrong number.");//printing if the given number is not an amstrong
    }  
}  
```

</p>
</details> 

<details>
<summary>Write a program to print multiplication table for given number.</summary>
<p>

```java
public class MultiplicationTable{  
    public static void main(String args[]){  
        int num=5;// assume given number is 5
        for(int i=1; i <= 10; i++){//loop for iterating an list upto 10 numbers
            System.out.println(num+" * "+i+" = "+num*i);//performing multiplication and print it out here
        }
    }  
}  
```

</p>
</details> 


<details>
<summary>Write a program to print sum of individual digits for given number.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int m, n, sum = 0;
        m = 456;//stroing the number in m variable
        while(m > 0) {
            n = m % 10;//performing modulo of the number
            sum = sum + n;//calculating sum of individual digits
            m = m / 10;//performing division
        }
        System.out.println("Sum of Digits:"+sum);//printing the sum of individual digits
    }  
}  
```

</p>
</details> 

<details>
<summary>Write a program to print Fibnacci Series.</summary>
<p>

```java
public class FibnacciSeries{  
    public static void main(String args[]){  
        int n1=0,n2=1,n3,i,count=10;    
	System.out.print(n1+" "+n2); //printing first two elements  

	for(i=2;i<count;++i) {    
	  n3=n1+n2;  //adding first two elements and storing another variable  
	  System.out.print(" "+n3);  //printing the sum of first two numbers  
	  n1=n2; //storing n2 in n1
	  n2=n3;  //storing n3 in n2  
	}
    }  
}  
```

</p>
</details> 

<details>
<summary>Write a program to print Pascal Triangle.</summary>
<p>

```java
public class PascalTriangle{  
    public static void main(String args[]){  
       	int r, i, k, number=1, j;
	r = 4;//stroing the number of rows in r variable

	for(i=0;i<r;i++) {
		for(k=r; k>i; k--) {
			System.out.print(" ");//printin empty other than the elements in the traingle shape
		}
	number = 1;
		for(j=0;j<=i;j++) {
			 System.out.print(number+ " ");
	 number = number * (i - j) / (j + 1);//printing the elements based on considering the number of rows
		}
		System.out.println();
	}
    }  
}  
```

</p>
</details> 


<details>
<summary>Write a program to find HCF.</summary>
<p>

```java
import java.util.Scanner;
public class HCF{  
    public static void main(String args[]){  
       	int a, b, x, y, t, hcf, lcm;
        Scanner scan = new Scanner(System.in);
		
        System.out.print("Enter Two Number : ");
        x = scan.nextInt();//storing first number in x
        y = scan.nextInt();//storing second number in y
		
        a = x;//stroing x in a
        b = y;//stroing y in b
		
        while(b != 0)//checking b not equal to zero
        {
            t = b;//then place b value in t
            b = a%b;//perform modulo operation
            a = t;//store t value in a
        }
		
        hcf = a;//place a value in hcf
        lcm = (x*y)/hcf;//formula for lcm 
		
        System.out.print("HCF = " +hcf);//print hcf
        System.out.print("\nLCM = " +lcm);//print lcm
        scan.close();//closing the object
    }  
}  
```

</p>
</details>

<details>
<summary>Write the program to print the following series 3 33 333 3333 33333 333333.</summary>
<p>

```java
import java.util.Scanner;
public class PatternSeries {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter the N value for the series : ");
		int N = scanner.nextInt();
		
		int baseValue = 3;
		int result = 0;
		for(int i=0;i<N;i++){
			result = result + baseValue * (int)Math.pow(10, i);
			System.out.print(result+" ");
		}
		
		System.out.print("\nUsing String approach: ");
		//Alternate approach
		String s = "";
		for(int i=0;i<N;i++){
			s += "3";
			System.out.print(s+" ");
		}
		
		scanner.close();
	}
} 
```

</p>
</details> 
	
<details>
<summary>Write the program to print Arithmetic Progression.</summary>
<p>

```java
import java.util.Scanner;
public class ArithmeticProgression {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter the start value of the series : ");
		int a = scanner.nextInt();
		System.out.println("Enter the common ratio : ");
		int d = scanner.nextInt();
		System.out.println("Enter the value (N) for the series : ");
		int N = scanner.nextInt();
	
		//printing the first value
		System.out.print(a+" ");
		for(int i=1;i<=N;i++){
			//current a will denote the previous value
			a = a + d;
			//new value a is calculated for the i-th iteration
			System.out.print(a+" ");
		}
		
		scanner.close();
	}
} 
```

</p>
</details> 

<details>
<summary>Write the program to print Geometric Progression.</summary>
<p>

```java
import java.util.Scanner;
public class GeometricProgression {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter the start value of the series : ");
		int a = scanner.nextInt();
		System.out.println("Enter the common ratio : ");
		int r = scanner.nextInt();
		System.out.println("Enter the value (N) for the series : ");
		int N = scanner.nextInt();
	
		//printing the first value
		System.out.print(a+" ");
		for(int i=1;i<=N;i++){
			//current a will denote the previous value
			a = a * r;
			//new value a is calculated for the i-th iteration
			System.out.print(a+" ");
		}
		
		scanner.close();
	}
}
```

</p>
</details> 
