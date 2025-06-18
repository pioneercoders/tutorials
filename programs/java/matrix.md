<details open>
<summary>1️⃣ Write a program to print a ChessBoard pattern</summary>
<p>

```java
import java.util.Arrays;

public class ChessBoard {
    public static void main(String[] args) {
        int size = 8;
        char[][] board = new char[size][size];

        for (int row = 0; row < size; row++) {
            boolean isWhite = row % 2 == 0;
            for (int col = 0; col < size; col++) {
                board[row][col] = isWhite ? 'W' : 'B';
                isWhite = !isWhite;
            }
        }

        for (char[] row : board) {
            System.out.println(Arrays.toString(row));
        }
    }
}
```

</p>
</details>

<details>
<summary>2️⃣ Write a program to perform Spiral Traversal on a Matrix</summary>
<p>

```java
public class SpiralTraversal {

    static int R = 4, C = 4;

    static void printSpiral(int[][] matrix, int i, int j, int m, int n) {
        if (i >= m || j >= n) return;

        for (int p = j; p < n; p++) System.out.print(matrix[i][p] + " ");
        for (int p = i + 1; p < m; p++) System.out.print(matrix[p][n - 1] + " ");
        if ((m - 1) != i)
            for (int p = n - 2; p >= j; p--) System.out.print(matrix[m - 1][p] + " ");
        if ((n - 1) != j)
            for (int p = m - 2; p > i; p--) System.out.print(matrix[p][j] + " ");

        printSpiral(matrix, i + 1, j + 1, m - 1, n - 1);
    }

    public static void main(String[] args) {
        int[][] matrix = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 },
            { 13, 14, 15, 16 }
        };
        printSpiral(matrix, 0, 0, R, C);
    }
}
```

</p>
</details>

<details>
<summary>3️⃣ Write a program to search for an element in a matrix (row/column-wise sorted)</summary>
<p>

```java
public class MatrixSearch {

    public static boolean searchMatrix(int[][] matrix, int key) {
        int row = 0, col = matrix[0].length - 1;

        while (row < matrix.length && col >= 0) {
            if (matrix[row][col] == key) return true;
            else if (matrix[row][col] > key) col--;
            else row++;
        }

        return false;
    }

    public static void main(String[] args) {
        int[][] matrix = {
            { 1, 3, 5, 7 },
            { 10, 11, 16, 20 },
            { 23, 30, 34, 50 }
        };

        int key = 16;
        System.out.println("Is key present? " + searchMatrix(matrix, key));
    }
}
```

</p>
</details>

<details>
<summary>4️⃣ Write a program to find the row with maximum number of 1s in a binary matrix</summary>
<p>

```java
public class RowWithMaxOnes {

    public static int rowWithMaxOnes(int[][] mat) {
        int maxRow = -1, col = mat[0].length - 1;

        for (int row = 0; row < mat.length; row++) {
            while (col >= 0 && mat[row][col] == 1) {
                col--;
                maxRow = row;
            }
        }

        return maxRow;
    }

    public static void main(String[] args) {
        int[][] mat = {
            { 0, 0, 0, 1 },
            { 0, 1, 1, 1 },
            { 1, 1, 1, 1 },
            { 0, 0, 0, 0 }
        };

        int index = rowWithMaxOnes(mat);
        System.out.println("Row with maximum 1s is at index: " + index);
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Write a program for Diagonal Traversal of a Matrix</summary>
<p>

```java
public class DiagonalTraversal {
    public static void main(String[] args) {
        int[][] matrix = {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };
        int m = matrix.length;
        int n = matrix[0].length;

        for (int d = 0; d < m + n - 1; d++) {
            int row = d < n ? 0 : d - n + 1;
            int col = d < n ? d : n - 1;

            while (row < m && col >= 0) {
                System.out.print(matrix[row][col] + " ");
                row++;
                col--;
            }
        }
    }
}
```

</p>
</details>

<details>
<summary>6️⃣ Write a program for Zigzag Traversal of a Matrix</summary>
<p>

```java
public class ZigzagTraversal {
    public static void main(String[] args) {
        int[][] matrix = {
            { 1, 2, 3 },
            { 4, 5, 6 },
            { 7, 8, 9 }
        };

        for (int i = 0; i < matrix.length; i++) {
            if (i % 2 == 0) {
                for (int j = 0; j < matrix[i].length; j++) {
                    System.out.print(matrix[i][j] + " ");
                }
            } else {
                for (int j = matrix[i].length - 1; j >= 0; j--) {
                    System.out.print(matrix[i][j] + " ");
                }
            }
        }
    }
}
```

</p>
</details>
