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



