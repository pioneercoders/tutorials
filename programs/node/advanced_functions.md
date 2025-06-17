<details open>
<summary>1️⃣ Assign a function to a variable - Calculate bill total.</summary>
<p>

```javascript
// Function to calculate total bill (including tax)
var calculateBill = function(price, taxRate) {
    var total = price + (price * taxRate);
    return total;
};

var finalAmount = calculateBill(100, 0.05);
console.log("Total Bill: $" + finalAmount); // $105
```

</p>
</details>

<details>
<summary>2️⃣ Pass a function to another function - Apply discount or tax.</summary>
<p>

```javascript
// Higher-order function that applies pricing logic
function applyCalculation(amount, calculationFunction) {
    var result = calculationFunction(amount);
    return result;
}

var addTax = function(amount) {
    return amount + (amount * 0.18); // 18% tax
};

var applyDiscount = function(amount) {
    return amount - (amount * 0.1); // 10% discount
};

var taxed = applyCalculation(500, addTax);
console.log("Price with Tax: " + taxed); // 590

var discounted = applyCalculation(500, applyDiscount);
console.log("Price after Discount: " + discounted); // 450
```

</p>
</details>

<details>
<summary>3️⃣ Return a function from another function - Create multipliers.</summary>
<p>

```javascript
// Function returns another function that multiplies
function createMultiplier(multiplier) {
    return function(amount) {
        return amount * multiplier;
    };
}

var double = createMultiplier(2);
var triple = createMultiplier(3);

console.log("Double of 5:", double(5));   // 10
console.log("Triple of 5:", triple(5));   // 15
```

</p>
</details>

<details>
<summary>4️⃣ Arrow function - Calculate area of rectangle.</summary>
<p>

```javascript
// Arrow function for area
var getArea = (length, width) => {
    var area = length * width;
    return area;
};

console.log("Area:", getArea(10, 5)); // 50
```

</p>
</details>

<details>
<summary>5️⃣ IIFE - Initialize configuration settings.</summary>
<p>

```javascript
// Immediately invoked function to initialize settings
var settings = (function() {
    var config = {
        theme: "dark",
        layout: "grid"
    };
    console.log("App initialized with settings");
    return config;
})();

console.log(settings.theme); // dark
```

</p>
</details>

<details>
<summary>6️⃣ Callback Function - User registration flow.</summary>
<p>

```javascript
// Simulate user registration with a callback
function registerUser(username, callback) {
    console.log("Registering user:", username);
    // pretend registration is done
    callback();
}

function showWelcomeMessage() {
    console.log("Welcome! Registration successful.");
}

registerUser("john_doe", showWelcomeMessage);

// Output:
// Registering user: john_doe
// Welcome! Registration successful.
```

</p>
</details>
