#### 1.What is TypeScript, and how is it different from JavaScript?
TypeScript is an open-source programming language developed and maintained by Microsoft.
It’s basically a superset of JavaScript — which means any valid JavaScript code is also valid TypeScript code — but it adds extra features, the biggest being static typing.

Key Differences Between TypeScript and JavaScript
| Feature                   | JavaScript                                          | TypeScript                                                                        |
| ------------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------- |
| **Typing**                | Dynamically typed (types are determined at runtime) | Statically typed (types are checked at compile time)                              |
| **Compilation**           | Interpreted directly by browsers/Node.js            | Needs to be compiled (transpiled) to JavaScript before running                    |
| **Error Detection**       | Errors are found at runtime                         | Many errors are caught during compile time                                        |
| **Language Features**     | Standard ECMAScript features                        | All JavaScript features **+** type annotations, interfaces, enums, generics, etc. |
| **IDE Support**           | Limited IntelliSense and refactoring support        | Excellent IntelliSense, autocompletion, and refactoring due to type information   |
| **Use in Large Projects** | Can become hard to maintain as it grows             | Easier to scale and maintain due to strong typing and tooling support             |


#### 2.How do you declare a variable with a type in TypeScript?
In TypeScript, you declare a variable with a type by adding a type annotation after the variable name using a colon (:).

let variableName: type = value;

(or)

const variableName: type = value;

#### 3.What is the difference between let, const, and var in TypeScript?

In TypeScript (and modern JavaScript), let, const, and var are all used to declare variables,
but they differ in scope, reassignment rules, and hoisting behavior.
1. Scope

| Keyword | Scope           | Meaning                                                      |
| ------- | --------------- | ------------------------------------------------------------ |
| `var`   | Function-scoped | Available throughout the entire function where it’s declared |
| `let`   | Block-scoped    | Available only within the block `{}` where it’s declared     |
| `const` | Block-scoped    | Available only within the block `{}` where it’s declared     |

2. Reassignment

| Keyword | Can Reassign?                          | Can Re-declare in same scope? |
| ------- | -------------------------------------- | ----------------------------- |
| `var`   | ✅ Yes                                  | ✅ Yes                         |
| `let`   | ✅ Yes                                  | ❌ No                          |
| `const` | ❌ No (must be assigned at declaration) | ❌ No                          |


#### 4.What is the purpose of type annotations in TypeScript?
The purpose of type annotations in TypeScript is to explicitly tell the compiler what type of data a variable, function parameter, or return value should hold.

They help catch errors early (at compile time) and make the code more readable, maintainable, and predictable.

Type annotations act like labels that tell TypeScript (and other developers) the shape and type of data you intend to use, ensuring safer and more maintainable code.

#### 5.Name some basic data types in TypeScript.
Some basic data types in TypeScript are:

| Data Type       | Description                                                             | Example                                                 |
| --------------- | ----------------------------------------------------------------------- | ------------------------------------------------------- |
| **`number`**    | Represents numeric values (integer, float, hex, binary, octal)          | `let age: number = 25;`                                 |
| **`string`**    | Represents text values                                                  | `let name: string = "Keerthi";`                         |
| **`boolean`**   | Represents `true` or `false`                                            | `let isActive: boolean = true;`                         |
| **`null`**      | Represents an explicitly empty value                                    | `let data: null = null;`                                |
| **`undefined`** | Represents a variable with no value assigned                            | `let value: undefined = undefined;`                     |
| **`any`**       | Can store any type (disables type checking)                             | `let randomValue: any = "hello";`                       |
| **`void`**      | Used for functions that don’t return a value                            | `function log(): void { console.log("Hello"); }`        |
| **`unknown`**   | Type-safe alternative to `any`; must check before use                   | `let data: unknown = 10;`                               |
| **`never`**     | Represents a value that never occurs (e.g., function that throws error) | `function fail(): never { throw new Error("Error!"); }` |

#### 6.How do you declare an array in TypeScript?

In TypeScript, you can declare an array in two main ways — by specifying the element type either with square brackets ([]) or with a generic type (Array<type>).

1. Using Square Brackets ([])
  ```typescript
let numbers: number[] = [1, 2, 3, 4];
let names: string[] = ["haswin", "devansh", "Anu"];
```
2. Using Generic Array Type (Array<type>)

let numbers: Array<number> = [1, 2, 3, 4];
let names: Array<string> = ["haswin", "devansh", "Anu"];

3.Array with Multiple Types (Union Type)

