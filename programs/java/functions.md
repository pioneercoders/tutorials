<details open>
<summary>1️⃣ Write function to find given number is even or odd.</summary>
<p>

```java
public class EvenOddFun {  
    public static void main(String[] args) {
        boolean result = isEven(4);
        System.out.println(result);  
    }  
    
    public static boolean isEven(int x) {
        return x % 2 == 0;
    }
}  
```

</p>
</details>

<details>
<summary>2️⃣ Write function to convert given string to uppercase.</summary>
<p>

```java
public class ToUpperCaseFun {  
    public static void main(String[] args) {
        String str = toUpper("welcome");
        System.out.println(str);  
    }  
    
    public static String toUpper(String s) {
        return s.toUpperCase();
    }
}  
```

</p>
</details>

<details>
<summary>3️⃣ Write function to show call by value.</summary>
<p>

```java
public class CallByValue {

    public static void main(String[] args) {
        int age = 24;
        System.out.println("Before change: " + age);
        changeAge(age);
        System.out.println("After change: " + age);
    }

    private static void changeAge(int age) {
        age = 45;
    }
}
```

</p>
</details>

<details>
<summary>4️⃣ Write function to print 1 to 10 without using loop.</summary>
<p>

```java
public class RecursionFun {
    
    public static void main(String[] args) {
        printWithoutLoop(1);
    }
    
    public static void printWithoutLoop(int n) {
        if (n <= 10) {
            System.out.println(n);
            printWithoutLoop(n + 1);
        }
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Write function to show call by reference.</summary>
<p>

```java
class Product {
    int id;
    String name;
    float price;
}

public class CallByReferenceEx {

    public static void main(String[] args) {
        Product pro = new Product();
        pro.id = 12;
        pro.name = "Nokia";
        pro.price = 3.4f;

        printProduct(pro);
        changeProductValues(pro);
        printProduct(pro);
        makeProductNull(pro);
        printProduct(pro);
    }

    private static void printProduct(Product pro) {
        if (pro != null) {
            System.out.println("printProduct() -> " + pro.id + " " + pro.name + " " + pro.price);
        } else {
            System.out.println("printProduct() -> null");
        }
    }

    private static void changeProductValues(Product pro) {
        pro.id = 14;
        pro.price = 3000.50f;
    }

    private static void makeProductNull(Product pro) {
        pro = null; // only affects local reference
    }
}
```

</p>
</details>

<details>
<summary>6️⃣ Write function to return list of products.</summary>
<p>

```java
import java.util.Scanner;

class Product {
    int id;
    String name;
    float price;
}

public class ProductListEx {

    public static void main(String[] args) {
        Product[] products = new Product[2];

        Product pro1 = new Product();
        pro1.id = 2;
        pro1.name = "Nokia 6";
        pro1.price = 7000.50f;

        Product pro2 = new Product();
        pro2.id = 4;
        pro2.name = "Samsung";
        pro2.price = 9000.50f;

        products[0] = pro1;
        products[1] = pro2;

        printProducts(products);

        products = getProductsFromUser();
        printProducts(products);
    }

    private static Product[] getProductsFromUser() {
        Scanner scanner = new Scanner(System.in);
        Product[] products = new Product[2];

        for (int i = 0; i < 2; i++) {
            Product pro = new Product();
            System.out.println("Enter product Id:");
            pro.id = scanner.nextInt();
            System.out.println("Enter product Name:");
            pro.name = scanner.next();
            System.out.println("Enter product Price:");
            pro.price = scanner.nextFloat();
            products[i] = pro;
        }

        scanner.close();
        return products;
    }

    private static void printProducts(Product[] products) {
        for (Product product : products) {
            System.out.println(product.id + " " + product.name + " " + product.price);
        }
    }
}
```

</p>
</details>

<details>
<summary>7️⃣ Write function to reverse given number.</summary>
<p>

```java
import java.util.Scanner;

public class ReverseGivenNumber {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter a number:");
        int n = sc.nextInt();
        int reversed = reverse(n);
        System.out.println("Reversed number: " + reversed);
        sc.close();
    }

    private static int reverse(int n) {
        int reversed = 0;
        while (n > 0) {
            int lastDigit = n % 10;
            reversed = reversed * 10 + lastDigit;
            n = n / 10;
        }
        return reversed;
    }
}
```

</p>
</details>

<details>
<summary>8️⃣ Write a simple calculator.</summary>
<p>

```java
import java.util.Scanner;

public class Calculator {

    static float sum(float a, float b) {
        return a + b;
    }

    static float subtract(float a, float b) {
        return a - b;
    }

    static float multiply(float a, float b) {
        return a * b;
    }

    static float divide(float a, float b) {
        if (b != 0) return a / b;
        else {
            System.out.println("Cannot divide by zero.");
            return 0;
        }
    }

    static float squareRoot(float a) {
        return (float) Math.sqrt(a);
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.println("Choose operation:\n1. SUM\n2. SUBTRACT\n3. MULTIPLY\n4. DIVIDE\n5. SQUARE ROOT");
        int choice = in.nextInt();

        switch (choice) {
            case 1:
                System.out.println("Enter two numbers:");
                System.out.println("Result: " + sum(in.nextFloat(), in.nextFloat()));
                break;
            case 2:
                System.out.println("Enter two numbers:");
                System.out.println("Result: " + subtract(in.nextFloat(), in.nextFloat()));
                break;
            case 3:
                System.out.println("Enter two numbers:");
                System.out.println("Result: " + multiply(in.nextFloat(), in.nextFloat()));
                break;
            case 4:
                System.out.println("Enter two numbers:");
                System.out.println("Result: " + divide(in.nextFloat(), in.nextFloat()));
                break;
            case 5:
                System.out.println("Enter a number:");
                System.out.println("Result: " + squareRoot(in.nextFloat()));
                break;
            default:
                System.out.println("Invalid choice.");
        }

        in.close();
    }
}
```

</p>
</details>
