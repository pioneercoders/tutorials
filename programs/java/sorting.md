<details open>
<summary>Write a programs for BubbleSort.</summary>
<p>

```java
public class BubbleSort {
    public static void sort(Integer[] array) {
        for (int i = 0; i < array.length - 1; i++) {
            for (int j = 1; j < array.length - i; j++) {
                if (array[j - 1] > array[j]) {
                    swap(array, j, j - 1);
                }
            }
        }
    }

    private static void swap(Integer[] array, int a, int b) {
        Integer temp = array[a];
        array[a] = array[b];
        array[b] = temp;
    }
    public static void main(String args[]) {
        int arr[] = {15,12,3,14,5}
        sort(array);
    }
} 
```

</p>
</details>

<details>
<summary>Write a programs for MergeSort.</summary>
<p>

```java
public class MergeSort {
    
    public static Integer[] sort(Integer[] array) {
        if (array.length <= 1)
            return array;

        int middle = array.length / 2;
        Integer[] left = new Integer[middle];
        Integer[] right = new Integer[array.length - middle];

        for (int i = 0; i < left.length; i++) {
            left[i] = array[i];
        }
        for (int i = 0; i < right.length; i++) {
            right[i] = array[i + left.length];
        }

        left = sort(left);
        right = sort(right);

        return merge(left, right);
    }

    public static Integer[] merge(Integer[] left, Integer[] right) {
        Integer[] result = new Integer[left.length + right.length];
        int leftIndex = 0;
        int rightIndex = 0;
        int resultIndex = 0;
        while (leftIndex < left.length || rightIndex < right.length) {
            if (leftIndex < left.length && rightIndex < right.length) {
                if (left[leftIndex] <= right[rightIndex]) {
                    result[resultIndex++] = left[leftIndex++];
                } else {
                    result[resultIndex++] = right[rightIndex++];
                }
            } else if (leftIndex < left.length) {
                result[resultIndex++] = left[leftIndex++];
            } else if (rightIndex < right.length) {
                result[resultIndex++] = right[rightIndex++];
            }
        }
        return result;
    }
    
    public static void main(String args[]) {
        int arr[] = {15,12,3,14,5}
        sort(array);
    }
}
```

</p>
</details>
