<details open>
<summary>write a program that can print the number of prime numbers less than N and you are given a non-negative integer N</summary>
<p>

```java
import java.util.stream.IntStream;

public class Main {
    public static int countPrimes(int N) {
        return (int) IntStream.range(2, N)
                .filter(Main::isPrime)
                .count();
    }

    public static boolean isPrime(int num) {
        if (num < 2) {
            return false;
        }

        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) {
                return false;
            }
        }

        return true;
    }

    public static void main(String[] args) {
        int N = 20;
        int count = countPrimes(N);
        System.out.println("Number of prime numbers less than " + N + ": " + count);
    }
}

```

</p>
</details>


<details>
<summary>Given two binary strings a and b,Write a program to find their sum as a binary string and perform the binary addition operation on these values  </summary>
<p>

```java
public class Main {
    public static String addBinary(String a, String b) {
        int carry = 0; // Initialize carry to 0
        StringBuilder result = new StringBuilder(); // StringBuilder to build the result string

        // Pad the strings with leading zeros if necessary
        int maxLength = Math.max(a.length(), b.length());
        while (a.length() < maxLength)
            a = "0" + a;
        while (b.length() < maxLength)
            b = "0" + b;

        // Perform binary addition
        for (int i = maxLength - 1; i >= 0; i--) {
            int digitA = a.charAt(i) - '0';
            int digitB = b.charAt(i) - '0';
            int sum = digitA + digitB + carry;
            result.insert(0, sum % 2); // Append the result (sum modulo 2) to the left side
            carry = sum / 2; // Determine the carry-over value for the next addition
        }

        // Handle any remaining carry-over
        if (carry > 0)
            result.insert(0, carry);

        return result.toString();
    }

    public static void main(String[] args) {
        String a = "1010";
        String b = "1111";
        String sum = addBinary(a, b);
        System.out.println("Sum: " + sum);
    }
}

```

</p>
</details>



<details>
<summary>Write a Java program that moves all zeros to the end of an integer list while maintaining the relative order of the non-zero elements.</summary>
<p>

```java
import java.util.List;

public class Main {
    public static void moveZeroes(List<Integer> nums) {
        int nonZeroIndex = 0; // Pointer to keep track of the position to swap non-zero elements
        
        // Move all the non-zero elements to the beginning of the list
        for (int i = 0; i < nums.size(); i++) {
            if (nums.get(i) != 0) {
                nums.set(nonZeroIndex, nums.get(i));
                nonZeroIndex++;
            }
        }
        
        // Fill the remaining elements with zeros
        while (nonZeroIndex < nums.size()) {
            nums.set(nonZeroIndex, 0);
            nonZeroIndex++;
        }
    }
    
    public static void main(String[] args) {
        // Test case
        List<Integer> nums = List.of(0, 1, 0, 3, 12);
        System.out.println("Before: " + nums);
        
        moveZeroes(nums);
        
        System.out.println("After: " + nums);
    }
}


```

</p>
</details>
    
<details>
<summary>Write a Java program that finds the size (number of cells occupied) of the largest contiguous cross-section consisting of a single element type in a 2D matrix A. The matrix A represents a cross-section of a nuclear reactor with different types of elements present in each cell.</summary>
<p>

```java
public class LargestCrossSectionSize {
    public static int findLargestCrossSection(int[][] matrix) {
        int maxCount = 0;  // Size of the largest contiguous cross-section
        int rowCount = matrix.length;     // Number of rows
        int colCount = matrix[0].length;  // Number of columns

        // Initialize visited matrix to keep track of visited cells
        boolean[][] visited = new boolean[rowCount][colCount];

        // Iterate over each cell in the matrix
        for (int i = 0; i < rowCount; i++) {
            for (int j = 0; j < colCount; j++) {
                if (!visited[i][j]) {
                    int count = getCrossSectionSize(matrix, visited, i, j, matrix[i][j]);
                    if (count > maxCount) {
                        maxCount = count;
                    }
                }
            }
        }

        return maxCount;
    }

    private static int getCrossSectionSize(int[][] matrix, boolean[][] visited, int row, int col, int elementType) {
        int rowCount = matrix.length;     // Number of rows
        int colCount = matrix[0].length;  // Number of columns

        // If the cell is out of bounds, has a different element type, or has been visited, return 0
        if (row < 0 || row >= rowCount || col < 0 || col >= colCount || matrix[row][col] != elementType || visited[row][col]) {
            return 0;
        }

        visited[row][col] = true;  // Mark the cell as visited

        // Recursively check the neighboring cells
        int count = 1;
        count += getCrossSectionSize(matrix, visited, row - 1, col, elementType);  // Up
        count += getCrossSectionSize(matrix, visited, row + 1, col, elementType);  // Down
        count += getCrossSectionSize(matrix, visited, row, col - 1, elementType);  // Left
        count += getCrossSectionSize(matrix, visited, row, col + 1, elementType);  // Right

        return count;
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 1, 2, 3},
            {1, 1, 1, 3},
            {4, 4, 4, 4},
            {5, 5, 5, 6}
        };

        int largestCrossSectionSize = findLargestCrossSection(matrix);
        System.out.println("Size of the largest contiguous cross-section: " + largestCrossSectionSize);
    }
}



```

</p>
</details>

    
<details>
<summary>Write a program to form a high-performance group of software developers based on the number of projects completed and their respective salaries and calculate the group's reputation based on the sum of the salary for each group, we can use a similar approach as before. We can calculate the trust factor for each developer based on the number of projects completed and salary, and then use the trust factor to select the top N developers to form the group. We can then compute the sum of salaries for each group and find the group with the maximum total salaries </summary>
<p>

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Developer {
    private String name;
    private int salary;
    private int projectsCompleted;

    public Developer(String name, int salary, int projectsCompleted) {
        this.name = name;
        this.salary = salary;
        this.projectsCompleted = projectsCompleted;
    }

    public String getName() {
        return name;
    }

    public int getSalary() {
        return salary;
    }

    public int getProjectsCompleted() {
        return projectsCompleted;
    }
}

public class Main {
    public static void main(String[] args) {
        List<Developer> developers = new ArrayList<>();
        // Add the developer information to the list
        developers.add(new Developer("Developer A", 3000, 10));
        developers.add(new Developer("Developer B", 4000, 15));
        developers.add(new Developer("Developer C", 2500, 20));
        developers.add(new Developer("Developer D", 3500, 12));
        developers.add(new Developer("Developer E", 2000, 25));
        developers.add(new Developer("Developer F", 5000, 8));
        developers.add(new Developer("Developer G", 1500, 30));
        developers.add(new Developer("Developer H", 4500, 11));
        developers.add(new Developer("Developer I", 1000, 40));
        developers.add(new Developer("Developer J", 6000, 5));

        // Sort the developers by the number of projects completed and salary
        developers.sort(Comparator.comparingInt(Developer::getProjectsCompleted).reversed()
                                    .thenComparingInt(Developer::getSalary));

        // Create a group of developers with the most projects completed but low salary
        List<Developer> group = new ArrayList<>();
        for (Developer developer : developers) {
            if (developer.getSalary() < 3000) {
                group.add(developer);
            }
        }

        // Print the group's members
        System.out.println("Group Members:");
        for (Developer developer : group) {
            System.out.println(developer.getName());
        }
    }
}


```

</p>
</details>
