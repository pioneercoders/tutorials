<details open>
<summary>1️⃣ Write a program to print all the elements in array.</summary>

```python
# Define the array
arr = [10, 20, 30, 40, 50]

# Print all elements using a loop
print("The elements in the array are:")
for element in arr:
    print(element)
```
</details>

<details>
<summary>2️⃣ Write a program to print alternate elements in array.</summary>

```python
# Define the array
arr = [10, 20, 30, 40, 50, 60, 70]

# Print alternate elements
print("Alternate elements in the array are:")
for i in range(0, len(arr), 2):
    print(arr[i])
```
</details>

<details>
<summary>3️⃣ Write a program to print even numbers in array.</summary>

```python
# Define the array
arr = [5, 8, 13, 22, 36, 41, 50]

# Print even numbers
print("Even numbers in the array are:")
for num in arr:
    if num % 2 == 0:
        print(num)
```
</details>

<details>
<summary>4️⃣ Write a program to print all the odd numbers in array.</summary>

```python
# Define the array
arr = [5, 8, 13, 22, 36, 41, 50]

# Print odd numbers
print("Odd numbers in the array are:")
for num in arr:
    if num % 2 != 0:
        print(num)
```
</details>

<details>
<summary>5️⃣ Write a program to print sum of all the elements in array.</summary>

```python
# Define the array
arr = [10, 20, 30, 40, 50]

# Calculate the sum
total = 0
for num in arr:
    total += num

print("Sum of all the elements is:", total)
```
</details>

<details>
<summary>6️⃣ Write a program to print largest element in array.</summary>

```python
# Define the array
arr = [10, 20, 30, 50, 40]

# Find the largest element
largest = arr[0]
for num in arr:
    if num > largest:
        largest = num

print("The largest element in the array is:", largest)
```
</details>

<details>
<summary>7️⃣ Write a program to print duplicate elements in array.</summary>

```python
# Define the array
arr = [10, 20, 30, 40, 20, 50, 30]

# Track duplicates using a dictionary
seen = {}
duplicates = []

for num in arr:
    if num in seen:
        if seen[num] == 1:
            duplicates.append(num)
        seen[num] += 1
    else:
        seen[num] = 1

# Print duplicates
print("Duplicate elements in the array are:")
for dup in duplicates:
    print(dup)
```
</details>

<details>
<summary>8️⃣ Write a program to sort elements in array.</summary>

```python
# Define the array
arr = [50, 20, 40, 10, 30]

# Sort using bubble sort
n = len(arr)
for i in range(n):
    for j in range(0, n - i - 1):
        if arr[j] > arr[j + 1]:
            arr[j], arr[j + 1] = arr[j + 1], arr[j]

print("Sorted array:", arr)
```
</details>

<details>
<summary>9️⃣ Write a program to find the Missing Number in 1 to N.</summary>

```python
# Define the array
arr = [1, 2, 4, 5, 6]

# Calculate expected sum
n = len(arr) + 1
expected_sum = n * (n + 1) // 2

# Actual sum
actual_sum = 0
for num in arr:
    actual_sum += num

# Missing number
missing = expected_sum - actual_sum
print("The missing number is:", missing)
```
</details>

<details>
<summary>🔟 Write a program to Move All the Zeros to end of the Array.</summary>

```python
# Define the array
arr = [0, 1, 0, 3, 12]

# Move non-zero elements to the front
non_zero_index = 0
for i in range(len(arr)):
    if arr[i] != 0:
        arr[non_zero_index] = arr[i]
        non_zero_index += 1

# Fill remaining positions with zero
for i in range(non_zero_index, len(arr)):
    arr[i] = 0

print("Array after moving zeros:", arr)
```
</details>

<details>
<summary>1️⃣1️⃣ Write a program to Rotate the Given array d times.</summary>

```python
# Function to left rotate array d times
def rotate_left(arr, d):
    n = len(arr)
    d = d % n
    return arr[d:] + arr[:d]

# Example
arr = [1, 2, 3, 4, 5, 6, 7]
d = 2
rotated = rotate_left(arr, d)
print("Array after rotating left", d, "times:", rotated)
```
</details>
