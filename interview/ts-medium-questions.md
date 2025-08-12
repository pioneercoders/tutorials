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

