<details open>
<summary>1️⃣ Write a program to print numbers from 1 to 10</summary>

```java
public class PrintNumbers {
    public static void main(String[] args) {
        for (int i = 1; i <= 10; i++) {
            System.out.println("The numbers are: " + i);
        }
    }
}
```

</details>

<details>
<summary>2️⃣ Write a program to print odd numbers till the given number</summary>

```java
import java.util.Scanner;

public class PrintOddNumbers {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        System.out.println("Odd numbers up to " + number + ":");
        for (int i = 1; i <= number; i++) {
            if (i % 2 != 0) {
                System.out.println(i);
            }
        }
        scanner.close();
    }
}
```

</details>

<details>
<summary>3️⃣ Write a program to print even numbers till the given number</summary>

```java
import java.util.Scanner;

public class PrintEvenNumbers {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        System.out.println("Even numbers up to " + number + ":");
        for (int i = 1; i <= number; i++) {
            if (i % 2 == 0) {
                System.out.println(i);
            }
        }
        scanner.close();
    }
}
```

</details>

<details>
<summary>4️⃣ Print numbers from 1 to a given number using while loop</summary>

```java
import java.util.Scanner;

public class PrintNumbersWhile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        int i = 1;
        System.out.println("Numbers from 1 to " + number + ":");
        while (i <= number) {
            System.out.println(i);
            i++;
        }
        scanner.close();
    }
}
```

</details>

<details>
<summary>5️⃣ Print even numbers using while loop</summary>

```java
import java.util.Scanner;

public class PrintEvenNumbersWhile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        int i = 1;
        System.out.println("Even numbers up to " + number + ":");
        while (i <= number) {
            if (i % 2 == 0) {
                System.out.println(i);
            }
            i++;
        }
        scanner.close();
    }
}
```

</details>

<details>
<summary>6️⃣ Print odd numbers using while loop</summary>

```java
import java.util.Scanner;

public class PrintOddNumbersWhile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        int i = 1;
        System.out.println("Odd numbers up to " + number + ":");
        while (i <= number) {
            if (i % 2 != 0) {
                System.out.println(i);
            }
            i++;
        }
        scanner.close();
    }
}
```

</details>

<details>
<summary>7️⃣ Print numbers using do-while loop</summary>

```java
import java.util.Scanner;

public class PrintNumbersDoWhile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        int i = 1;
        System.out.println("Numbers from 1 to " + number + ":");
        do {
            System.out.println(i);
            i++;
        } while (i <= number);
        scanner.close();
    }
}
```

</details>

<details>
<summary>8️⃣ Print even numbers using do-while loop</summary>

```java
import java.util.Scanner;

public class PrintEvenNumbersDoWhile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        int i = 1;
        System.out.println("Even numbers up to " + number + ":");
        do {
            if (i % 2 == 0) {
                System.out.println(i);
            }
            i++;
        } while (i <= number);
        scanner.close();
    }
}
```

</details>

<details>
<summary>9️⃣ Print odd numbers using do-while loop</summary>

```java
import java.util.Scanner;

public class PrintOddNumbersDoWhile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = scanner.nextInt();
        int i = 1;
        System.out.println("Odd numbers up to " + number + ":");
        do {
            if (i % 2 != 0) {
                System.out.println(i);
            }
            i++;
        } while (i <= number);
        scanner.close();
    }
}
```

</details>

<details>
<summary>🔟 Check if a number is Armstrong</summary>

```java
public class Armstrong {
    public static void main(String[] args) {
        int number = 371, originalNumber = number, remainder, result = 0;
        while (number != 0) {
            remainder = number % 10;
            result += Math.pow(remainder, 3);
            number /= 10;
        }
        if (result == originalNumber)
            System.out.println(originalNumber + " is an Armstrong number.");
        else
            System.out.println(originalNumber + " is not an Armstrong number.");
    }
}
```

</details>

<details>
<summary>1️⃣1️⃣ Print multiplication table for a given number</summary>

