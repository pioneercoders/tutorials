<details open>
<summary>Write function to find given number is even or odd.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){
        boolean r = isEven(4);
        System.out.println(r);  
    }  
    
    public static boolean isEven(int x){
        boolean result = x%2 == 0;
        return result;
    }
}  
```

</p>
</details> 

<details>
<summary>Write function to return given string with uppercase.</summary>
<p>

```java
public class App{  
    public static void main(String args[]){
        String str = toUpper("welcome");
        System.out.println(str);  
    }  
    
    public static boolean toUpper(String s){
        String result = s.toUpperCase();
        return result;
    }
}  
```

</p>
</details> 

<details>
<summary>Write function to show call by value.</summary>
<p>

```java
public class CallByValue {

	public static void main(String[] args) {
		int age = 24;
		System.out.println(age);
		changeAge(age);
		System.out.println(age);
	}

	private static void changeAge(int age) {
		age = 45;
	}

}
```

</p>
</details> 

<details>
<summary>Write function to Print 1 to 10 without using loop.</summary>
<p>

```java
public class RecursionFun {
	
	public static void main(String[] args) {
		printWihtoutLoop(1);
	}
	
	public static void printWihtoutLoop(int n){
		if(n <= 10){
			System.out.println(n);
			printWihtoutLoop( n+1 );
		}
	}
}
```

</p>
</details> 


<details>
<summary>Write function to show call by reference.</summary>
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
		System.out.println("printProduct() -> " + pro.id + " " + pro.name + " " + pro.price);
	}

	private static void changeProductValues(Product pro) {
		pro.id = 14;
		pro.price = 3000.50f;
	}

	private static void makeProductNull(Product pro) {
		pro = null;
	}
}

```

</p>
</details>

<details>
<summary>Write function to show class type as argument and return type.</summary>
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
		Product products[] = new Product[2];
		// create first product
		Product pro = new Product();
		pro.id = 2;
		pro.name = "Nokia 6";
		pro.price = 7000.50f;

		Product pro1 = new Product();
		pro1.id = 4;
		pro1.name = "Samsung";
		pro1.price = 9000.50f;

		products[0] = pro; // assign product to array zero location
		products[1] = pro1; // assign product to array first location

		printProducts(products);

		products = getProducts();
		printProducts(products);
	}

	private static Product[] getProducts() {
		Product products[] = new Product[2];
		Scanner scaner = new Scanner(System.in);
		for (int i = 0; i < 2; i++) {
			System.out.println("Enter product Id:");
			int productId = scaner.nextInt();
			System.out.println("Enter product Name:");
			String productName = scaner.next();
			System.out.println("Enter product Price:");
			float productPrice = scaner.nextFloat();
			Product pro = new Product();
			pro.id = productId;
			pro.name = productName;
			pro.price = productPrice;
			products[i] = pro;
		}
		scaner.close();
		return products;
	}

	private static void printProducts(Product[] products) {
		for (int index = 0; index < products.length; index++) {
			System.out.println(products[index].id + " " + products[index].name + " " + products[index].price);
		}
	}

}
```

</p>
</details> 
