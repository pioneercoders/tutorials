#### 1.Difference between interface and abstract class in TypeScript.
In TypeScript, both interfaces and abstract classes are used to define contracts, but they serve different purposes.

--> An interface is purely a blueprint – it only defines the structure of properties and methods, without any implementation. A class can implement multiple interfaces, so it’s mainly used when we just want to enforce shape or contract across different classes.

--> On the other hand, an abstract class can have both abstract methods (without body) and concrete methods (with implementation). It cannot be instantiated directly, but it allows us to share common logic across subclasses. A class can extend only one abstract class.

For example, if I need all animals to have a makeSound() method but also want to provide a default move() method, I’d use an abstract class. If I just want to say “any class that is an Animal must have name and makeSound()”, I’d use an interface.

#### 2.What is union type and intersection type? Give examples.

1.Union Type

A union type allows a variable to hold one of several types.

Example :

```ts
let value: string | number;

value = "Hello";  // ✅ valid
value = 42;       // ✅ valid
// value = true;  // ❌ invalid (not part of union)
``

2.Intersection Type

An intersection type combines multiple types into one.

```ts
type Person = { name: string };
type Employee = { employeeId: number };

type Staff = Person & Employee;

const staffMember: Staff = {
  name: "Keerthi",
  employeeId: 123
};
```