```java
public class MultiplicationTable {
    public static void main(String[] args) {
        int num = 5;
        for (int i = 1; i <= 10; i++) {
            System.out.println(num + " * " + i + " = " + num * i);
        }
    }
}
```

</details>

<details>
<summary>1️⃣2️⃣ Sum of digits of a number</summary>

```java
public class SumOfDigits {
    public static void main(String[] args) {
        int m = 456, n, sum = 0;
        while (m > 0) {
            n = m % 10;
            sum += n;
            m /= 10;
        }
        System.out.println("Sum of Digits: " + sum);
    }
}
```

</details>

<details>
<summary>1️⃣3️⃣ Print Fibonacci series</summary>

```java
public class FibonacciSeries {
    public static void main(String[] args) {
        int n1 = 0, n2 = 1, n3, count = 10;
        System.out.print(n1 + " " + n2);
        for (int i = 2; i < count; ++i) {
            n3 = n1 + n2;
            System.out.print(" " + n3);
            n1 = n2;
            n2 = n3;
        }
    }
}
```

</details>

<details>
<summary>1️⃣4️⃣ Print Pascal triangle</summary>

```java
public class PascalTriangle {
    public static void main(String[] args) {
        int r = 4, i, j, k, number;
        for (i = 0; i < r; i++) {
            for (k = r; k > i; k--) {
                System.out.print(" ");
            }
            number = 1;
            for (j = 0; j <= i; j++) {
                System.out.print(number + " ");
                number = number * (i - j) / (j + 1);
            }
            System.out.println();
        }
    }
}
```

</details>

<details>
<summary>1️⃣5️⃣ Find HCF and LCM of two numbers</summary>

```java
import java.util.Scanner;

public class HCF_LCM {
    public static void main(String[] args) {
        int a, b, x, y, t, hcf, lcm;
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter Two Numbers: ");
        x = scan.nextInt();
        y = scan.nextInt();
        a = x;
        b = y;
        while (b != 0) {
            t = b;
            b = a % b;
            a = t;
        }
        hcf = a;
        lcm = (x * y) / hcf;
        System.out.println("HCF = " + hcf);
        System.out.println("LCM = " + lcm);
        scan.close();
    }
}
```

</details>

<details>
<summary>1️⃣6️⃣ Print series: 3 33 333 3333...</summary>

```java
import java.util.Scanner;

public class PatternSeries {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter N: ");
        int N = scanner.nextInt();

        int baseValue = 3;
        int result = 0;
        for (int i = 0; i < N; i++) {
            result = result + baseValue * (int)Math.pow(10, i);
            System.out.print(result + " ");
        }

        System.out.print("\nUsing String approach: ");
        String s = "";
        for (int i = 0; i < N; i++) {
            s += "3";
            System.out.print(s + " ");
        }

        scanner.close();
    }
}
```

</details>

<details>
<summary>1️⃣7️⃣ Print Arithmetic Progression</summary>

```java
import java.util.Scanner;

public class ArithmeticProgression {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter start value: ");
        int a = scanner.nextInt();
        System.out.print("Enter common difference: ");
        int d = scanner.nextInt();
        System.out.print("Enter total terms (N): ");
        int N = scanner.nextInt();

        System.out.print(a + " ");
        for (int i = 1; i < N; i++) {
            a = a + d;
            System.out.print(a + " ");
        }

        scanner.close();
    }
}
```

</details>

<details>
<summary>1️⃣8️⃣ Print Geometric Progression</summary>

```java
import java.util.Scanner;

public class GeometricProgression {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter start value: ");
        int a = scanner.nextInt();
        System.out.print("Enter common ratio: ");
        int r = scanner.nextInt();
        System.out.print("Enter total terms (N): ");
        int N = scanner.nextInt();

        System.out.print(a + " ");
        for (int i = 1; i < N; i++) {
            a = a * r;
            System.out.print(a + " ");
        }

        scanner.close();
    }
}
```

</details>
