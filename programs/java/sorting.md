<details open>
<summary>1️⃣ Bubble Sort</summary>
<p>

```java
public class BubbleSort {

    public static void sort(int[] array) {
        int n = array.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 1; j < n - i; j++) {
                if (array[j - 1] > array[j]) {
                    swap(array, j - 1, j);
                    swapped = true;
                }
            }
            if (!swapped) break; // Optimization: stop if already sorted
        }
    }

    private static void swap(int[] array, int a, int b) {
        int temp = array[a];
        array[a] = array[b];
        array[b] = temp;
    }

    private static void printArray(int[] array) {
        for (int val : array) {
            System.out.print(val + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {15, 12, 3, 14, 5};
        System.out.println("Original Array:");
        printArray(arr);

        sort(arr);

        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```

</p>
</details>

<details>
<summary>2️⃣ Merge Sort</summary>
<p>

```java
public class MergeSort {

    public static int[] sort(int[] array) {
        if (array.length <= 1) return array;

        int mid = array.length / 2;
        int[] left = new int[mid];
        int[] right = new int[array.length - mid];

        for (int i = 0; i < mid; i++) left[i] = array[i];
        for (int i = 0; i < right.length; i++) right[i] = array[mid + i];

        return merge(sort(left), sort(right));
    }

    private static int[] merge(int[] left, int[] right) {
        int[] merged = new int[left.length + right.length];
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            merged[k++] = (left[i] <= right[j]) ? left[i++] : right[j++];
        }

        while (i < left.length) merged[k++] = left[i++];
        while (j < right.length) merged[k++] = right[j++];

        return merged;
    }

    private static void printArray(int[] array) {
        for (int val : array) System.out.print(val + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {15, 12, 3, 14, 5};
        System.out.println("Original Array:");
        printArray(arr);

        arr = sort(arr);

        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```

</p>
</details>

<details>
<summary>3️⃣ Quick Sort</summary>
<p>

```java
public class QuickSort {

    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pivotIndex = partition(arr, low, high);
            quickSort(arr, low, pivotIndex - 1);
            quickSort(arr, pivotIndex + 1, high);
        }
    }

    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        swap(arr, i + 1, high);
        return i + 1;
    }

    private static void swap(int[] arr, int a, int b) {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }

    private static void printArray(int[] arr) {
        for (int num : arr) System.out.print(num + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {9, 7, 5, 11, 12, 2, 14, 3, 10, 6};
        System.out.println("Original Array:");
        printArray(arr);

        quickSort(arr, 0, arr.length - 1);

        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```

</p>
</details>

<details>
<summary>4️⃣ Insertion Sort</summary>
<p>

```java
public class InsertionSort {

    public static void sort(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            int key = arr[i];
            int j = i - 1;

            // Shift elements greater than key to the right
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = key;
        }
    }

    private static void printArray(int[] arr) {
        for (int val : arr) System.out.print(val + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {15, 12, 3, 14, 5};
        System.out.println("Original Array:");
        printArray(arr);

        sort(arr);

        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Selection Sort</summary>
<p>

```java
public class SelectionSort {

    public static void sort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            int minIdx = i;

            // Find the index of the minimum element in the unsorted part
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }

            // Swap if a smaller element was found
            if (minIdx != i) {
                int temp = arr[minIdx];
                arr[minIdx] = arr[i];
                arr[i] = temp;
            }
        }
    }

    private static void printArray(int[] arr) {
        for (int val : arr) System.out.print(val + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {15, 12, 3, 14, 5};
        System.out.println("Original Array:");
        printArray(arr);

        sort(arr);

        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```

</p>
</details>
