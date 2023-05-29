<details open>
<summary open>Write a program to assign a function to a variable in java8.</summary>
<p>

```java
import java.util.function.*;

public class FunctionTest {

    public static void main(String[] args) {
        Function<Integer,Boolean> isEven = (x) -> x %2 == 0;
        boolean result = isEven.apply(6);
        System.out.println(result);
        boolean result1 = isEven.apply(5);
        System.out.println(result1);
    }
}
```

</p>
</details> 

<details>
<summary open>Write a program to pass two arguments to a function in java8.</summary>
<p>

```java
import java.util.function.*;

public class FunctionTest {

    public static void main(String[] args) {
        BiFunction<Integer,Integer, Integer> add = (x, y) -> x + y;
        int result = add.apply(6, 5);
        System.out.println(result);
        int result1 = add.apply(64, 15);
        System.out.println(result1);
    }
}
```

</p>
</details> 


<details>
<summary open>Write a program to pass function as argument to another function in java8.</summary>
<p>

```java
import java.util.function.*;

public class FunctionTest {
    public static BiFunction<Integer,Integer, Integer> add = (x, y) -> x + y;
    public static BiFunction<Integer,Integer, Integer> mul = (x, y) -> x * y;
    
    public static int calc(BiFunction<Integer,Integer,Integer> fun, Integer x, Integer y){
        Integer result = fun.apply(x,y);
        return result;
    }

    public static void main(String[] args) {
        int result = calc(add,6, 5);
        System.out.println(result);
        int result1 = calc(mul,3, 4);
        System.out.println(result);
    }
}
```

</p>
</details> 
