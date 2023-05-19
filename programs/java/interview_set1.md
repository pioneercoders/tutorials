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
