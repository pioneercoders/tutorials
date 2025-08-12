#### 1.What is the difference between type aliases and interface in TypeScript? When would you use one over the other?

In TypeScript, both type aliases and interfaces can describe the shape of objects, but they have some key differences in capabilities, extendability, and usage scenarios.
Syntax & Basic Purpose
Interface
interface Person {
  name: string;
  age: number;
}

Type Alias
type Person = {
  name: string;
  age: number;
};

Both define the shape of an object, but type can also represent primitives, unions, intersections, tuples, etc., whereas interface is purely for object-like structures.

 2.Capabilities
| Feature                   | Interface              | Type Alias  |
| ------------------------- | ---------------------- | ----------- |
| **Describes objects**     | ✅                      | ✅           |
| **Describes functions**   | ✅                      | ✅           |
| **Describes tuples**      | ❌                      | ✅           |
| **Union types**           | ❌                      | ✅           |
| **Intersection types**    | ❌ (only via `extends`) | ✅           |
| **Primitives**            | ❌                      | ✅           |
| **Declaration merging**   | ✅                      | ❌           |
| **Extending other types** | ✅ (via `extends`)      | ✅ (via `&`) |

3.Extending
Interface extends interface

interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

Type alias extends type (intersection)
type Animal = { name: string };
type Dog = Animal & { breed: string };

4.Declaration Merging (Interface only)
Interfaces with the same name merge automatically.
interface User {
  name: string;
}
interface User {
  age: number;
}

// Merged type:
const u: User = { name: "John", age: 30 };
Type aliases cannot merge:
type User = { name: string };
type User = { age: number }; // ❌ Error: Duplicate identifier


 When to Use Which?
 Use interface when

You want to define object shapes that may need extension later.

You want declaration merging (e.g., extending library types).

You are modeling a domain with mostly structured data (objects & classes).
Use type when

You need unions, intersections, tuples, or primitives.

You want to compose complex types using operators like | or &.

You are defining function signatures or generic utility types.


#### 2.Explain the difference between unknown and any. Why is unknown safer?
In TypeScript, both unknown and any represent “could be anything,” but the big difference is in type safety.

1.Basic Definitions

any

Completely disables type checking for that variable.

You can do anything with it — no compiler errors.

Dangerous because mistakes slip through at compile time.
let value: any = "hello";
value.trim(); // ✅ No error
value();      // ✅ No error, but will crash at runtime if not a function

unknown

Means “type is unknown for now,” but you must check or assert its type before using it.

Forces type safety at compile time.
let value: unknown = "hello";
value.trim(); // ❌ Error: Object is of type 'unknown'

// Must narrow first:
if (typeof value === "string") {
  value.trim(); // ✅ Works after check
}


2.Why unknown is safer
| Feature                                    | `any` | `unknown`                   |
| ------------------------------------------ | ----- | --------------------------- |
| Can be assigned to anything                | ✅     | ❌ (only `unknown` or `any`) |
| Can call properties/methods without checks | ✅     | ❌                           |
| Requires type narrowing before usage       | ❌     | ✅                           |
| Type safety                                | ❌     | ✅                           |

3.When to Use Which

 Use unknown when

You’re dealing with external/unknown data (e.g., API responses, JSON.parse, event.data).

You want to force checks before usage.

Use any only when

You are in a temporary prototyping phase.

You truly cannot type the value yet and don’t care about type safety.

#### 3.How do readonly properties work in TypeScript? Can you make an array readonly?

In TypeScript, the readonly modifier is used to make properties immutable after they are assigned — meaning you can set them once (either during declaration or in the constructor), but you cannot reassign them later.

1.Readonly on Object Properties
class Person {
  readonly name: string;

  constructor(name: string) {
    this.name = name; // ✅ Allowed (initial assignment)
  }

  changeName(newName: string) {
    this.name = newName; // ❌ Error: Cannot assign to 'name' because it is a read-only property
  }
}

const p = new Person("Alice");
p.name = "Bob"; // ❌ Error

readonly works for:

Class properties

Object properties

Interface/type definitions

Readonly in Interfaces and Types
interface User {
  readonly id: number;
  name: string;
}

const u: User = { id: 1, name: "John" };
u.id = 2; // ❌ Error

Both approaches:

Prevent modifying methods (push, pop, splice, etc.).

Still allow reading values and using non-mutating methods (map, filter, etc.).

 Important Notes
readonly prevents reassignment of a property or array element, but does not make nested objects immutable.

If you want deep immutability, you’d need extra tooling (like Readonly<T> recursively).

#### 4.What is the difference between Partial<T>, Required<T>, Pick<T, K> and Omit<T, K> utility types?
In TypeScript, Partial<T>, Required<T>, Pick<T, K>, and Omit<T, K> are built-in utility types that help transform existing types without rewriting them.

