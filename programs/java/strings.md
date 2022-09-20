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
class App{  
    public static void main(String args[]){  
     System.out.print("Welcome to PC.");  
    }  
}  
```
    
</p>
</details> 

<details>
<summary>3) Write a program to find duplicate characters in a string.</summary>
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

<details>
<summary>4) Write a program to convert string to integer and integer to string.</summary>
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
