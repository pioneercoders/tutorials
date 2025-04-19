<details open>
<summary>write a program that can print the number of prime numbers less than N and you are given a non-negative integer N</summary>
<p>

```python
   def is_prime(num):
    if num < 2:
        return False
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            return False
    return True

def count_primes(n):
    count = 0
    for i in range(n):
        if is_prime(i):
            count += 1
    return count

# Example: Input from user
N = int(input("Enter a non-negative integer: "))
print("Number of prime numbers less than", N, "is:", count_primes(N))

```

</p>
</details>

<details>
<summary>Given two binary strings a and b,Write a program to find their sum as a binary string and perform the binary addition operation on these values</summary>
<p>

```python
def add_binary(a, b):
    # Convert binary strings to integers
    num1 = int(a, 2)
    num2 = int(b, 2)
    
    # Add the integers
    total = num1 + num2
    
    # Convert the result back to binary string and remove '0b' prefix
    return bin(total)[2:]

# Example usage
a = input("Enter first binary number: ")  # e.g., 1010
b = input("Enter second binary number: ") # e.g., 1101

result = add_binary(a, b)
print(f"Binary sum of {a} and {b} is: {result}")


```

</p>
</details>

<details >
<summary>Write a Java program that moves all zeros to the end of an integer list while maintaining the relative order of the non-zero elements.</summary>
<p>

```python

def move_zeros_to_end(arr):
    n = len(arr)
    index = 0  # Position to place the next non-zero element

    # Move all non-zero elements to the front
    for i in range(n):
        if arr[i] != 0:
            arr[index] = arr[i]
            index += 1

    # Fill remaining positions with 0
    while index < n:
        arr[index] = 0
        index += 1

    return arr

# Example usage
arr = [0, 1, 0, 3, 12, 0, 5]
print("Original Array:", arr)
result = move_zeros_to_end(arr)
print("After moving zeros to end:", result)

```

</p>
</details>

<details >
<summary>Write a Java program that finds the size (number of cells occupied) of the largest contiguous cross-section consisting of a single element type in a 2D matrix A. The matrix A represents a cross-section of a nuclear reactor with different types of elements present in each cell.</summary>
<p>

```python
def largest_contiguous_region(matrix):
    if not matrix or not matrix[0]:
        return 0

    rows = len(matrix)
    cols = len(matrix[0])
    visited = [[False] * cols for _ in range(rows)]
    max_size = 0

    # Directions: up, down, left, right
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]

    def dfs(r, c, value):
        stack = [(r, c)]
        size = 0

        while stack:
            x, y = stack.pop()
            if 0 <= x < rows and 0 <= y < cols and not visited[x][y] and matrix[x][y] == value:
                visited[x][y] = True
                size += 1
                for dx, dy in directions:
                    stack.append((x + dx, y + dy))
        return size

    for i in range(rows):
        for j in range(cols):
            if not visited[i][j]:
                region_size = dfs(i, j, matrix[i][j])
                max_size = max(max_size, region_size)

    return max_size

# Example usage
A = [
    [1, 2, 2, 3],
    [1, 2, 2, 3],
    [4, 4, 2, 3],
    [4, 4, 4, 3]
]

print("Size of the largest contiguous region:", largest_contiguous_region(A))


```

</p>
</details>

</details>

<details >
<summary>Write a Java program that finds the size (number of cells occupied) of the largest contiguous cross-section consisting of a single element type in a 2D matrix A. The matrix A represents a cross-section of a nuclear reactor with different types of elements present in each cell.</summary>
<p>

```python

```

</p>
</details>
