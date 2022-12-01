<details open>
<summary open>Write a program to print all the elements in array.</summary>
<p>

```java
public class PrintElementsInArray {

        public static void main(String[] args) {
            // TODO Auto-generated method stub
            int[] array = {1, 2, 3, 4, 5};//initialization of elements in an array

            for (int i=0; i<= array.length-1;i++) {
                System.out.println(array[i]);//printing the array elements using for loop
            }
        }
    } 
```

</p>
</details> 

<details>
<summary>Write a program to print alternate elements in array.</summary>
<p>

```java
import java.util.Scanner;

public class PrintAlternateElementsInArray {

    public static void main(String[] args) {
        // TODO Auto-generated method stub

        int i, count;
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter the Length of Array");
        count = scan.nextInt();//stores the length of the array in count variable
        int a[] = new int[count];
        for (i = 0; i < count; i++) {
            System.out.print("Enter number " + (i + 1));
            a[i] = scan.nextInt();//entered elements are stored in an array
        }
        scan.close();//object closing
        System.out.print("\nOriginal array is :\t");
        for (i = 0; i < count; i++)
            System.out.print(a[i] + "\t");//printing the original array

        System.out.print("\n\nAlternate elements :\t");
        for (i = 0; i < count; i = i + 2)
            System.out.print(a[i] + "\t");//printing the alternate elements in an array
    }
}
```

</p>
</details> 



<details>
<summary open>Write a program to print even numbers in array.</summary>
<p>

```java
import java.util.Scanner;

public class PrintEvenNums {

    public static void main(String[] args) {
        int arr[] = {1,2,3,4,5,6,7,8};//initialization of elements in an array

        for (int i = 0; i<=arr.length-1; i++) {
            if (arr[i] % 2 == 0)//condition to find out the even numbers in an array
                System.out.println(arr[i]+"is Even Number");//printing the even numbers in the given array
        }
    }
}
```

</p>
</details> 


<details>
<summary open>Write a program to print all the odd numbers in array.</summary>
<p>

```java
public class PrintOddNumsArray {

    public static void main(String[] args) {
        int arr[] = {1,2,3,4,5,6,7,8};//initialization of elements in an array
        for (int i = 0; i<=arr.length-1; i++) {
            if (arr[i] % 2 != 0)//condition for the odd numbers
                System.out.println(arr[i]+"is Odd Number");//printing odd numbers in an array
        }
    }
} 
```

</p>
</details>

<details>
<summary open>Write a program to print sum of all the elements in array.</summary>
<p>

```java
import java.util.Scanner;

public class SumAndAvgOfArray {

    public static void main(String[] args) {
        int n, sum = 0;
        float average;
        Scanner sr = new Scanner(System.in);
        System.out.print("Enter no. of elements you want in array:");
        n = sr.nextInt();//storing the elemnts in 'n' varaible
        int arr[] = new int[n];
        System.out.println("Enter all the elements:");
        for(int i = 0; i < n ; i++)//displaying all elements in an array
        {
            arr[i] = sr.nextInt();
            sum = sum + arr[i];//adding one by one element and storing in a sum varaible
        }
        System.out.println("Sum:"+sum);
        average = (float)sum / n;//calculation average of given numbers in an aray
        System.out.println("Average:"+average);//printing the average value
    }
}
```

</p>
</details>

<details>
<summary open>Write a program to print largest element in array.</summary>
<p>

```java
import java.util.Scanner;

public class LargestNumInArray {

	public static void main(String[] args) {
		
		int n, max;
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter number of elements in the array:");
        n = scan.nextInt();
        int arr[] = new int[n];
        System.out.println("Enter elements of array:");
        for(int i = 0; i < n; i++)
        {
            arr[i] = scan.nextInt();
        }
        max = arr[0];
        for(int i = 0; i < n; i++)
        {
            if(max < arr[i])
            {
                max = arr[i];
            }
        }
        System.out.println("Maximum value:"+max);
    }
}
```

</p>
</details>

<details>
<summary open>Write a program to print duplicate elements in array.</summary>
<p>

```java
public class DuplicateElementsInArray {

	public static void main(String[] args) {
		String[] strArray = {"ramu", "hari", "phani", "phani", "Aparna", "hari", "krishna"};
		 
        for (int i = 0; i < strArray.length-1; i++)
        {
            for (int j = i+1; j < strArray.length; j++)
            {
                if( (strArray[i].equals(strArray[j])) && (i != j) )
                {
                    System.out.println("Duplicate Element is : "+strArray[j]);
                }
            }
        }
    }    
}
```

</p>
</details>

<details>
<summary open>Write a program to sort elements in array.</summary>
<p>

```java
import java.util.Scanner;

public class SortAnArray {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        int n, temp;
        Scanner s = new Scanner(System.in);
        System.out.print("Enter the Size of array:");
        n = s.nextInt();
        int arr[] = new int[n];
        System.out.println("Enter all the elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = s.nextInt();
        }
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                if (arr[i] > arr[j]){
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
        System.out.print("Ascending Order:");
        for (int i = 0; i < n - 1; i++)
        {
            System.out.print(arr[i] + ",");
        }
        System.out.print(arr[n - 1]);
    }
}
```

</p>
</details>

<details>
<summary>Write a program to find the Missing Number in 1 to N.</summary>
<p>

```java
public class FindMissingNo {
	public static void main(String[] args) {
//		int array[] = {2, 4, 1, 6, 7, 5, 3, 9};
		int array[] = {2, 4, 1, 6, 3};
		int n = array.length;

		//calculate the sum of array
		int arraySum = 0;
		for(int v : array)
			arraySum += v;

		//array length is 8
		//one no is missing, then n should be n+1
		// here 8+1
		n = n+1;
		
		//this calculates the sum from 1 to (n).
		//1+2+3+....n
		int expectedSum = (n * (n+1)) / 2;
		
		System.out.println("The Given Array is : ");
		for(int v : array)
			System.out.print(v+" ");
		
		int missingNo = expectedSum - arraySum;
		System.out.println("\nMissing Number is : "+missingNo);
	}
}
```

</p>
</details>

<details>
<summary>Write a program to Move All the Zeros to end of the Array.</summary>
<p>

```java
public class MoveAllZerosToEnd {
	public static void main(String[] args) {
		int array[] = {1, 0, 4, 3, 0, 0, 2, 0, 1, 0};
		System.out.println("The Given Array is :: ");
		for(int v : array)
			System.out.print(v+" ");
		
		int count = 0;
		for(int i=0;i<array.length;i++)
			if(array[i] != 0)
				array[count++] = array[i];
		
		while(count < array.length)
			array[count++] = 0;
		
		System.out.println("\nAfter moving all zeros to end of array :: ");
		for(int v : array)
			System.out.print(v+" ");
		
	}
}
```

</p>
</details>
	
<details>
<summary>Write a program to Rotate the Given array d times.</summary>
<p>

```java
public class ArrayRotation {
	public static void main(String[] args) {
		int arr[] = {1, 2, 3, 4, 5, 6};
		int d = 6;
		int n = arr.length;
		
		if(d > n)
			d = d-n;
		int new_arr[] = new int[n];
		int new_index = 0;
		for(int i=(n-d);i<n;i++,new_index++)
			new_arr[new_index] = arr[i];
		for(int i=0;i<(n-d);i++,new_index++)
			new_arr[new_index] = arr[i];
		
		System.out.println("Original Array ");
		System.out.println(Arrays.toString(arr));
		
		System.out.println("Array after rotation");
		System.out.println(Arrays.toString(new_arr));
	}
}
```

</p>
</details>
