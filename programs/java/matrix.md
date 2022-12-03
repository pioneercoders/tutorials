<details open>
<summary>Write a program to print ChessBoard.</summary>
<p>

```java
import java.util.*;

public class ChessBoard {
    public static void main(String[] args) {
        int boardDim = 8; 
        char[][] board = new char[boardDim][boardDim];
        boolean isWhite = false;
        
        for(int y = 0; y < board.length; y++)
        {
            isWhite = !isWhite;
            for(int x = 0; x < board[y].length; x++)
            {
                if(isWhite) board[y][x] = 'W';
                if(!isWhite) board[y][x] = 'B';
                isWhite = !isWhite;
            }
        }
        
        for(int i = 0; i < board.length; i++)
        {
            System.out.println(Arrays.toString(board[i]));
        }
    }
}  
```

</p>
</details> 

<details>
<summary>Write a programs to print Spiral traversal on a Matrix.</summary>
<p>

```java
public class SpiralTraversal {

    static int R = 4;
    static int C = 4;

    // Function for printing matrix in spiral
    // form i, j: Start index of matrix, row
    // and column respectively m, n: End index
    // of matrix row and column respectively
    static void print(int arr[][], int i, int j, int m,
                      int n)
    {
        // If i or j lies outside the matrix
        if (i >= m || j >= n) {
            return;
        }

        // Print First Row
        for (int p = i; p < n; p++) {
            System.out.print(arr[i][p] + " ");
        }

        // Print Last Column
        for (int p = i + 1; p < m; p++) {
            System.out.print(arr[p][n - 1] + " ");
        }

        // Print Last Row, if Last and
        // First Row are not same
        if ((m - 1) != i) {
            for (int p = n - 2; p >= j; p--) {
                System.out.print(arr[m - 1][p] + " ");
            }
        }

        // Print First Column, if Last and
        // First Column are not same
        if ((n - 1) != j) {
            for (int p = m - 2; p > i; p--) {
                System.out.print(arr[p][j] + " ");
            }
        }
        print(arr, i + 1, j + 1, m - 1, n - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] a = { { 1, 2, 3, 4 },
                { 5, 6, 7, 8 },
                { 9, 10, 11, 12 },
                { 13, 14, 15, 16 } };

        // Function Call
        print(a, 0, 0, R, C);
    }
}  
```

</p>
</details> 

<details>
<summary>Write a programs to Search an element in a matrix.</summary>
<p>

```java
public class MatrixSearch {
    static int R = 4;
    static int C = 4;

    // Function for printing matrix in spiral
    // form i, j: Start index of matrix, row
    // and column respectively m, n: End index
    // of matrix row and column respectively
    static void print(int[][] arr, int i, int j, int m, int n)
    {
        // If i or j lies outside the matrix
        if (i >= m || j >= n) {
            return;
        }

        // Print First Row
        for (int p = i; p < n; p++) {
            System.out.print(arr[i][p] + " ");
        }

        // Print Last Column
        for (int p = i + 1; p < m; p++) {
            System.out.print(arr[p][n - 1] + " ");
        }

        // Print Last Row, if Last and
        // First Row are not same
        if ((m - 1) != i) {
            for (int p = n - 2; p >= j; p--) {
                System.out.print(arr[m - 1][p] + " ");
            }
        }

        // Print First Column, if Last and
        // First Column are not same
        if ((n - 1) != j) {
            for (int p = m - 2; p > i; p--) {
                System.out.print(arr[p][j] + " ");
            }
        }
        print(arr, i + 1, j + 1, m - 1, n - 1);
    }

    // Driver Code
    public static void main(String[] args) {
        int[][] a = { { 1, 2, 3, 4 },
                { 5, 6, 7, 8 },
                { 9, 10, 11, 12 },
                { 13, 14, 15, 16 } };

        // Function Call
        print(a, 0, 0, R, C);
    }
} 
```

</p>
</details> 

<details>
<summary>Write a programs to Find row with maximum no. of 1's</summary>
<p>

```java
public class Matrix_Problem_04 {

    static int R = 4, C = 4;
    // Function that returns index of row with maximum number of 1s.
    static int rowWithMax1s(int[][] mat) {

        // Initialize first row as row with max 1s
        int j,max_row_index = 0;
        j = C - 1;

        for (int i = 0; i < R; i++) {
            // Move left until a 0 is found
            while (j >= 0 && mat[i][j] == 1) {
                j = j - 1; // Update the index of leftmost 1
                // seen so far
                max_row_index = i; // Update max_row_index
            }
        }

        if(max_row_index==0&&mat[0][C-1]==0)
            return -1;

        return max_row_index;
    }

    // Driver Code
    public static void main(String[] args) {
        int[][] mat = {
                { 0, 0, 0, 1 },
                { 0, 1, 1, 1 },
                { 1, 1, 1, 1 },
                { 0, 0, 0, 0 }
        };
        System.out.println("Index of row with maximum 1s is " + rowWithMax1s(mat));
    }
} 
```

</p>
</details> 
