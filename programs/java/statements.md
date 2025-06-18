<details open>
<summary>1️⃣ Program to find Simple Interest</summary>
<p>

```java
public class SimpleInterest {
    public static void main(String[] args) {
        int principal = 20000;
        float rate = 2;
        float time = 5;
        float si = (principal * rate * time) / 100;
        System.out.println("Simple Interest: " + si);
    }
}
```

</p>
</details>

<details>
<summary>2️⃣ Program to find Compound Interest</summary>
<p>

```java
public class CompoundInterest {
    public static void main(String[] args) {
        int principal = 2000;
        int time = 5;
        double rate = 0.08;
        int n = 12;

        double amount = principal * Math.pow(1 + (rate / n), n * time);
        double interest = amount - principal;

        System.out.println("Compound Interest after " + time + " years: " + interest);
        System.out.println("Total Amount: " + amount);
    }
}
```

</p>
</details>

<details>
<summary>3️⃣ Program to find Area of a Circle</summary>
<p>

```java
public class CircleArea {
    public static void main(String[] args) {
        int radius = 4;
        double pi = 3.14;
        double area = pi * radius * radius;
        System.out.println("Area of Circle: " + area);
    }
}
```

</p>
</details>

<details>
<summary>4️⃣ Program to find Average of Three Numbers</summary>
<p>

```java
public class AverageOfThree {
    public static void main(String[] args) {
        int num1 = 10, num2 = 20, num3 = 30;
        int average = (num1 + num2 + num3) / 3;
        System.out.println("Average: " + average);
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Program to find Maximum between Two Numbers</summary>
<p>

```java
public class MaxOfTwo {
    public static void main(String[] args) {
        int a = 10, b = 20;
        int max = (a > b) ? a : b;
        System.out.println("Maximum: " + max);
    }
}
```

</p>
</details>

<details>
<summary>6️⃣ Program to find Smallest of Three Numbers</summary>
<p>

```java
public class SmallestNumber {
    public static void main(String[] args) {
        int a = 10, b = 5, c = 20;
        int smallest = a;

        if (b < smallest) smallest = b;
        if (c < smallest) smallest = c;

        System.out.println("Smallest number: " + smallest);
    }
}
```

</p>
</details>

<details>
<summary>7️⃣ Program to Swap Two Numbers</summary>
<p>

```java
public class SwapNumbers {
    public static void main(String[] args) {
        int x = 14, y = 20;
        int temp = x;
        x = y;
        y = temp;
        System.out.println("After Swap - X: " + x + ", Y: " + y);
    }
}
```

</p>
</details>

<details>
<summary>8️⃣ Program to Print Digits of a Number</summary>
<p>

```java
import java.util.Scanner;

public class DigitsOfNumber {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter any positive integer: ");
        int num = scanner.nextInt();
        System.out.print("Digits: ");
        String str = Integer.toString(num);
        for (int i = 0; i < str.length(); i++) {
            System.out.print(str.charAt(i) + " ");
        }
        scanner.close();
    }
}
```

</p>
</details>

<details>
<summary>9️⃣ Program to Check Even or Odd</summary>
<p>

```java
public class EvenOrOdd {
    public static void main(String[] args) {
        int n = 10;
        if (n % 2 == 0)
            System.out.println(n + " is Even");
        else
            System.out.println(n + " is Odd");
    }
}
```

</p>
</details>

<details>
<summary>🔟 Program to Check if Number is Divisible by 2 and 3</summary>
<p>

```java
public class DivisibleBy2And3 {
    public static void main(String[] args) {
        int n = 6;
        if (n % 2 == 0 && n % 3 == 0)
            System.out.println(n + " is divisible by both 2 and 3");
        else
            System.out.println(n + " is NOT divisible by both 2 and 3");
    }
}
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Program to Check if Number is Divisible by 3 or 7</summary>
<p>

```java
public class DivisibleBy3Or7 {
    public static void main(String[] args) {
        int n = 14;
        if (n % 3 == 0 || n % 7 == 0)
            System.out.println(n + " is divisible by 3 or 7");
        else
            System.out.println(n + " is NOT divisible by 3 or 7");
    }
}
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Program to Check if Number is Divisible by 2 but Not by 5</summary>
<p>

```java
public class DivisibleBy2Not5 {
    public static void main(String[] args) {
        int n = 14;
        if (n % 2 == 0 && n % 5 != 0)
            System.out.println(n + " is divisible by 2 but not by 5");
        else
            System.out.println(n + " is either not divisible by 2 or divisible by 5");
    }
}
```

</p>
</details>

<details>
<summary>1️⃣3️⃣ Program to Find LCM (Least Common Multiple)</summary>
<p>

```java
public class LCM {
    public static void main(String[] args) {
        int a = 5, b = 7;
        int lcm = (a > b) ? a : b;

        while (true) {
            if (lcm % a == 0 && lcm % b == 0) {
                System.out.println("LCM of " + a + " and " + b + " is " + lcm);
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
<summary>1️⃣4️⃣ Program to Check Perfect Number</summary>
<p>

```java
import java.util.Scanner;

public class PerfectNumber {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a positive integer: ");
        int num = scanner.nextInt();
        int sum = 0;

        for (int i = 1; i <= num / 2; i++) {
            if (num % i == 0)
                sum += i;
        }

        if (sum == num)
            System.out.println(num + " is a Perfect Number");
        else
            System.out.println(num + " is NOT a Perfect Number");

        scanner.close();
    }
}
```

</p>
</details>

<details>
<summary>1️⃣5️⃣ Program for Temperature Converter</summary>
<p>

```java
import java.util.Scanner;

public class TemperatureConverter {
    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        System.out.print("Input type (F/C/K): ");
        char inputType = reader.next().toUpperCase().charAt(0);
        System.out.print("Output type (F/C/K): ");
        char outputType = reader.next().toUpperCase().charAt(0);
        System.out.print("Temperature: ");
        float temp = reader.nextFloat();

        float celsius = toCelsius(temp, inputType);
        float result = fromCelsius(celsius, outputType);

        System.out.println("Converted Temperature: " + result);
        reader.close();
    }

    public static float toCelsius(float t, char type) {
        switch (type) {
            case 'F': return (t - 32) * 5 / 9;
            case 'K': return t - 273.15f;
            default: return t;
        }
    }

    public static float fromCelsius(float t, char type) {
        switch (type) {
            case 'F': return (t * 9 / 5) + 32;
            case 'K': return t + 273.15f;
            default: return t;
        }
    }
}
```

</p>
</details>
