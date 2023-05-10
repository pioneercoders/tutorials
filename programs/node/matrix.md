<details open>
<summary>Write a program for Matrix Multiplication.</summary>
<p>

```javascript
    let r = 2;
    let c = 2;
    const mA = [[1, 2], [3, 4]];
    const mB = [[1,-1], [2,-2]];
    const mC = [[],[]];

    for(let i=0;i<r;i++)    
    {    
        for(let j=0;j<c;j++)    
        {    
            mC[i][j]=0;    
            for(let k=0;k<c;k++)    
            {    
                mC[i][j]= mC[i][j] + mA[i][k]*mB[k][j];    
            }    
        }    
    }   

    console.log(mC);
```

</p>
</details>
