<details open>
<summary>1️⃣ Linear Search Implementation</summary>
<p>

```java
import java.util.Scanner;

public class LinearSearch {

    public static int search(int[] array, int key) {
        for (int index = 0; index < array.length; index++) {
            if (array[index] == key) {
                return index;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of elements: ");
        int length = scanner.nextInt();

        int[] array = new int[length];
        System.out.println("Enter " + length + " integers:");

        for (int i = 0; i < length; i++) {
            array[i] = scanner.nextInt();
        }

        System.out.print("Enter element to search: ");
        int key = scanner.nextInt();
        scanner.close();

        int result = search(array, key);
        if (result == -1) {
            System.out.println("Element not found.");
        } else {
            System.out.println("Element found at index: " + result);
        }
    }
}
```

</p>
</details>


<details>
<summary>2️⃣ Binary Search Implementation (Recursive & Iterative)</summary>
<p>

```java
import java.util.Arrays;

public class BinarySearch {

    public static boolean binarySearchRecursive(int[] array, int key, int start, int end) {
        if (start > end) return false;

        int mid = (start + end) / 2;

        if (array[mid] == key) return true;
        if (key < array[mid]) {
            return binarySearchRecursive(array, key, start, mid - 1);
        } else {
            return binarySearchRecursive(array, key, mid + 1, end);
        }
    }

    public static boolean binarySearchIterative(int[] array, int key) {
        int start = 0, end = array.length - 1;

        while (start <= end) {
            int mid = (start + end) / 2;

            if (array[mid] == key) return true;
            if (key < array[mid]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }

        return false;
    }

    public static void main(String[] args) {
        int[] array = { 1, 8, 34, 67, 9, 6, 78, 12, 56, 41, 90 };
        int key1 = 12, key2 = 91;

        Arrays.sort(array);

        System.out.println("Sorted Array:");
        System.out.println(Arrays.toString(array));

        System.out.println("\n🔁 Iterative Binary Search:");
        System.out.println(key1 + (binarySearchIterative(array, key1) ? " Found" : " Not Found"));
        System.out.println(key2 + (binarySearchIterative(array, key2) ? " Found" : " Not Found"));

        System.out.println("\n🔁 Recursive Binary Search:");
        System.out.println(key1 + (binarySearchRecursive(array, key1, 0, array.length - 1) ? " Found" : " Not Found"));
        System.out.println(key2 + (binarySearchRecursive(array, key2, 0, array.length - 1) ? " Found" : " Not Found"));
    }
}
```

</p>
</details>
