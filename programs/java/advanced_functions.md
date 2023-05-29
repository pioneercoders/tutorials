<details open>
<summary open>Write a program to assign a function to a variable in java.</summary>
<p>

```java
import java.util.function.Function;

public class FunctionTest {

    public static void main(String[] args) {
        Function<Integer,Boolean> isEven = (x) -> x %2 == 0;
        boolean result = isEven.apply(6);
        System.out.println(result);
    }
}
```

</p>
</details> 
