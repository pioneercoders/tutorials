```javascript
var products = [
    {
        "id":1,
        "name":"Redmi Note 8",
        "brand":"xiomi",
        "price":10000,
        "category":"electronics"
    },
    {
       "id":2,
        "name":"Lenevo K10",
        "brand":"Lenevo",
        "price":8000,
        "category":"electronics" 
    },
    {
        "id":3,
        "name":"Realme 5s",
        "brand":"Realme",
        "price":9999,
        "category":"electronics"
    },
    {
        "id":4,
        "name":"AC",
        "brand":"LG",
        "price":25000,
        "category":"homeAppliances"
    },
    {
        "id":5,
        "name":"Refrigerator",
        "brand":"Samsung",
        "price":20000,
        "category":"homeAppliances"
    },
    {
        "id":6,
        "name":"Indigo Cs",
        "brand":"Tata",
        "price":700000,
        "category":"cars"
    },
    {
        "id":7,
        "name":"Hornet 160R",
        "brand":"Honda",
        "price":120000,
        "category":"bikes"
    }
];


function filter(arr, prop, val) {
    let filteredProducts = [];
    for(var i=0; i<arr.length; i++){
       if(arr[i][prop] === val){
           filteredProducts.push(products[i]);
       }
    }
    return filteredProducts;
};

var filteredProducts = filter(products, "brand", "Honda");
console.log(filteredProducts);
```
