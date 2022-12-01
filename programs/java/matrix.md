<details open>
<summary>Print Hellow World Program.</summary>
<p>

```java
class App{  
    public static void main(String args[]){  
     System.out.println("Hello Java");  
    }  
}  
```

</p>
</details> 

<details>
<summary>Print Welcome to PC Program.</summary>
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

---
title: Use tabs to organize content
output: html_document
---

You can turn parallel sections to tabs in `html_document` output.

## Results {.tabset}

### Plots

We show a scatter plot in this section.

```{r, fig.dim=c(5, 3)}
par(mar = c(4, 4, .5, .1))
plot(mpg ~ hp, data = mtcars, pch = 19)
```

### Tables

We show the data in this tab.

```{r}
head(mtcars)
```
