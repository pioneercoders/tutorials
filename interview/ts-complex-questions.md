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




















