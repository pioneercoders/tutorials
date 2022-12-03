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
<summary>Write a program to find area of circle.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int radius = 4;
	double pi = 3.14, area;
	area = pi * radius * radius; //formula for calculating radius
	System.out.println("Area of circle:"+area); //printing the value 
    }  
}  
```

</p>
</details> 


<details>
<summary>Write a program to find average of three numbers.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int num1=10, num2=20, num3=30, average;//declaration of variables
	average = ( num1 + num2 + num3 ) / 3;//fromula for calculating the average of given numbers
	System.out.println(" Average : "+average);//printing the average of given numbers
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
<summary>Write a program to find Smallest number.</summary>
<p>

```java
public class FindTheSmallest {
	public static void main(String[] args) {
		int a = 10;
		int b = 5;
		int c = 20;
		
		if(a/b == 0 && a/c == 0)
			System.out.println("a is the smallest");
		else if(b/a == 0 && b/c == 0)
			System.out.println("b is the smallest");
		else
			System.out.println("c is the smallest");
	}
}
```

</p>
</details>

<details>
<summary>Write a program to Swap two numbers.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){  
        int x = 14,y=20;
	int temp=0;
	temp = x;
	x =y;
	y=temp
       	System.out.println("X:"+x+" Y:" +y);
    }  
}  
```

</p>
</details> 

<details>
<summary>Write a program to print Digits of a Given Number.</summary>
<p>

```java
public class DigitsOfNumber {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter any positive integer :: ");
		int num = scanner.nextInt();
		
		ArrayList<Integer> digitsList = new ArrayList<>();
		while(num > 0){
			int unitDigit = num % 10;
			digitsList.add(0, unitDigit);
			num = num/10;
		}
		
		System.out.println("The digits of the Giver Number : ");
		for(int digit : digitsList)
			System.out.print(digit+" ");
		scanner.close();
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

<details>
<summary>Write a program to print LCM - Least Common Multiple.</summary>
<p>

```java
public class LCM {
	public static void main(String[] args) {
		int a = 5;
		int b = 7;
		
		int lcm = (a > b) ? a : b;
		
		while(true){
			if(lcm % a == 0 && lcm % b == 0){
				System.out.println("LCM of "+a+" & "+b+" is "+lcm);
				break;
			}
			lcm++;
		}
	}
}
```

</p>
</details> 

<details>
<summary>Write a program to check Perfect Number.</summary>
<p>

```java
/** Following are the examples of perfect number.
 * 6 = 1+2+3
 * 28= 1+2+4+7+14 
 * 496= 1+2+4+8+16+31+62+124+248
 *  
 **/
public class PerfectNumber {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter any positive integer :: ");
		int num = Integer.parseInt(scanner.nextLine().trim());
		
		if(isPerfectNumber(num))
			System.out.println("Given number : "+num+" is a Perfect Number");
		else
			System.out.println("Given number : "+num+" is NOT a Perfect Number");
		scanner.close();
	}

	private static boolean isPerfectNumber(int num) {
		int tempNum = num;
		int divisorSum = 1;
		for (int i = 2; i <= num / 2; i++)
			if (num % i == 0)
				divisorSum += i;

		if(tempNum == divisorSum)
			return true;
		return false;
	}
}
```

</p>
</details>

<details>
<summary>Write a program for Temperature Converter.</summary>
<p>

```java
import java.util.*;

// F to C: ((t-32.0f)*5.0f)/9.0f
// C to K: t+273.15f
// K to F: (((t-273.15f)*9.0f)/5.0f)+32.0f

public class TemperatureConverter {
    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        char inputType;
        char outputType;
        float inputValue;
        float returnValue;
        
        System.out.print("Input type (F/C/K): ");
        inputType = reader.next().charAt(0);
        System.out.print("Output type (F/C/K): ");
        outputType = reader.next().charAt(0);
        System.out.print("Temperature: ");
        inputValue = reader.nextFloat();
        
        switch(inputType)
        {
            case 'F':
                inputValue = fToC(inputValue);
                break;
            case 'C':
                break;
            case 'K':
                inputValue = fToC(kToF(inputValue));
                break;
            default:
                System.exit(1);
        }
        
        switch(outputType)
        {
            case 'F':
                inputValue = kToF(cToK(inputValue));
                break;
            case 'C':
                break;
            case 'K':
                inputValue = cToK(inputValue);
                break;
            default:
                System.exit(1);
        }
        
        System.out.println(inputValue);
    }
    
    public static float fToC(float fVal)
    {
        return ((fVal-32.0f)*5.0f)/9.0f;
    }
    public static float kToF(float kVal)
    {
        return (((kVal-273.15f)*9.0f)/5.0f)+32.0f;
    }
    public static float cToK(float cVal)
    {
        return cVal+273.15f;
    }
}
```

</p>
</details> 
