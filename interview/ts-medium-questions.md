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
a.toUpperCase(); // ✅ safe

let b = identity<number>(42); // type = number
// b.toUpperCase(); ❌ error: number doesn’t have toUpperCase

```


