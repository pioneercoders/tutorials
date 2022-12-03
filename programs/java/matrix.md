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
<summary>Print Welcome to PC Program.</summary>
<p>

```java
class App{  
    public static void main(String args[]){  
     System.out.print("Welcome to PC.");  
    }  
}  
```

</p>
</details> 
