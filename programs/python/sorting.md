<details open>
<summary>1️⃣ Bubble Sort</summary>

```python
def bubble_sort(arr):
    n = len(arr)
    print("Original array:", arr)
    
    for i in range(n):
        swapped = False
        print(f"\nPass {i + 1}:")
        for j in range(0, n - i - 1):
            print(f"  Comparing {arr[j]} and {arr[j + 1]}...", end=" ")
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
                print("swapped!")
            else:
                print("no change.")
        
        print("  Array after this pass:", arr)
        if not swapped:
            print("  No swaps done. Array is sorted.")
            break

    print("\nSorted array:", arr)

# Example usage
if __name__ == "__main__":
    data = [64, 25, 12, 22, 11]
    bubble_sort(data)
```

</details>

<details>
<summary>2️⃣ Merge Sort</summary>

```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]

        print(f"Splitting: {arr}")
        merge_sort(left_half)
        merge_sort(right_half)

        i = j = k = 0

        # Merge the sorted halves
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        # Copy any remaining elements
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

</details>

<details>
<summary>3️⃣ Quick Sort</summary>

```python
def quick_sort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)

        # Recursively sort the two halves
        quick_sort(arr, low, pi - 1)
        quick_sort(arr, pi + 1, high)

def partition(arr, low, high):
    pivot = arr[high]  # Choose the last element as pivot
    i = low - 1

    print(f"\nPartitioning with pivot {pivot} from index {low} to {high}")
    for j in range(low, high):
        print(f"  Comparing {arr[j]} with pivot...", end=" ")
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
            print("swapped.")
        else:
            print("no change.")

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    print(f"  Pivot positioned at index {i + 1}")
    print("  Current array:", arr)
    return i + 1

# Example usage
if __name__ == "__main__":
    data = [10, 7, 8, 9, 1, 5]
    print("Original array:", data)
    quick_sort(data, 0, len(data) - 1)
    print("Sorted array:", data)
```

</details>


<details>
<summary>4️⃣ Insertion Sort</summary>

```python
def insertion_sort(arr):
    print("Original array:", arr)
    
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        print(f"\nInserting {key} into sorted portion...")
        # Move elements greater than key one position ahead
        while j >= 0 and arr[j] > key:
            print(f"  {arr[j]} > {key} → shifting {arr[j]} to the right")
            arr[j + 1] = arr[j]
            j -= 1
        
        arr[j + 1] = key
        print(f"  Inserted {key} at position {j + 1}")
        print("  Array now:", arr)

    print("\nSorted array:", arr)

# Example usage
if __name__ == "__main__":
    data = [9, 5, 1, 4, 3]
    insertion_sort(data)
```

</details>

<details>
<summary>5️⃣ Selection Sort</summary>

```python
def selection_sort(arr):
    print("Original array:", arr)

    n = len(arr)
    for i in range(n):
        min_index = i
        print(f"\nPass {i + 1}:")
        
        # Find index of the minimum element in remaining unsorted array
        for j in range(i + 1, n):
            print(f"  Comparing {arr[min_index]} and {arr[j]}")
            if arr[j] < arr[min_index]:
                min_index = j
                print(f"  → New minimum found: {arr[min_index]} at index {min_index}")
        
        # Swap the found minimum element with the first element of unsorted part
        if min_index != i:
            arr[i], arr[min_index] = arr[min_index], arr[i]
            print(f"  Swapped {arr[min_index]} with {arr[i]}")
        else:
            print("  No swap needed.")

        print("  Array now:", arr)

    print("\nSorted array:", arr)

# Example usage
if __name__ == "__main__":
    data = [64, 25, 12, 22, 11]
    selection_sort(data)
```

</details>

