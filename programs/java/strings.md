### Write Programs
<details open>
<summary>1) Write a program to count number of words in a string.</summary>
<p>
    
```java
public class CountWordsinString {
		/* static Method for Count*/ 
	 static int wordCount(String str){  
       int count=0;  
   
         char ch[]= new char[str.length()];     
         for(int i=0;i<str.length();i++){  
            ch[i]= str.charAt(i);  
            if( ((i>0)&&(ch[i]!=' ')&&(ch[i-1]==' ')) || ((ch[0]!=' ')&&(i==0)) )  
            count++;  
         	}  
         return count;  
     }  
   public static void main(String[] args) {  
       String str ="    India Is My Country";  
      System.out.println(wordCount(str) + " words.");	
	}

} 
```

</p>
</details> 

<details>
<summary>2) Write a program to remove all white spaces from a string.</summary>
<p>
    
```java
public class RemoveAllSpaces {
	 
	    public static void main(String[] args) {  
	        String strg = "India     Is My    Country";   
	        String Str = strg.replaceAll("\\s", ""); 
	        System.out.println(Str);
	    }  
	}  
```
 
</p>
</details> 

<details>
<summary>3) Write a program to find duplicate characters in a string.</summary>
<p>

```java
package com.string.programs;
import java.util.HashMap;  
import java.util.Map;  
import java.util.Set;  

public class DuplicateCharFinder {  
	
	/*method to find delicate */
    public void findIt(String str) {  
    	
        Map<Character, Integer> baseMap = new HashMap<Character, Integer>(); 
        
        /*converting to character Array*/
        
        char[] charArray = str.toCharArray(); 
        
         /*looping the each char in array*/
        
        for (Character ch : charArray) {  
            if (baseMap.containsKey(ch)) {  
                baseMap.put(ch, baseMap.get(ch) + 1);  
            }
            else {  
                baseMap.put(ch, 1);  
            }  
        }  
        
        
        Set<Character> keys = baseMap.keySet();  
        
        for (Character ch : keys) {  
            if (baseMap.get(ch) > 1) {  
                System.out.println(ch + "  is " + baseMap.get(ch) + " times");  
            }  
        }  
    }  
   
    public static void main(String a[]) {  
    	
    	/*creating the object of Duplicate Array*/
    	
        DuplicateCharFinder dcf = new DuplicateCharFinder();  
        dcf.findIt("India is my country");  
    }  
}  
```

</p>
</details> 

<details>
<summary>4) Write a program to convert string to integer and integer to string.</summary>
<p>
    
```java
public class StringToIntegerandIntegerToString {
	
	public static void main(String args[]){  
		
		String str="200";  
		int i=300; 
		/*converting string to int using valueofmethod()*/
		
		Integer a=Integer.valueOf(str); 
		
		/*converting intiger to string to*/
		
		String st=String.format("%d",i);    
		
		System.out.println(a);  
		System.out.println(st);
	}
}
```
    
</p>
</details> 

<details>
<summary>5) Write a program to print first non repeated character from String.</summary>
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
