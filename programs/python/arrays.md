<details open>
<summary>Write a program to print all the elements in array.</summary>
<p>

```python
   # Define the array
arr = [10, 20, 30, 40, 50]

# Print all elements using a loop
print("The elements in the array are:")
for element in arr:
    print(element)

```

</p>
</details>
<details>
<summary>Write a program to print alternate elements in array.</summary>
<p>

```python
# Define the array
arr = [10, 20, 30, 40, 50, 60, 70]

# Print alternate elements
print("Alternate elements in the array are:")
for i in range(0, len(arr), 2):  # step by 2
    print(arr[i])

```

</p>
</details>

<details>
<summary>Write a program to print even numbers in array.</summary>
<p>

```python
# Define the array
arr = [5, 8, 13, 22, 36, 41, 50]

# Print even numbers
print("Even numbers in the array are:")
for num in arr:
    if num % 2 == 0:
        print(num)


```

</p>
</details>
<details>
<summary>Write a program to print all the odd numbers in array.</summary>
<p>

```python
# Define the array
arr = [5, 8, 13, 22, 36, 41, 50]

# Print odd numbers
print("Odd numbers in the array are:")
for num in arr:
    if num % 2 != 0:
        print(num)

```
</p>
</details>
<details>
<summary>Write a program to print sum of all the elements in array.</summary>
<p>

```python
# Define the array
arr = [10, 20, 30, 40, 50]

# Calculate the sum of all elements
total_sum = sum(arr)

# Print the sum
print("The sum of all the elements in the array is:", total_sum)
```
</p>
</details>

<details>
<summary>Write a program to print largest element in array.</summary>
<p>

```python

# Define the array
arr = [10, 20, 30, 50, 40]

# Find the largest element
largest_element = max(arr)

# Print the largest element
print("The largest element in the array is:", largest_element)

```
</p>
</details>

<details>
<summary>Write a program to print duplicate elements in array.</summary>
<p>

```python

# Define the array
arr = [10, 20, 30, 40, 20, 50, 30]

# Use a set to track duplicates
duplicates = set()
for num in arr:
    if arr.count(num) > 1:  # If the element appears more than once
        duplicates.add(num)

# Print the duplicate elements
print("Duplicate elements in the array are:")
for duplicate in duplicates:
    print(duplicate)

```
</p>
</details>


<details>
<summary>Write a program to sort elements in array.</summary>
<p>

```python
# Define the array
arr = [50, 20, 40, 10, 30]

# Sort the array in ascending order
arr.sort()

# Print the sorted array
print("Sorted array in ascending order:", arr)

```
</p>
</details>

<details>
<summary>Write a program to find the Missing Number in 1 to N. </summary>
<p>

```python
# Define the array
arr = [1, 2, 4, 5, 6]  # Example array with one missing number

# Calculate the expected sum of numbers from 1 to N
n = len(arr) + 1  # Since one number is missing
expected_sum = n * (n + 1) // 2  # Formula for sum of first N natural numbers

# Calculate the actual sum of the given array
actual_sum = sum(arr)

# Find the missing number
missing_number = expected_sum - actual_sum

# Print the missing number
print("The missing number is:", missing_number)

```
</p>
</details>


<details>
<summary>Write a program to Move All the Zeros to end of the Array. </summary>
<p>

```python
# Define the array
arr = [0, 1, 0, 3, 12]

# Create a new index to place non-zero elements
non_zero_index = 0

# Move non-zero elements forward
for i in range(len(arr)):
    if arr[i] != 0:
        arr[non_zero_index] =

```
</p>
</details>

<details>
<summary>Write a program to Rotate the Given array d times.</summary>
<p>

```python
# Function to rotate array to the left d times
def left_rotate_array(arr, d):
    n = len(arr)
    d = d % n  # To handle if d > n
    return arr[d:] + arr[:d]

# Example usage
arr = [1, 2, 3, 4, 5, 6, 7]
d = 2  # Number of times to rotate

rotated_array = left_rotate_array(arr, d)
print("Array after", d, "left rotations:", rotated_array)

```
</p>
</details>
