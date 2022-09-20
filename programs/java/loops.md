
<details open>
<summary>Write a program to print multiplication table for given number.</summary>
<p>

```java
class App{  
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
class App{  
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
