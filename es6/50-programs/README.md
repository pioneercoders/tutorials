<details>
    <summary> Write a program to filter the products based on property and value.</summary>
    <p>
        
```javascript
var products = [{"id":1,"name":"Redmi Note 8","brand":"xiomi","price":10000,"category":"electronics"},
    {"id":2,"name":"Lenevo K10","brand":"Lenevo","price":8000,"category":"electronics" },
    {"id":3,"name":"Realme 5s","brand":"Realme","price":9999,"category":"electronics"},
    {"id":4,"name":"AC","brand":"LG","price":25000,"category":"homeAppliances"},
    {"id":5,"name":"Refrigerator","brand":"Samsung","price":20000,"category":"homeAppliances"},
    {"id":6,"name":"Indigo Cs","brand":"Tata","price":700000,"category":"cars"},
    {"id":7,"name":"Hornet 160R","brand":"Honda","price":120000,"category":"bikes"}
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
</p>
</details>


<details>
    <summary> Write a program to find the buses list based on source and dest locations.</summary>
    <p>
        
```javascript
var findBuses = function(busList,source,destination,)// Find the Buses As per the source and destination
{
    var newBusList=[];
    for(var i=0;i<busList.length;i++) {
        var tempBus=busList[i];
        if(tempBus.source.localeCompare(source) ==0 && 
            tempBus.destination.localeCompare(destination)==0) {
            newBusList.push(tempBus);
        }
    }
    return newBusList;
}

var buses=[{BusNumber:"12JI83T5",operator:"RedBus",source:"Hyderabad",destination:"Bangalore",price:470,startTime:"7AM",endTime:"8Pm"},
{BusNumber:"7U12UKJE",operator:"AbhiBus",source:"Bangalore",destination:"Hyderabad",price:540,startTime:"8AM",endTime:"8Pm"},
{BusNumber:"KL9OMJER",operator:"Travels",source:"Mumbai",destination:"Bangalore",price:1200,startTime:"9AM",endTime:"9PM"},
{BusNumber:"T45JIEK",operator:"MKT",source:"CHENNAI",destination:"Hyderabad",price:1450,startTime:"9AM",endTime:"9PM"},
{BusNumber:"12JI8343",operator:"RedBus",source:"Hyderabad",destination:"Bangalore",price:1000,startTime:"7AM",endTime:"8Pm"},
{BusNumber:"12JKU4ER",operator:"Yalls",source:"Hyderabad",destination:"Bangalore",price:2000,startTime:"9AM",endTime:"8Pm"},
{BusNumber:"12JKIU89",operator:"RedBu",source:"Hyderabad",destination:"Bangalore",price:1280,startTime:"10AM",endTime:"8Pm"}];

var newListOfBus=findBuses(buses,"Hyderabad","Bangalore");
console.log("Final List => ", newListOfBus);

```
</p>
</details>
