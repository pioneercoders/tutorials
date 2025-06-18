<details open>
<summary>1️⃣ Write a program to check if a number is an Armstrong number.</summary>

```java
import java.util.Scanner;

public class ArmstrongNumber {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number to check if it's an Armstrong number: ");
        int number = scanner.nextInt();
        scanner.close();
        checkArmstrong(number);
    }

    private static void checkArmstrong(int n) {
        int sum = 0, temp = n;
        while (n != 0) {
            int digit = n % 10;
            sum += digit * digit * digit;
            n /= 10;
        }

        if (temp == sum) {
            System.out.println(temp + " is an Armstrong number.");
        } else {
            System.out.println(temp + " is not an Armstrong number.");
        }
    }
}
```

</details>

<details>
<summary>2️⃣ Write a program to find the factorial of a given number.</summary>

```java
import java.util.Scanner;

public class Factorial {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number to find factorial: ");
        int number = scanner.nextInt();
        scanner.close();
        findFactorial(number);
    }

    private static void findFactorial(int num) {
        int result = 1;
        for (int i = 1; i <= num; i++) {
            result *= i;
        }
        System.out.println("Factorial of " + num + " is: " + result);
    }
}
```

</details>

<details>
<summary>3️⃣ Write a program to check if a number is a Palindrome.</summary>

```java
import java.util.Scanner;

public class Palindrome {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number to check if it's a palindrome: ");
        int number = scanner.nextInt();
        scanner.close();
        checkPalindrome(number);
    }

    private static void checkPalindrome(int n) {
        int temp = n, reverse = 0;
        while (n > 0) {
            int digit = n % 10;
            reverse = reverse * 10 + digit;
            n /= 10;
        }

        if (temp == reverse) {
            System.out.println(temp + " is a palindrome.");
        } else {
            System.out.println(temp + " is not a palindrome.");
        }
    }
}
```

</details>

<details>
<summary>4️⃣ Write a program to print a star pattern.</summary>

```java
import java.util.Scanner;

public class StarPattern {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter number of rows for the star pattern: ");
        int n = scanner.nextInt();
        scanner.close();

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```

</details>

<details>
<summary>5️⃣ Write a program to check if a number is Prime.</summary>

```java
import java.util.Scanner;

public class PrimeNumber {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number to check if it's prime: ");
        int num = scanner.nextInt();
        scanner.close();

        if (isPrime(num)) {
            System.out.println(num + " is a prime number.");
        } else {
            System.out.println(num + " is not a prime number.");
        }
    }

    private static boolean isPrime(int num) {
        if (num <= 1) return false;
        for (int i = 2; i <= num / 2; i++) {
            if (num % i == 0) return false;
        }
        return true;
    }
}
```

</details>

<details>
<summary>6️⃣ Write a program to print the Fibonacci series up to N terms.</summary>

```java
import java.util.Scanner;

public class FibonacciSeries {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter number of terms for Fibonacci series: ");
        int n = scanner.nextInt();
        scanner.close();
        
        printFibonacci(n);
    }

    private static void printFibonacci(int n) {
        int a = 0, b = 1;
        System.out.print("Fibonacci Series: " + a);
        if (n > 1) System.out.print(" " + b);

        for (int i = 2; i < n; i++) {
            int next = a + b;
            System.out.print(" " + next);
            a = b;
            b = next;
        }
        System.out.println();
    }
}
```

</details>
