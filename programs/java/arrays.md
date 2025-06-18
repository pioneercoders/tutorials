<details open>
<summary>1️⃣ Write a program to print all the elements in array.</summary>

```java
public class PrintElementsInArray {

    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5}; // initialization of elements in an array
        printArr(array);
    }

    private static void printArr(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]); // printing the array elements using for loop
        }
    }
}
```

</details>

<details>
<summary>2️⃣ Write a program to print alternate elements in array.</summary>

```java
import java.util.Scanner;

public class PrintAlternateElementsInArray {

    public static void main(String[] args) {
        int[] arr = createArr();
        printAlternate(arr);
    }

    private static int[] createArr() {
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter the Length of Array: ");
        int count = scan.nextInt();
        int[] a = new int[count];
        for (int i = 0; i < count; i++) {
            System.out.print("Enter number " + (i + 1) + ": ");
            a[i] = scan.nextInt();
        }
        scan.close();
        return a;
    }

    private static void printAlternate(int[] arr) {
        System.out.println("Alternate elements:");
        for (int i = 0; i < arr.length; i += 2) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```

</details>

<details>
<summary>3️⃣ Write a program to print even numbers in array.</summary>

```java
public class PrintEvenNums {

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7, 8};
        printEven(arr);
    }

    private static void printEven(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] % 2 == 0)
                System.out.println(arr[i] + " is Even Number");
        }
    }
}
```

</details>

<details>
<summary>4️⃣ Write a program to print odd numbers in array.</summary>

```java
public class PrintOddNumsArray {

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7, 8};
        printOdd(arr);
    }

    private static void printOdd(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] % 2 != 0)
                System.out.println(arr[i] + " is Odd Number");
        }
    }
}
```

</details>

<details>
<summary>5️⃣ Write a program to print sum and average of array elements.</summary>

```java
import java.util.Scanner;

public class SumAndAvgOfArray {

    public static void main(String[] args) {
        Scanner sr = new Scanner(System.in);
        System.out.print("Enter number of elements in array: ");
        int n = sr.nextInt();
        int[] arr = new int[n];
        int sum = 0;

        System.out.println("Enter all the elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = sr.nextInt();
            sum += arr[i];
        }

        float average = (float) sum / n;
        System.out.println("Sum: " + sum);
        System.out.println("Average: " + average);
    }
}
```

</details>

<details>
<summary>6️⃣ Write a program to print largest element in array.</summary>

```java
import java.util.Scanner;

public class LargestNumInArray {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = scan.nextInt();
        int[] arr = new int[n];

        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = scan.nextInt();
        }

        int max = arr[0];
        for (int i = 1; i < n; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }

        System.out.println("Maximum value: " + max);
    }
}
```

</details>

<details>
<summary>7️⃣ Write a program to print duplicate elements in array.</summary>

```java
public class DuplicateElementsInArray {

    public static void main(String[] args) {
        String[] strArray = {"ramu", "hari", "phani", "phani", "Aparna", "hari", "krishna"};

        for (int i = 0; i < strArray.length - 1; i++) {
            for (int j = i + 1; j < strArray.length; j++) {
                if (strArray[i].equals(strArray[j]) && i != j) {
                    System.out.println("Duplicate Element: " + strArray[j]);
                }
            }
        }
    }
}
```

</details>

<details>
<summary>8️⃣ Write a program to sort elements in array.</summary>

```java
import java.util.Scanner;

public class SortAnArray {

    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.print("Enter size of array: ");
        int n = s.nextInt();
        int[] arr = new int[n];

        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = s.nextInt();
        }

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (arr[i] > arr[j]) {
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }

        System.out.print("Sorted array: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + (i < n - 1 ? ", " : ""));
        }
    }
}
```

</details>

<details>
<summary>9️⃣ Write a program to find the missing number from 1 to N.</summary>

```java
public class FindMissingNo {

    public static void main(String[] args) {
        int[] array = {2, 4, 1, 6, 3};
        int arraySum = 0;
        for (int value : array)
            arraySum += value;

        int n = array.length + 1; // One number is missing
        int expectedSum = n * (n + 1) / 2;

        int missingNumber = expectedSum - arraySum;

        System.out.println("The given array is: ");
        for (int v : array)
            System.out.print(v + " ");
        System.out.println("\nMissing Number is: " + missingNumber);
    }
}
```

</details>

<details>
<summary>🔟 Write a program to move all zeros to the end of array.</summary>

```java
public class MoveAllZerosToEnd {

    public static void main(String[] args) {
        int[] array = {1, 0, 4, 3, 0, 0, 2, 0, 1, 0};
        System.out.println("Original array: ");
        for (int v : array)
            System.out.print(v + " ");

        int count = 0;
        for (int i = 0; i < array.length; i++) {
            if (array[i] != 0) {
                array[count++] = array[i];
            }
        }

        while (count < array.length) {
            array[count++] = 0;
        }

        System.out.println("\nAfter moving all zeros to end: ");
        for (int v : array)
            System.out.print(v + " ");
    }
}
```

</details>

<details>
<summary>1️⃣1️⃣ Write a program to rotate the array d times to the right.</summary>

```java
import java.util.Arrays;

public class ArrayRotation {

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6};
        int d = 2;
        int n = arr.length;

        d = d % n;
        int[] rotated = new int[n];
        int index = 0;

        for (int i = n - d; i < n; i++) {
            rotated[index++] = arr[i];
        }

        for (int i = 0; i < n - d; i++) {
            rotated[index++] = arr[i];
        }

        System.out.println("Original Array:");
        System.out.println(Arrays.toString(arr));
        System.out.println("Array after " + d + " rotations:");
        System.out.println(Arrays.toString(rotated));
    }
}
```

</details>
