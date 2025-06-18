<details open>
<summary>1️⃣ Program to Demonstrate Arithmetic Operators</summary>
<p>

```java
import java.util.Scanner;

public class ArithmeticOperators {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the first number: ");
        double num1 = scanner.nextDouble();

        System.out.print("Enter the second number: ");
        double num2 = scanner.nextDouble();
        scanner.close();

        System.out.println("\n🔢 Arithmetic Operations:");
        System.out.println("Addition        : " + (num1 + num2));
        System.out.println("Subtraction     : " + (num1 - num2));
        System.out.println("Multiplication  : " + (num1 * num2));
        System.out.println("Division        : " + (num2 != 0 ? (num1 / num2) : "Undefined (division by zero)"));
        System.out.println("Modulus         : " + (num2 != 0 ? (num1 % num2) : "Undefined (mod by zero)"));
    }
}
```

</p>
</details>


<details>
<summary>2️⃣ Program to Demonstrate Relational Operators</summary>
<p>

```java
import java.util.Scanner;

public class RelationalOperators {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter first integer: ");
        int num1 = scanner.nextInt();

        System.out.print("Enter second integer: ");
        int num2 = scanner.nextInt();
        scanner.close();

        System.out.println("\n📏 Relational Operations:");
        System.out.println("num1 > num2   : " + (num1 > num2));
        System.out.println("num1 < num2   : " + (num1 < num2));
        System.out.println("num1 >= num2  : " + (num1 >= num2));
        System.out.println("num1 <= num2  : " + (num1 <= num2));
        System.out.println("num1 == num2  : " + (num1 == num2));
        System.out.println("num1 != num2  : " + (num1 != num2));
    }
}
```

</p>
</details>


<details>
<summary>3️⃣ Program to Demonstrate Logical Operators</summary>
<p>

```java
public class LogicalOperators {
    public static void main(String[] args) {
        boolean a = true;
        boolean b = false;

        System.out.println("🔁 Logical Operations:");
        System.out.println("a         : " + a);
        System.out.println("b         : " + b);
        System.out.println("a && b    : " + (a && b));
        System.out.println("a || b    : " + (a || b));
        System.out.println("!a        : " + (!a));
        System.out.println("!b        : " + (!b));
    }
}
```

</p>
</details>


<details>
<summary>4️⃣ Program to Demonstrate Bitwise Operators</summary>
<p>

```java
public class BitwiseOperators {
    public static void main(String[] args) {
        int a = 5;  // 0101
        int b = 7;  // 0111

        System.out.println("🔧 Bitwise Operations:");
        System.out.println("a & b      : " + (a & b));  // 0101 & 0111 = 0101 (5)
        System.out.println("a | b      : " + (a | b));  // 0101 | 0111 = 0111 (7)
        System.out.println("a ^ b      : " + (a ^ b));  // 0101 ^ 0111 = 0010 (2)
        System.out.println("~a         : " + (~a));     // Inverts all bits

        a &= b; // a = a & b
        System.out.println("a &= b     : " + a);        // Compound AND assignment
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Program to Demonstrate Ternary Operator</summary>
<p>

```java
import java.util.Scanner;

public class TernaryOperator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter first number: ");
        int num1 = scanner.nextInt();

        System.out.print("Enter second number: ");
        int num2 = scanner.nextInt();
        scanner.close();

        // Ternary operator to find the maximum
        int max = (num1 > num2) ? num1 : num2;

        System.out.println("\n📌 Using Ternary Operator:");
        System.out.println("The greater number is: " + max);

        // Example with boolean condition
        String result = (num1 == num2) ? "Both numbers are equal" : "Numbers are not equal";
        System.out.println(result);
    }
}
```

</p>
</details>
