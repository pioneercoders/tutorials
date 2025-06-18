<details open>
<summary>1️⃣ Write a program to count number of words in a string.</summary>
<p>

```java
public class CountWordsInString {
    
    public static int wordCount(String str) {
        int count = 0;
        boolean isWord = false;
        int endOfLine = str.length() - 1;

        for (int i = 0; i < str.length(); i++) {
            // check if the char is a letter
            if (str.charAt(i) != ' ' && i != endOfLine) {
                isWord = true;
            } else if (str.charAt(i) == ' ' || i == endOfLine) {
                if (isWord) {
                    count++;
                    isWord = false;
                }
            }
        }
        return count;
    }

    public static void main(String[] args) {
        String str = "    India Is My Country";
        System.out.println(wordCount(str) + " words.");
    }
}
```

</p>
</details>

<details>
<summary>2️⃣ Write a program to remove all white spaces from a string.</summary>
<p>

```java
public class RemoveAllSpaces {

    public static void main(String[] args) {
        String str = "India     Is My    Country";
        String result = str.replaceAll("\\s", "");
        System.out.println("Without spaces: " + result);
    }
}
```

</p>
</details>

<details>
<summary>3️⃣ Write a program to find duplicate characters in a string.</summary>
<p>

```java
import java.util.HashMap;
import java.util.Map;

public class DuplicateCharFinder {

    public void findDuplicates(String str) {
        Map<Character, Integer> charCount = new HashMap<>();

        for (char ch : str.toCharArray()) {
            if (ch != ' ') {
                charCount.put(ch, charCount.getOrDefault(ch, 0) + 1);
            }
        }

        System.out.println("Duplicate characters:");
        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            if (entry.getValue() > 1) {
                System.out.println("'" + entry.getKey() + "' appears " + entry.getValue() + " times");
            }
        }
    }

    public static void main(String[] args) {
        DuplicateCharFinder finder = new DuplicateCharFinder();
        finder.findDuplicates("India is my country");
    }
}
```

</p>
</details>

<details>
<summary>4️⃣ Write a program to convert string to integer and integer to string.</summary>
<p>

```java
public class StringToIntegerAndIntegerToString {

    public static void main(String[] args) {

        String str = "200";
        int num = 300;

        // String to Integer
        int intVal = Integer.parseInt(str);

        // Integer to String
        String strVal = Integer.toString(num);

        System.out.println("Converted to Integer: " + intVal);
        System.out.println("Converted to String: " + strVal);
    }
}
```

</p>
</details>

<details>
<summary>5️⃣ Write a program to print first non-repeated character from string.</summary>
<p>

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeatedChar {

    public static void main(String[] args) {
        String str = "India is my country";
        char result = findFirstNonRepeated(str);
        if (result != 0) {
            System.out.println("First non-repeated character: " + result);
        } else {
            System.out.println("No non-repeated character found.");
        }
    }

    public static char findFirstNonRepeated(String str) {
        Map<Character, Integer> countMap = new LinkedHashMap<>();

        for (char ch : str.toCharArray()) {
            if (ch != ' ') {
                countMap.put(ch, countMap.getOrDefault(ch, 0) + 1);
            }
        }

        for (Map.Entry<Character, Integer> entry : countMap.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }

        return 0;
    }
}
```

</p>
</details>
