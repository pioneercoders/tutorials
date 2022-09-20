
<details open>
<summary>Write a program to print multiplication table for given number.</summary>
<p>

```java
public class App{  
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
<summary>Write a program to print given number is amstrong.</summary>
<p>

```java
public class App{  
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
