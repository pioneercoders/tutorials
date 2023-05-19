<details open>
<summary>write a program that can print the number of prime numbers less than N and you are given a non-negative integer N</summary>
<p>

```java
import java.util.stream.IntStream;

public class Main {
    public static int countPrimes(int N) {
        return (int) IntStream.range(2, N)
                .filter(Main::isPrime)
                .count();
    }

    public static boolean isPrime(int num) {
        if (num < 2) {
            return false;
        }

        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) {
                return false;
            }
        }

        return true;
    }

    public static void main(String[] args) {
        int N = 20;
        int count = countPrimes(N);
        System.out.println("Number of prime numbers less than " + N + ": " + count);
    }
}

```

</p>
</details>


<details>
<summary>Given two binary strings a and b,Write a program to find their sum as a binary string and perform the binary addition operation on these values  </summary>
<p>

```java
public class Main {
    public static String addBinary(String a, String b) {
        int carry = 0; // Initialize carry to 0
        StringBuilder result = new StringBuilder(); // StringBuilder to build the result string

        // Pad the strings with leading zeros if necessary
        int maxLength = Math.max(a.length(), b.length());
        while (a.length() < maxLength)
            a = "0" + a;
        while (b.length() < maxLength)
            b = "0" + b;

        // Perform binary addition
        for (int i = maxLength - 1; i >= 0; i--) {
            int digitA = a.charAt(i) - '0';
            int digitB = b.charAt(i) - '0';
            int sum = digitA + digitB + carry;
            result.insert(0, sum % 2); // Append the result (sum modulo 2) to the left side
            carry = sum / 2; // Determine the carry-over value for the next addition
        }

        // Handle any remaining carry-over
        if (carry > 0)
            result.insert(0, carry);

        return result.toString();
    }

    public static void main(String[] args) {
        String a = "1010";
        String b = "1111";
        String sum = addBinary(a, b);
        System.out.println("Sum: " + sum);
    }
}

```

</p>
</details>
