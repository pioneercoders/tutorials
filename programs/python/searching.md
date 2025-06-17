<details open>
<summary>1️⃣ Linear Search</summary>

```python
def linear_search(arr, target):
    print(f"Searching for {target} in {arr}")
    
    for i in range(len(arr)):
        print(f"Checking index {i}, value {arr[i]}")
        if arr[i] == target:
            print(f"✅ Found {target} at index {i}")
            return i

    print(f"❌ {target} not found in the array.")
    return -1

# Example usage
if __name__ == "__main__":
    data = [5, 3, 7, 1, 9, 2]
    key = 7
    linear_search(data, key)
```

</details>

<details>
<summary>2️⃣ Binary Search (on sorted array)</summary>

```python
def binary_search(arr, target):
    low = 0
    high = len(arr) - 1
    print(f"Searching for {target} in {arr}")
    
    while low <= high:
        mid = (low + high) // 2
        print(f"Checking middle index {mid}, value {arr[mid]}")
        
        if arr[mid] == target:
            print(f"✅ Found {target} at index {mid}")
            return mid
        elif arr[mid] < target:
            print(f"{target} > {arr[mid]} → searching right half")
            low = mid + 1
        else:
            print(f"{target} < {arr[mid]} → searching left half")
            high = mid - 1

    print(f"❌ {target} not found in the array.")
    return -1

# Example usage
if __name__ == "__main__":
    data = [1, 3, 5, 7, 9, 11, 13]  # Must be sorted!
    key = 9
    binary_search(data, key)
```

</details>
