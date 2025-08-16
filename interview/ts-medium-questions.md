#### 1.Difference between interface and abstract class in TypeScript.
In TypeScript, both interfaces and abstract classes are used to define contracts, but they serve different purposes.

--> An interface is purely a blueprint – it only defines the structure of properties and methods, without any implementation. A class can implement multiple interfaces, so it’s mainly used when we just want to enforce shape or contract across different classes.

--> On the other hand, an abstract class can have both abstract methods (without body) and concrete methods (with implementation). It cannot be instantiated directly, but it allows us to share common logic across subclasses. A class can extend only one abstract class.

For example, if I need all animals to have a makeSound() method but also want to provide a default move() method, I’d use an abstract class. If I just want to say “any class that is an Animal must have name and makeSound()”, I’d use an interface.

#### 2.What is union type and intersection type? Give examples.

1.Union Type

A union type allows a variable to hold one of several types.

Example :
```typescript
let value: string | number;

value = "Hello"; 
value = 42;       
// value = true;  
```

2.Intersection Type

An intersection type combines multiple types into one.

```typescript
type Person = { name: string };
type Employee = { employeeId: number };

type Staff = Person & Employee;

const staffMember: Staff = {
  name: "Keerthi",
  employeeId: 123
};
```
#### 3.Explain generics in TypeScript. Why are they useful?

Generics in TypeScript let us create reusable and type-safe components. Instead of using any, we pass types as parameters, which gives flexibility while preserving type safety. For example, a generic function identity<T>(value: T): T can work with both strings and numbers without losing type information.

Example without Generics
```typescript
function identity(value: any): any {
  return value;
}

let a = identity("Hello"); // returns string, but TS thinks it's `any`
a.toUpperCase(); // works, but not type-safe
```

Example with Generics

```typescript
function identity<T>(value: T): T {
  return value;
}

let a = identity<string>("Hello"); // type = string
a.toUpperCase(); 

let b = identity<number>(42); // type = number
// b.toUpperCase(); // error: number doesn’t have toUpperCase

```
#### 4.What is type assertion in TypeScript? How is it different from type casting?
Type assertion in TypeScript is a way to tell the compiler to treat a value as a specific type. It doesn’t change the actual data at runtime, it only affects type checking.
This is different from type casting in languages like Java or C#, where casting actually converts the value into another type at runtime.

#### 5.Explain declaration merging in TypeScript.

Declaration Merging happens when TypeScript combines multiple declarations with the same name into a single definition.
This allows us to extend existing types, interfaces, namespaces, or modules.

For example, if two interfaces User are declared separately, TypeScript merges their properties. It also works with namespaces and enums. This is especially useful for extending existing libraries or splitting large type definitions.

#### 6.What is a tuple in TypeScript? How is it different from an array?
A tuple in TypeScript is like a fixed-length, ordered array where each element has a specific type.
Unlike arrays, which usually store elements of the same type and have dynamic length, tuples enforce a strict structure. For example, [string, number] means the first element must be a string and the second a number.

#### 7.What is structural typing in TypeScript?

TypeScript uses structural typing, which means compatibility is based on the shape of the object rather than the name of the type. If two types have the same properties and methods, they are considered compatible. For example, an object with { name: string; age: number } can be assigned to both Person and User interfaces, even if they are defined separately.

#### 8.Explain keyof and typeof operators in TypeScript.

In TypeScript, 
--> typeof gets the type of a variable or object. For example, type T = typeof user creates a type based on the structure of user.
--> keyof gets the union of keys of a type. For example, keyof Person gives "name" | "age" | "location".
They’re often combined: keyof typeof obj gives all keys of an object, which is useful for type-safe property access.