let mixed: (number | string)[] = [1, "two", 3, "four"];

4. Readonly Array
let colors: readonly string[] = ["red", "green"];
// colors.push("blue"); ❌ Error

5.Tuple (Fixed Length & Types)
let person: [string, number] = ["haswin", 25];

If you know the type of elements, always specify it — it helps TypeScript catch errors early and improves IntelliSense.

#### 7.How do you define a tuple in TypeScript?

In TypeScript, a tuple is a special type of array where:

The number of elements is fixed

The type of each element is known and can be different

Syntax:
let tupleName: [type1, type2, ..., typeN] = [value1, value2, ..., valueN];

Example:
let person: [string, number, boolean] = ["Keerthi", 25, true];

console.log(person[0]); // "Keerthi"
console.log(person[1]); // 25
console.log(person[2]); // true

Arrays can have any number of elements of the same type,
while tuples have a fixed length and predetermined types for each position.

#### 8.How do you define an arrow function in TypeScript?
In TypeScript, an arrow function is defined using the => syntax, just like in JavaScript,
but you can add type annotations for parameters and the return value.


 Why use Arrow Functions in TypeScript?

Shorter syntax

Automatically binds this (doesn’t change this context)

Works well with callbacks & functional programming

Syntax

const functionName = (param1: Type1, param2: Type2): ReturnType => {
  // function body
};

Example
const add = (a: number, b: number): number => {
  return a + b;
};

console.log(add(5, 3)); // 8

Single-Line Arrow Function (Implicit Return)
const multiply = (x: number, y: number): number => x * y;

#### 9.What is function overloading in TypeScript?

Function overloading in TypeScript means you can define multiple function signatures for a single function,
so the same function name can handle different parameter types or counts, but still provide type safety.

How It Works
You write multiple function signatures (overload declarations) with different parameter and/or return types.

You write one implementation that handles all cases.

TypeScript will check at compile time that calls match one of the declared signatures.

#### 10.What is the difference between interface and type in TypeScript?

In TypeScript, both interface and type are used to define the shape (structure) of data,
but they have some differences in capabilities, extension, and usage.

1. Basic Similarity
Both can define object structures:
interface Person {
  name: string;
  age: number;
}

type PersonType = {
  name: string;
  age: number;
};

2. Key Differences

| Feature                      | `interface`                                                                                    | `type`                                                                      |
| ---------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Extension / Inheritance**  | Can **extend** other interfaces or multiple interfaces (`extends`)                             | Can **intersect** with other types using `&`                                |
| **Merging**                  | Supports **declaration merging** (can define the same interface multiple times and they merge) | Cannot be re-declared; no merging                                           |
| **Usage**                    | Best for defining object shapes, class contracts                                               | Can represent **objects, primitives, unions, tuples, function types**, etc. |
| **Complex Types**            | Limited to describing objects, arrays, and functions                                           | More flexible — can describe unions, intersections, conditional types       |
| **Implements (in classes)**  | ✅ Yes                                                                                          | ✅ Yes                                                                       |
| **Extending Built-in Types** | ✅ Easier with `interface`                                                                      | Possible, but not as straightforward                                        |


Rule of Thumb
Use interface when defining object shapes or class contracts, especially when you expect them to be extended or merged.

Use type when you need unions, intersections, or complex type expressions.

#### 11.What is the readonly modifier in TypeScript?

The readonly modifier in TypeScript is used to make a property immutable — meaning it can only be assigned a value once (either during declaration or in the constructor, if it’s in a class).
1.For Object Properties
When used in interfaces or type aliases, readonly prevents changing the property after it’s set.
interface Person {
  readonly name: string;
  age: number;
}

const p: Person = { name: "Haswin", age: 25 };

p.age = 26;      // ✅ OK
// p.name = "Ravi"; // ❌ Error: Cannot assign to 'name' because it is a read-only property

2.For Arrays
TypeScript provides readonly arrays that cannot be modified.
let colors: readonly string[] = ["red", "green", "blue"];

// colors.push("yellow"); // ❌ Error
// colors[0] = "pink";    // ❌ Error

3.For Class Properties
readonly in a class means the property can be assigned only once, inside the constructor or at declaration.
class Car {
  readonly model: string;
  
  constructor(model: string) {
    this.model = model; // ✅ Allowed
  }
}

const c = new Car("Tesla");
// c.model = "BMW"; // ❌ Error

readonly only prevents reassignment;
it does not make nested objects immutable.

If you need deep immutability, you need Readonly<T> utility type or external libraries.






