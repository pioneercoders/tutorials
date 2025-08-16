#### 1. What is the difference between interface extends and type intersection?

interface extends: Creates a new interface by inheriting from another.

type intersection (&): Combines multiple types into one.

interface A { a: string; }
interface B { b: number; }
interface C extends A, B {}

type D = A & B; // Same as above, but works with any type

#### 2.Explain the difference between any, unknown, and never in detail?

--> any disables type checking — you can assign and use any value, but it’s unsafe.
--> unknown is like a safer any: it can hold any value, but you must check its type before using it.
--> never represents a type that never occurs, usually for functions that don’t return or for exhaustive type checks.

#### 3.What are mapped types in TypeScript? Provide an example.

Mapped types in TypeScript let you create new types by transforming existing ones.
They work by looping over the keys of another type (keyof) and applying a transformation to each property.

For example:

```typescript
type PartialPerson = { [K in keyof Person]?: Person[K] };
```
makes all properties of Person optional.
TypeScript also provides built-in mapped types like Partial<T>, Readonly<T>, Pick<T>, and Record<K, T> that are commonly used in real-world projects.

#### 4.How does TypeScript handle function overloading?
TypeScript handles function overloading by letting us define multiple signatures for a single function, but with one shared implementation. The overload signatures define the valid ways a function can be called, while the single implementation must handle all cases, usually using type checks. At runtime, only the single implementation exists — the overloads are purely for compile-time type safety.

#### 5.What is the difference between nominal typing and structural typing? Why does TypeScript use structural typing?

Nominal typing is name-based: types are compatible only if they are explicitly declared related (like in Java or C#). Structural typing is shape-based: types are compatible if they have the same structure, regardless of their names. TypeScript uses structural typing because JavaScript itself is dynamic and duck-typed, so structural typing makes TypeScript more flexible, easier to use with existing JS code, and better suited for real-world JS interoperability.

#### 6.Explain how decorators work in TypeScript.
Decorators in TypeScript are special functions used to attach metadata or modify behavior of classes, methods, properties, or parameters. They are written with an @ prefix, like @Component in Angular. TypeScript provides class, method, property, accessor, and parameter decorators. For example, a method decorator can wrap a function to log when it’s called. They’re widely used in frameworks like Angular and NestJS for dependency injection, metadata, and configuration.

Types of Decorators

Class Decorator – applied to classes

Property Decorator – applied to class properties

Method Decorator – applied to class methods

Accessor Decorator – applied to getters/setters

Parameter Decorator – applied to method parameters

#### 7.How does TypeScript handle async/await with types?

In TypeScript, async functions always return a Promise<T>. The type T is inferred from the value you return. When you use await, TypeScript unwraps the promise and infers the correct type for the resolved value. For example, if a function returns Promise<User>, then await will give you a User. Errors are inferred as unknown in catch blocks. Generics also work seamlessly with async/await, making it type-safe for APIs and data fetching.

#### 8.What is the difference between global and module augmentation?

In TypeScript, augmentation means extending existing types.

Global augmentation is when we add new properties or methods to types that exist in the global scope, like String, Window, or Array. For example, I can add a custom method to String and it will be available everywhere in the project.

Module augmentation is when we extend types inside a specific module, usually an external library. For example, in an Express project, I can augment the Request interface to include a userId property, and it will only affect the express module.

#### 10.How does TypeScript support JSX in React applications?
TypeScript supports JSX by treating it as a special syntax extension. When we use React with TypeScript, the JSX is type-checked and then compiled down to JavaScript function calls like React.createElement.

In tsconfig.json, we enable JSX support with the "jsx" compiler option ("react", "react-jsx", or "react-jsxdev" depending on the React version).

TypeScript uses the JSX namespace and React’s type definitions (@types/react) to check JSX expressions, component props, and children.

Function components are typed using React.FC or explicit prop interfaces, so TypeScript ensures that the JSX elements we pass match the expected props.