1.Partial<T>
Makes all properties in T optional.

interface User {
  id: number;
  name: string;
  email: string;
}

type PartialUser = Partial<User>;
/*
type PartialUser = {
  id?: number;
  name?: string;
  email?: string;
}
*/

const u: PartialUser = { name: "Alice" }; // ✅ Allowed

Use case: When updating part of an object (e.g., patch updates).

2.Required<T>
Makes all properties in T required, even if they were optional.
interface User {
  id: number;
  name?: string;
}

type RequiredUser = Required<User>;
/*
type RequiredUser = {
  id: number;
  name: string;
}
*/

const u: RequiredUser = { id: 1, name: "Alice" }; // ✅ Must include all props

Use case: Enforcing completeness of an object (e.g., after validation).

3.Pick<T, K>
Creates a new type by picking only specific properties from T.

interface User {
  id: number;
  name: string;
  email: string;
}

type UserName = Pick<User, "id" | "name">;
/*
type UserName = {
  id: number;
  name: string;
}
*/

const u: UserName = { id: 1, name: "Alice" }; // ✅ Only id & name allowed

Use case: Selecting a subset of properties for specific operations (e.g., displaying minimal data).

4.Omit<T, K>
Creates a new type by removing specific properties from T.

5.Quick Comparison Table
| Utility Type  | What it does                  | Example                       |
| ------------- | ----------------------------- | ----------------------------- |
| `Partial<T>`  | Makes all properties optional | Update object partially       |
| `Required<T>` | Makes all properties required | Ensure full object is present |
| `Pick<T, K>`  | Keep only certain properties  | Minimal data type             |
| `Omit<T, K>`  | Remove certain properties     | Hide sensitive data           |

#### 5.What is a generic in TypeScript? Give an example.

A generic in TypeScript is a way to create reusable, type-safe code that works with multiple types without sacrificing type checking.

Think of it as a type parameter you can pass into a function, class, or interface — similar to how you pass a value parameter into a function.

1.Why Generics?

Without generics, you might use any for flexibility, but any loses type safety.
function identity(arg: any): any {
  return arg;
}

let result = identity("Hello"); // ✅ Works, but result is 'any'

2.With Generics

function identity<T>(arg: T): T {
  return arg;
}

let result1 = identity<string>("Hello"); // T = string
let result2 = identity<number>(42);      // T = number

Type is preserved — result1 is string, result2 is number.

3.Generic Function (Type Inference)
TypeScript can infer T automatically:
function identity<T>(arg: T): T {
  return arg;
}

let val = identity("Test"); // T inferred as string

4.Generic Interface
interface Box<T> {
  value: T;
}

let stringBox: Box<string> = { value: "Hello" };
let numberBox: Box<number> = { value: 123 };

5.Generic Class
class DataStore<T> {
  private data: T[] = [];
  
  add(item: T) {
    this.data.push(item);
  }
  
  getAll(): T[] {
    return this.data;
  }
}

const stringStore = new DataStore<string>();
stringStore.add("apple");

const numberStore = new DataStore<number>();
numberStore.add(42);

6.Generic Constraints
You can restrict what types are allowed:
function logLength<T extends { length: number }>(arg: T) {
  console.log(arg.length);
}

logLength("Hello"); // ✅ Works
logLength([1, 2, 3]); // ✅ Works
logLength(42); // ❌ Error: number has no 'length'

#### 6.What is the difference between a generic interface and a generic function?

The main difference between a generic interface and a generic function in TypeScript is where and how the type parameter (T) is defined and applied.

1.Generic Function
The type parameter is declared per function call.

Each call can use a different type for T.

Useful for operations where the type depends on the input.

function identity<T>(value: T): T {
  return value;
}

let a = identity<string>("Hello"); // T = string
let b = identity<number>(42);      // T = number

Here, T exists only inside this function, and you can pick a new T for each call.

2. Generic Interface
The type parameter is declared when you create an instance or implement it.

That type is fixed for the entire interface usage.

Useful for data structures or contracts that consistently use one type.
interface Box<T> {
  value: T;
  getValue(): T;
}

let stringBox: Box<string> = {
  value: "Hi",
  getValue() { return this.value; }
};

let numberBox: Box<number> = {
  value: 123,
  getValue() { return this.value; }
};

 Here, T is locked when you define stringBox or numberBox.

 3.Key Differences Table

 | Feature              | Generic Function                                                 | Generic Interface                                |
| -------------------- | ---------------------------------------------------------------- | ------------------------------------------------ |
| Type parameter scope | Per function call                                                | Per instance/implementation                      |
| Flexibility          | Can change `T` each call                                         | Fixed `T` for lifetime of the instance           |
| Best for             | Reusable operations (sorting, mapping, identity functions, etc.) | Data structures, API contracts, class blueprints |
| Example use case     | `map<T>(array: T[], callback: ...)`                              | `Repository<T>` for database entities            |

