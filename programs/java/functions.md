### Sample Programs
<details open>
<summary>Write function to find given number is even or odd.</summary>
<p>

```java
class App{  
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
class App{  
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
