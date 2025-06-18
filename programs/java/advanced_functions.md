<details open>
<summary>1️⃣ Assign a function to a variable</summary>
<p>

```java
import java.util.function.*;

public class FunctionAssignment {
    public static void main(String[] args) {
        Function<Integer, Boolean> isEven = x -> x % 2 == 0;
        System.out.println(isEven.apply(6));  // true
        System.out.println(isEven.apply(5));  // false
    }
}
```

</p>
</details>

<details>
<summary>2️⃣ Pass two arguments to a function</summary>
<p>

```java
import java.util.function.*;

public class BiFunctionExample {
    public static void main(String[] args) {
        BiFunction<Integer, Integer, Integer> add = (x, y) -> x + y;
        System.out.println(add.apply(6, 5));   // 11
        System.out.println(add.apply(64, 15)); // 79
    }
}
```

</p>
</details>

<details>
<summary>3️⃣ Pass a function as an argument (Higher-order function)</summary>
<p>

```java
import java.util.function.*;

public class FunctionAsArgument {
    public static int calculate(BiFunction<Integer, Integer, Integer> op, int a, int b) {
        return op.apply(a, b);
    }

    public static void main(String[] args) {
        BiFunction<Integer, Integer, Integer> add = (x, y) -> x + y;
        BiFunction<Integer, Integer, Integer> mul = (x, y) -> x * y;
        System.out.println(calculate(add, 6, 5));  // 11
        System.out.println(calculate(mul, 3, 4));  // 12
    }
}
```

</p>
</details>

<details>
<summary>4️⃣ Return a function from another function (Higher-order function)</summary>
<p>

```java
import java.util.function.*;

public class FunctionReturningFunction {
    public static BiFunction<Integer, Integer, Integer> getAdder() {
        return (x, y) -> x + y;
    }

    public static void main(String[] args) {
        BiFunction<Integer, Integer, Integer> adder = getAdder();
        System.out.println(adder.apply(3, 4)); // 7
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Compose functions using Function.compose and andThen</summary>
<p>

```java
import java.util.function.*;

public class FunctionComposition {
    public static void main(String[] args) {
        Function<Integer, Integer> multiplyBy2 = x -> x * 2;
        Function<Integer, Integer> add10 = x -> x + 10;

        Function<Integer, Integer> composed1 = multiplyBy2.andThen(add10); // (x*2)+10
        Function<Integer, Integer> composed2 = multiplyBy2.compose(add10); // (x+10)*2

        System.out.println(composed1.apply(5)); // 20
        System.out.println(composed2.apply(5)); // 30
    }
}
```

</p>
</details>

<details>
<summary>6️⃣ Use Predicate to filter a list</summary>
<p>

```java
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

public class PredicateFiltering {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 5, 10, 15, 20, 25);
        Predicate<Integer> isDivisibleBy5 = x -> x % 5 == 0;

        List<Integer> filtered = numbers.stream()
                                        .filter(isDivisibleBy5)
                                        .collect(Collectors.toList());

        System.out.println(filtered); // [5, 10, 15, 20, 25]
    }
}
```

</p>
</details>

<details>
<summary>7️⃣ Lambda chaining with streams</summary>
<p>

```java
import java.util.*;
import java.util.stream.*;

public class LambdaChaining {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("rama", "krishna", "arjun", "bharat", "kiran");

        List<String> result = names.stream()
                                   .filter(name -> name.length() > 4)
                                   .map(String::toUpperCase)
                                   .sorted()
                                   .collect(Collectors.toList());

        System.out.println(result); // [BHARAT, KRISHNA]
    }
}
```

</p>
</details>

<details>
<summary>8️⃣ Chain Predicates using and(), or(), negate()</summary>
<p>

```java
import java.util.function.*;

public class PredicateChaining {
    public static void main(String[] args) {
        Predicate<String> startsWithK = s -> s.startsWith("K");
        Predicate<String> endsWithN = s -> s.endsWith("n");

        Predicate<String> combined = startsWithK.and(endsWithN);

        System.out.println(combined.test("Kiran")); // true
        System.out.println(combined.test("Karthik")); // false
    }
}
```

</p>
</details>

<details>
<summary>9️⃣ Use Stream map and reduce for transformation and aggregation</summary>
<p>

```java
import java.util.*;
import java.util.stream.*;

public class MapAndReduce {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(2, 3, 4, 5);

        int sumOfSquares = numbers.stream()
                                  .map(x -> x * x)
                                  .reduce(0, Integer::sum);

        System.out.println("Sum of squares: " + sumOfSquares); // 54
    }
}
```

</p>
</details>

<details>
<summary>🔟 Grouping with Streams and Collectors</summary>
<p>

```java
import java.util.*;
import java.util.stream.*;
import java.util.function.*;
import java.util.Map;

class Person {
    String name;
    String city;
    Person(String name, String city) {
        this.name = name;
        this.city = city;
    }
}

public class StreamGrouping {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
            new Person("Ravi", "Delhi"),
            new Person("Priya", "Mumbai"),
            new Person("Amit", "Delhi"),
            new Person("Neha", "Mumbai")
        );

        Map<String, List<String>> grouped = people.stream()
            .collect(Collectors.groupingBy(
                p -> p.city,
                Collectors.mapping(p -> p.name, Collectors.toList())
            ));

        System.out.println(grouped);
        // Output: {Delhi=[Ravi, Amit], Mumbai=[Priya, Neha]}
    }
}
```

</p>
</details>
