<details open>
<summary>Write a program for leaner search implementation.</summary>
<p>

```java
public class LinearSearch {

    public static int search(int[] list, int search) {
        int length = list.length;
        for (int index = 0; index < length; index++) {
            if (list[index] == search) {
                return index;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        System.out.print("Enter length of list : ");
        Scanner scanner = new Scanner(System.in);

        int length = scanner.nextInt();
        int[] list = new int[length];

        for (int index = 0; index < length; index++) {
            list[index] = scanner.nextInt();
        }

        System.out.print("Enter element to search : ");
        int search = scanner.nextInt();
        int elementAt = search(list, search);

        String result = elementAt == -1 ? "Element not found." : "Element is at index " + elementAt;
        System.out.println(result);
    }
} 
```

</p>
</details>


<details>
<summary>Write a programs for Binary Search.</summary>
<p>

```java
    public static boolean binarySearchRecursive(int[] array, int key, int start, int end) {
        int middle = (start + end) / 2;

        if (end < start) {
            return false;
        }

        if (key < array[middle]) {
            return binarySearchRecursive(array, key, start, middle - 1);
        } else if (key > array[middle]) {
            return binarySearchRecursive(array, key, middle + 1, end);
        } else if (key == array[middle]) {
            return true;
        }

        return false;
    }

    public static boolean binarySearchIterative(int[] array, int key) {
        int start = 0;
        int end = array.length - 1;

        while (start <= end) {
            int middle = (start + end) / 2;

            if (key < array[middle]) {
                end = middle - 1;
            } else if (key > array[middle]) {
                start = middle + 1;
            } else if (key == array[middle]) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int[] array = { 1, 8, 34, 67, 9, 6, 78, 12, 56, 41, 90 };
        int key1 = 12, key2 = 91;
        Arrays.sort(array);

        System.out.println("Array :");
        System.out.println(Arrays.toString(array));

        System.out.println();
        System.out.println("Using binary search iterative : ");
        System.out.println(binarySearchIterative(array, key1) ? key1 + " Found" : key1 + " Not found");
        System.out.println(binarySearchIterative(array, key2) ? key2 + " Found" : key2 + " Not found");

        System.out.println();
        System.out.println("Using binary search recursive : ");
        System.out.println(
                binarySearchRecursive(array, key1, 0, array.length - 1) ? key1 + " Found" : key1 + " Not found");
        System.out.println(
                binarySearchRecursive(array, key2, 0, array.length - 1) ? key2 + " Found" : key2 + " Not found");
    } 
```

</p>
</details>
