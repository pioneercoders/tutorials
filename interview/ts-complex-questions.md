#### 1. What is the difference between interface extends and type intersection?

interface extends: Creates a new interface by inheriting from another.

type intersection (&): Combines multiple types into one.

interface A { a: string; }
interface B { b: number; }
interface C extends A, B {}

type D = A & B; // Same as above, but works with any type

#### 2.How do you enforce type safety in a function that accepts both strings and numbers but behaves differently for each?
You can use function overloads.
function processInput(input: string): string;
function processInput(input: number): number;
function processInput(input: string | number): string | number {
  return typeof input === "string" ? input.toUpperCase() : input * 2;
}

processInput("hello"); // Returns string
processInput(5);       // Returns number

Key point: Overloads allow precise type inference for different input types.

#### 3.How does TypeScript handle never type and when would you use it?
never represents values that never occur.

Used in:

Functions that throw errors

Exhaustive type checking

function throwError(message: string): never {
  throw new Error(message);
}

type Shape = { kind: "circle" } | { kind: "square" };
function area(shape: Shape) {
  if (shape.kind === "circle") { /* ... */ }
  else if (shape.kind === "square") { /* ... */ }
  else {
    const _exhaustive: never = shape; // Compile error if new shape type is added
  }
}

Key point: never ensures you handle all possible cases.

#### 4.How do you make a property read-only but only during runtime, not at compile time?

Use Object.freeze() with a mutable type.
type Config = {
  url: string;
};

const config: Config = { url: "https://api.com" };
Object.freeze(config);

config.url = "https://new.com"; // Runtime error, not compile-time

Key point: Compile-time immutability uses readonly; runtime immutability uses Object.freeze().

#### 5.What is the difference between keyof and typeof?
typeof: Gets the type of a value.

keyof: Gets all keys of a type as a union.

const person = { name: "John", age: 25 };

type PersonType = typeof person; // { name: string; age: number; }
type PersonKeys = keyof PersonType; // "name" | "age"

#### 6.How can you restrict a generic type to accept only certain keys of another type?
interface User {
  id: number;
  name: string;
  age: number;
}

function getUserProperty<T extends keyof User>(key: T, user: User): User[T] {
  return user[key];
}

const u: User = { id: 1, name: "John", age: 30 };
const nameValue = getUserProperty("name", u); // string

#### 7.How does type narrowing work in TypeScript?
Type narrowing in TypeScript is the process where the compiler refines a variable’s type to something more specific than its declared type, based on control flow analysis and type guards.

Think of it like detective work:
TypeScript starts with a broad suspect list (union type) and, as your code provides clues, it eliminates impossible types until it’s sure who’s left.

How it works
Start: You declare a variable with a union or broad type.

Evidence: You use checks (like typeof, instanceof, equality checks, truthiness) or custom type guards.

Refinement: TypeScript “narrows” the type within that code branch.

function printLength(value: string | number) {
  if (typeof value === "string") {
    // value is narrowed to string here
    console.log(value.length);
  } else {
    // value is narrowed to number here
    console.log(value.toFixed(2));
  }
}

Common Ways to Narrow Types
1️⃣ typeof narrowing
if (typeof x === "boolean") {
  // x is boolean here
}

2️⃣ instanceof narrowing
if (obj instanceof Date) {
  // obj is Date
}

3️⃣ Equality checks
if (status === "success") {
  // status is "success" literal type
}

4️⃣ Truthiness checks
if (value) {
  // value is not null/undefined/false/0/""
}

5️⃣ Custom type guards
A type guard is a function that returns a boolean and has a return type in the form parameterName is Type.
type Cat = { meow: () => void };
type Dog = { bark: () => void };

function isCat(animal: Cat | Dog): animal is Cat {
  return (animal as Cat).meow !== undefined;
}

function makeSound(animal: Cat | Dog) {
  if (isCat(animal)) {
    animal.meow(); // animal is Cat here
  } else {
    animal.bark(); // animal is Dog here
  }
}

Narrowing happens per branch — outside the branch, the type returns to its original form.

The compiler follows the logical flow of your code to deduce types.

Type narrowing helps avoid runtime errors by catching impossible operations at compile time.



















