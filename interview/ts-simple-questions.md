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




