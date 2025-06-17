<details open>
<summary>1️⃣ Print a Chessboard Pattern</summary>

```python
# Function to print chessboard pattern
def print_chessboard(size=8):
    for i in range(size):
        row = ""
        for j in range(size):
            if (i + j) % 2 == 0:
                row += "B "
            else:
                row += "W "
        print(row.strip())

print_chessboard()
```
</details>

<details>
<summary>2️⃣ Spiral Traversal of a Matrix</summary>

```python
def spiral_traversal(matrix):
    if not matrix or not matrix[0]:
        return []

    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1

    while top <= bottom and left <= right:
        for i in range(left, right + 1):
            result.append(matrix[top][i])
        top += 1

        for i in range(top, bottom + 1):
            result.append(matrix[i][right])
        right -= 1

        if top <= bottom:
            for i in range(right, left - 1, -1):
                result.append(matrix[bottom][i])
            bottom -= 1

        if left <= right:
            for i in range(bottom, top - 1, -1):
                result.append(matrix[i][left])
            left += 1

    return result

matrix = [
    [1,  2,  3,  4],
    [5,  6,  7,  8],
    [9, 10, 11, 12],
    [13,14, 15, 16]
]

print("Spiral Traversal:", spiral_traversal(matrix))
```
</details>

<details>
<summary>3️⃣ Search an Element in a Matrix</summary>

```python
def search_matrix(matrix, target):
    for i in range(len(matrix)):
        for j in range(len(matrix[i])):
            if matrix[i][j] == target:
                return f"Element {target} found at position ({i}, {j})"
    return f"Element {target} not found"

matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

target = 5
print(search_matrix(matrix, target))
```
</details>

<details>
<summary>4️⃣ Find Row with Maximum Number of 1's</summary>

```python
def row_with_max_ones(matrix):
    max_count = 0
    row_index = -1
    for i in range(len(matrix)):
        count = matrix[i].count(1)
        if count > max_count:
            max_count = count
            row_index = i
    return row_index if row_index != -1 else "No 1's found"

matrix = [
    [0, 1, 1, 0],
    [1, 1, 1, 0],
    [1, 1, 0, 0],
    [0, 1, 1, 1]
]

print(f"Row with the maximum number of 1's: Row {row_with_max_ones(matrix)}")
```
</details>

<details>
<summary>5️⃣ Sum of Primary and Secondary Diagonals</summary>

```python
def diagonal_sums(matrix):
    n = len(matrix)
    primary = 0
    secondary = 0
    for i in range(n):
        primary += matrix[i][i]
        secondary += matrix[i][n - i - 1]
    return primary, secondary

matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

primary, secondary = diagonal_sums(matrix)
print("Primary diagonal sum:", primary)
print("Secondary diagonal sum:", secondary)
```
</details>

<details>
<summary>6️⃣ Matrix Multiplication</summary>

```python
def multiply_matrices(A, B):
    result = []
    rows_A = len(A)
    cols_A = len(A[0])
    cols_B = len(B[0])

    for i in range(rows_A):
        row = []
        for j in range(cols_B):
            val = 0
            for k in range(cols_A):
                val += A[i][k] * B[k][j]
            row.append(val)
        result.append(row)
    return result

A = [
    [1, 2],
    [3, 4]
]

B = [
    [5, 6],
    [7, 8]
]

product = multiply_matrices(A, B)
print("Matrix multiplication result:")
for row in product:
    print(row)
```
</details>