#### 7.What’s the difference between public, private, protected, and readonly in TypeScript classes?
In TypeScript classes, public, private, protected, and readonly are access modifiers (plus readonly is also an immutability modifier) that control how and where class members (properties/methods) can be accessed and/or modified.

1.public
Default if no modifier is specified.

Accessible anywhere: inside the class, subclasses, and outside the class.
class Person {
  public name: string; // default
  constructor(name: string) {
    this.name = name;
  }
}

const p = new Person("Alice");
console.log(p.name); // ✅ Accessible

2. private
Accessible only inside the same class.

Not accessible in subclasses or outside the class.
class Person {
  private ssn: string;
  constructor(ssn: string) {
    this.ssn = ssn;
  }
  getSSN() {
    return this.ssn; // ✅ Allowed
  }
}

const p = new Person("123-45-6789");
console.log(p.ssn); // ❌ Error

3.protected
Accessible inside the same class and in subclasses.

Not accessible outside the class hierarchy.
class Animal {
  protected type: string;
  constructor(type: string) {
    this.type = type;
  }
}

class Dog extends Animal {
  bark() {
    console.log(`Woof! I am a ${this.type}`); // ✅ Allowed in subclass
  }
}

const d = new Dog("Bulldog");
d.type; // ❌ Error: protected

4.readonly
Makes the property immutable after initialization.

Can be combined with public, private, or protected.

Can be set only in declaration or constructor.
class Person {
  readonly id: number;
  constructor(id: number) {
    this.id = id; // ✅ Allowed in constructor
  }
}

const p = new Person(1);
p.id = 2; // ❌ Error: read-only property

#### 8.What are intersection types (&) and union types (|)? Give examples of when you’d use them.

In TypeScript, intersection types (&) and union types (|) let you combine or allow multiple types in flexible ways — but they mean very different things.

1. Union Types (|)
"Either this type or that type"
A value can be one of several types.

let value: string | number;
value = "Hello"; // ✅ OK
value = 42;      // ✅ OK
value = true;    // ❌ Error

Common use cases:

Function parameters that accept multiple formats.

API responses with different possible shapes.
function printId(id: string | number) {
  console.log(`ID: ${id}`);
}

printId(101);      // ✅
printId("abc123"); // ✅

2.Intersection Types (&)
"Must satisfy all types at the same time"
A value must have all properties/methods from all combined types.
interface Name {
  name: string;
}
interface Age {
  age: number;
}

type Person = Name & Age;

const p: Person = {
  name: "Alice",
  age: 30
}; // ✅ Must have BOTH name and age

Common use cases:

Combining multiple interfaces into one.

type Developer = { skills: string[] };
type Manager = { teamSize: number };

type TechLead = Developer & Manager;

const lead: TechLead = {
  skills: ["TypeScript", "Angular"],
  teamSize: 5
};

3.Quick Analogy
Union (|) → "This OR that" — like a menu where you pick one dish.

Intersection (&) → "This AND that" — like a combo meal that includes everything.

 4.When to Use Each
 | Type                   | Use When...                                                    |                                                              |
| ---------------------- | -------------------------------------------------------------- | ------------------------------------------------------------ |
| \*\*Union (\`          | \`)\*\*                                                        | You want flexibility — value can be one of multiple options. |
| **Intersection (`&`)** | You want to merge multiple types into a single required shape. |                                                              |


#### 8.Explain mapped types with an example.
Mapped types in TypeScript let you create new types by transforming each property of an existing type according to a specific rule.

Think of them as a “loop” over the keys of a type that changes their modifiers (optional, readonly, required) or their value types.

interface User {
  id: number;
  name: string;
  email: string;
}

// Mapped type to make all properties readonly
type ReadonlyUser = {
  readonly [K in keyof User]: User[K];
};

const u: ReadonlyUser = { id: 1, name: "Alice", email: "a@example.com" };
u.name = "Bob"; // ❌ Error: Cannot assign to 'name' because it is a read-only property

Here:

K in keyof User iterates over "id" | "name" | "email".

User[K] gets the type of each property.

readonly modifier is applied to each property.

2. Built-in Mapped Types
TypeScript’s utility types (Partial<T>, Required<T>, Readonly<T>, Record<K, T>) are all built with mapped types.

Example: Partial<T> internally is like:
type Partial<T> = {
  [K in keyof T]?: T[K];
};

This makes all properties optional.

3.Custom Transformation Example
You can also transform value types:

type Stringify<T> = {
  [K in keyof T]: string;
};

type StringifiedUser = Stringify<User>;
/*
type StringifiedUser = {
  id: string;
  name: string;
  email: string;
}
*/
4.Why use mapped types?
They avoid repetitive code when modifying many properties.

They make your types DRY (Don’t Repeat Yourself).































