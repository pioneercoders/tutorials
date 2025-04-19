<details open>
<summary>Write a program to print ChessBoard.</summary>
<p>

```python
  # Function to print chessboard pattern
def print_chessboard(size=8):
    for i in range(size):
        row = ""
        for j in range(size):
            # Alternate between black (B) and white (W)
            if (i + j) % 2 == 0:
                row += "B "  # Black square
            else:
                row += "W "  # White square
        print(row)

# Call the function to print the chessboard
print_chessboard()
 
```

</p>
</details>
<details >
<summary>Write a programs to print Spiral traversal on a Matrix.</summary>
<p>

```python
# Function to print spiral traversal of matrix
def spiral_traversal(matrix):
    if not matrix:
        return
    
    top, bottom, left, right = 0, len(matrix) - 1, 0, len(matrix[0]) - 1
    result = []

    while top <= bottom and left <= right:
        # Traverse from left to right along the top row
        for i in range(left, right + 1):
            result.append(matrix[top][i])
        top += 1

        # Traverse from top to bottom along the right column
        for i in range(top, bottom + 1):
            result.append(matrix[i][right])
        right -= 1

        if top <= bottom:
            # Traverse from right to left along the bottom row
            for i in range(right, left - 1, -1):
                result.append(matrix[bottom][i])
            bottom -= 1

        if left <= right:
            # Traverse from bottom to top along the left column
            for i in range(bottom, top - 1, -1):
                result.append(matrix[i][left])
            left += 1

    return result

# Example matrix
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
]

# Print the result of spiral traversal
result = spiral_traversal(matrix)
print("Spiral Traversal:", result)

```

</p>
</details>

<details >
<summary>Write a programs to Search an element in a matrix.</summary>
<p>

```python
# Function to search for an element in the matrix
def search_matrix(matrix, target):
    for i in range(len(matrix)):
        for j in range(len(matrix[i])):
            if matrix[i][j] == target:
                return f"Element {target} found at position ({i}, {j})"
    return f"Element {target} not found in the matrix"

# Example matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Target element to search for
target = 5

# Print the result of the search
result = search_matrix(matrix, target)
print(result)

```

</p>
</details>

<details >
<summary>Write a programs to Search an element in a matrix.</summary>
<p>

```python

```

</p>
</details>
