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
    <summary> Write a program to find the bus list based on source and dest locations.</summary>
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


<details>
    <summary> Write a program to find the tax calculation.</summary>
    <p>
        
```javascript
/*
    Tax Calculator
    - £0 to £10k is taxed at 0%
    - £10,001 to £35k is taxed at 20%
    - £35,001 to £100,000 is taxed at 40%
    - £100k plus is taxed at 50%
*/

var calculateTax = function(amt) {
  var income = parseFloat(amt);
  let t = calcTaxes(income);
  console.log(t);
  function calcTaxes(amount){
  var calculate = 0;
  if(amount > 100000){
      tax = ((amount - 100000)*.50 + (100000-35001)*.40 + (35000-10001)*.20).toFixed(2);
      taxPrint = 'Tax Payable: £' + tax;
      salaryaftertax = (income - tax).toFixed(2);
      salaryaftertaxPrint = ' Salary After Tax: £' + salaryaftertax;
      percentagebracket1 = ((10000/amount)*100).toFixed(1);
      percentagebracket2 = ((24999/amount)*100).toFixed(1);
      percentagebracket3 = ((64999/amount)*100).toFixed(1);
      percentagebracket4 = (((amount-100000)/amount)*100).toFixed(1);
      percentagebracketPrint = ' See your percentage breakdown of salary by tax band: ' + percentagebracket1 + '% between £0 to £10k, ' + percentagebracket2 + '% between £10,001 to £35k, ' + percentagebracket3 + '% between £35,001 to £100k and ' + percentagebracket4 + '% across the £100k+ bracket';
      taxband1 = 0;
      taxband2 = ((35000-10001)*.20).toFixed(2);
      taxband3 = ((100000-35001)*.40).toFixed(2);
      taxband4 = ((amount - 100000)*.50).toFixed(2);
      taxbandPrint = ' and, here is your breakdown of tax paid at each band: £' + taxband1 + ' at 0%, £' + taxband2 + ' at 20%, £' + taxband3 + ' at 40% and £' + taxband4 + ' at 50%.';
  }
  else if( amount > 35001){
      tax = ((amount - 35001)*.40 + (35000-10001)*.20).toFixed(2);
      taxPrint = 'Tax Payable: £' + tax;
      salaryaftertax = (income - tax).toFixed(2);
      salaryaftertaxPrint = ' Salary After Tax: £' + salaryaftertax;
      percentagebracket1 = ((10000/amount)*100).toFixed(1);
      percentagebracket2 = ((24999/amount)*100).toFixed(1);
      percentagebracket3 = (((amount-35001)/amount)*100).toFixed(1);
      percentagebracketPrint = ' See your percentage breakdown of salary by tax band: ' + percentagebracket1 + '% between £0 to £10k, ' + percentagebracket2 + '% between £10,001 to £35k and ' + percentagebracket3 + '% between £35,001 to £100k';
      taxband1 = 0;
      taxband2 = ((35000-10001)*.20).toFixed(2);
      taxband3 = ((amount-35001)*.40).toFixed(2);
      taxbandPrint = ' and, here is your breakdown of tax paid at each band: £' + taxband1 + ' at 0%, £' + taxband2 + ' at 20% and £' + taxband3 + ' at 40%.';
  }
  else if(amount > 10001){
      tax = ((amount - 10001)*.20).toFixed(2);
      taxPrint = 'Tax Payable: £' + tax;
      salaryaftertax = (income - tax).toFixed(2);
      salaryaftertaxPrint = ' Salary After Tax: £' + salaryaftertax;
      percentagebracket1 = ((10000/amount)*100).toFixed(1);
      percentagebracket2 = (((amount-10001)/amount)*100).toFixed(1);
      percentagebracketPrint = ' See your percentage breakdown of salary by tax band: ' + percentagebracket1 + '% between £0 to £10k and ' + percentagebracket2 + '% between £10,001 to £35k';
      taxband1 = 0;
      taxband2 = ((amount-10001)*.20).toFixed(2);
      taxbandPrint = ' and, here is your breakdown of tax paid at each band: £' + taxband1 + ' at 0% and £' + taxband2 + ' at 20%.';
  }
  else if(amount > 0){
       tax = amount*0;
       taxPrint = 'Tax Payable: £' + tax;
       salaryaftertax = (income - tax).toFixed(2);
       salaryaftertaxPrint = ' Salary After Tax: £' + salaryaftertax;
       percentagebracket1 = 100;
       percentagebracketPrint = ' See your percentage breakdown of salary by tax band: ' + percentagebracket1 + '% between £0 to £10k';
       taxband1 = 0;
       taxbandPrint = ' and, here is your breakdown of tax paid at each band: £' + taxband1 + ' at 0%.';
  }
  else {
    taxPrint = 'n/a';
    salaryaftertaxPrint = ' n/a';
    percentagebracketPrint = ' n/a';
    taxbandPrint = ' n/a'
  }
  return [taxPrint, salaryaftertaxPrint, percentagebracketPrint, taxbandPrint];
}}

calculateTax(1000000);
```
</p>
</details>



<details>
    <summary> Write a program to calculate the areas of various geometrical shapes.</summary>
    <p>
        
```javascript
/**
 *  Square of side a : Area = a2(asqure)
    Rectangle of length 'I' and width ‘w’: Area = w x I
    Circle of radius ‘r’: Area = Pi x r2 (rsquare)
    Triangle of base ‘b’ and height ‘h’: Area = 0.5 x b x h
 * @param {*} shape 
 * @param {*} values 
 */
var calculateArea = function(shape, values){
      let area;
      switch(shape) {
        case 'square':
          console.log("It's a square with a=" +values[0]);
          area =values[0]*values[0];
          break;
        case 'rectangle':
          console.log("It's a rectangle with a=" + values[0] + " and b=" + values[1]);
          area = values[0] * values[1];
          break;
        case 'circle':
          console.log("It's a circle with r=" + values[0]);
          area = values[0]*values[0] * 3.14;
          break;
        case 'triangle':
          console.log("It's a triangle with b=" + values[0]+ " and h=" + values[1] )
          area = 0.5 * values[0]*values[1];
          break;
        default:
            area = -1
          break;
      }
      return area;
  }

  let getAreas = (shapes, values_arr) => {
    for(let i= 0; i < shapes.length; i++) {
        let area = calculateArea(shapes[i], values_arr[i]);
        console.log(`area of ${shapes[i]} is ${area}`);
    }
  };


  let shapes = ["square", "rectangle", "circle", "triangle"];
  let values_arr = [[2], [3, 4], [5], [2, 4]];
  getAreas(shapes, values_arr)

```
    </p>
</details>
