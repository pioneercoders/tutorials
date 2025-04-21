<details open>
<summary>Write a programs for BubbleSort.</summary>
<p>

```python
    def bubble_sort(arr):
    n = len(arr)
    print("Original array:", arr)
    
    for i in range(n):
        swapped = False
        print(f"\nPass {i+1}:")
        for j in range(0, n - i - 1):
            print(f"  Comparing {arr[j]} and {arr[j+1]}...", end=" ")
            if arr[j] > arr[j + 1]:
                # Swap if elements are in wrong order
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
                print("swapped!")
            else:
                print("no change.")
        
        print("  Array after this pass:", arr)
        if not swapped:
            # If no swaps, array is already sorted
            break

    print("\nSorted array:", arr)

# Example usage
if __name__ == "__main__":
    data = [64, 25, 12, 22, 11]
    bubble_sort(data)

```

</p>
</details>

<details >
<summary>Write a programs for MergeSort.</summary>
<p>

```python
  def merge_sort(arr):
    if len(arr) > 1:
        # Split the array
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]

        print(f"Splitting: {arr}")
        merge_sort(left_half)
        merge_sort(right_half)

        # Merging process
        i = j = k = 0

        # Copy data to temp arrays left_half[] and right_half[]
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        # Checking if any element was left
        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1

        print(f"Merging: {arr}")

# Example usage
if __name__ == "__main__":
    data = [38, 27, 43, 3, 9, 82, 10]
    print("Original array:", data)
    merge_sort(data)
    print("Sorted array:", data)
 
```

</p>
</details>

<details >
<summary>Write a programs for QuickSort.</summary>
<p>

```python
   def quick_sort(arr, low, high):
    if low < high:
        # pi is partitioning index
        pi = partition(arr, low, high)

        # Recursively sort elements before and after partition
        quick_sort(arr, low, pi - 1)
        quick_sort(arr, pi + 1, high)

def partition(arr, low, high):
    pivot = arr[high]  # pivot
    i = low - 1         # smaller element index

    for j in range(low, high):
        # If current element is smaller than or equal to pivot
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]  # swap
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Example usage
if __name__ == "__main__":
    data = [10, 7, 8, 9, 1, 5]
    print("Original array:", data)
    quick_sort(data, 0, len(data) - 1)
    print("Sorted array:", data)

```

</p>
</details>
