## JavaScript (JS)

### Primitive Types
Single, immutable data types:
- string
- number (2^53 - 1)
- boolean
- null – Intentional absence of any object value
- undefined – A variable declared but not assigned
- symbol – Unique and immutable value used as object keys
- BigInt – Large integers beyond the safe limit (2^53 - 1) of number

Their container values cannot be changed directly but can be assigned again. Below is an example of immutability:

```javascript
var myVar = "Hello World";
myVar = "Hello World!!!!"; // new String reference assigned
// this will assign and return a new String reference to myVar object
myVar = myVar.toUpperCase();
```

### Non-Primitive Types
Complex, mutable data types:
- object (key-value pairs with string and symbol keys)
- array
- set (same as array with unique values)
- map (same as object with unique keys of any type, Faster than object, Maintains insertion order, Directly iterable)

### Scoping
- Lexical: Scope defined by where variables/functions are written
- Block: Variables declared inside `{}` using `let` or `const` are not accessible outside
- Function: `var` is only accessible within the function it's declared in

### Variable Declarations
- `let` – Block-scoped, can be reassigned, Causes TDZ.
- `const` – Block-scoped, cannot be reassigned, Causes TDZ.
- `var` – Function-scoped, gets hoisted (avoid using as it causes global pollution)

```function testVar() {
  const a = 10;
  if (true) {
    var x = 10;
    let y = 20;
    const z = 30;
    console.log(z); // ✅ 30 — accessible
  }
  console.log(x); // ✅ 10 — accessible outside the block
  console.log(y); // ❌ ReferenceError: y is not defined
  console.log(z); // ❌ ReferenceError: z is not defined
  console.log(a); // ✅ 10 — accessible
}
```

### Arrow vs Regular Functions
- Arrow functions `()=>{}` are concise, lightweight and do not bind their own `this`, `arguments`, or `super`
- Regular functions use their own `this` depending on how they're called
```
const obj = {
  name: "Rajan",
  arrowFn: () => {
    console.log(this.name); // ❌ undefined
  },
  regularFn: function () {
    console.log(this.name); // ✅ "Rajan"
  }
};

obj.arrowFn();
obj.regularFn();
```

### Hoisting
Assignment of memory to declarations (not initializations) before code execution.
Applicable to `var`, functions, and classes (in limited ways).

### Execution Context
The environment where memory is assigned to variables and function references are stored and code to be executed.

### Call Stack
- Stack where function calls are pushed and popped in order for execution
- When function calls exceed call stack space, maximum depth error will be thrown

### Event Loop
The event loop manages the process of offloading async tasks from the call stack to browser or Node.js APIs, and later retrieves the results, placing the associated callbacks into the callback queue (or priority queue for prmomises) for execution once the call stack is clear.

### Queue Types
- Callback queue holds `setTimeout`, `setInterval` callbacks
- Microtasks (e.g., `Promise.then`) goes to priority queue

### Currying
Breaking a function with multiple arguments into a series of unary functions:
```javascript
function multiply(a) {
  return function(b) {
    return a * b;
  };
}
const double = multiply(2);
console.log(double(5));  // 10
```

### Object Methods
- `Object.create` – Creates a new object using another as a prototype
- `Object.assign` – Copies properties from one or more objects
- `Object.freeze` – Makes an object immutable
- `Object.seal` – Prevents deleting and creating keys but values can be modified

### Object Copying
- Assignment: Whole object or array is referenced
- Shallow copy: Only the first level of the object is copied; deeper levels are referenced
- Deep copy: All levels of the object are copied (true copy)
```javascript
const original = { name: "Tony" };
const copy = original;
const shallow = Object.assign({}, original);
const deep = structuredClone(original);
```

### Prototypes
They allow shared behavior (methods or properties) across all instances of an object without duplicating them in memory.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, I'm ${this.name}`);
};

const p1 = new Person("Alice");
p1.greet();  // Hello, I'm Alice
```

#### Function Methods
- `call`: Invokes function with specified `this` and arguments
- `apply`: Same as call but takes arguments as an array
- `bind`: Returns a new function with `this` permanently set

```javascript
function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

const person = { name: "Alice" };
greet.call(person, "Hello");  // Hello, Alice
greet.apply(person, ["Hi"]);  // Hi, Alice
const sayHello = greet.bind(person, "Hey");
sayHello();  // Hey, Alice
```

### Code Complexity
| Big O | Meaning | Example |
|-------|---------|----------|
| O(1) | Constant time | Just one print or lookup |
| O(n) | Linear time | One loop over array |
| O(n²) | Quadratic time | Nested loop |
| O(log n) | Logarithmic time | Binary search |

### Promises
A Promise is a JavaScript object that represents the eventual completion (or failure) of an async operation and returns its resulting value.

### Closures
Functions with their lexical environment are closures:
```javascript
function outer() {
  let count = 0;
  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();  // outer is called once
counter();  // 1
counter();  // 2
```
