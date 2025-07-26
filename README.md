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
- object
- array
- set (same as array with unique values)
- map (same as object with unique keys of any type)

### Variable Declarations
- `let` – Block-scoped, can be reassigned
- `const` – Block-scoped, cannot be reassigned
- `var` – Function-scoped, gets hoisted (avoid using as it causes global pollution)

### Functions
#### Arrow vs Regular Functions
- Arrow functions `()=>{}` are concise, lightweight and do not bind their own `this`, `arguments`, or `super`
- Regular functions use their own `this` depending on how they're called

### Scoping
- Lexical: Scope defined by where variables/functions are written
- Block: Variables declared inside `{}` using `let` or `const` are not accessible outside
- Function: `var` is only accessible within the function it's declared in

### JavaScript Concepts
#### Hoisting
Assignment of memory to declarations (not initializations) before code execution.
Applicable to `var`, functions, and classes (in limited ways).

#### Execution Context
The environment where memory is assigned to variables and function references are stored and code to be executed.

#### Call Stack
- Stack where function calls are pushed and popped in order for execution
- When function calls exceed call stack space, maximum depth error will be thrown

#### Event Loop
The event loop manages the process of offloading async tasks from the call stack to browser or Node.js APIs, and later retrieves the results, placing the associated callbacks into the callback queue (or priority queue) for execution once the call stack is clear.

#### Queue Types
- Callback queue holds `setTimeout`, `setInterval` callbacks
- Microtasks (e.g., `Promise.then`) go into a higher-priority queue

### Advanced Concepts
#### Currying
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

#### Object Methods
- `Object.create` – Creates a new object using another as a prototype
- `Object.assign` – Copies properties from one or more objects
- `Object.freeze` – Makes an object immutable
- `Object.seal` – Prevents deleting and creating keys

#### Object Copying
- Assignment: Whole object or array is referenced
- Shallow copy: Only the first level of the object is copied; deeper levels are referenced
- Deep copy: All levels of the object are copied (true copy)

#### Prototypes
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

### Asynchronous Programming
#### Promises
A Promise is a JavaScript object that represents the eventual completion (or failure) of an async operation and returns its resulting value.

#### Closures
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

## React

### Core Concepts
#### State and Props
- State: Internal data controlled by the component
- Props: External data passed down from parent component

#### DOM
React uses a virtual DOM to efficiently update only changed elements in the real DOM (reconciliation).

#### Components
- Controlled: Form values are managed via React state
- Uncontrolled: Form values handled by the DOM using `ref`

#### Keys
Keys uniquely identify elements in a list to help React optimize rendering.

### Hooks
- `useState` – Hook to declare state in functional components
- `useEffect` – Hook for handling side effects (e.g., fetching data, timers)
- `useRef` – Holds mutable persistent values that don't trigger re-renders
- `useContext` – Accesses values from the nearest context provider

```javascript
const UserContext = createContext();

function App() {
  return (
    <UserContext.Provider value={{ name: "Alice" }}>
      <GrandChild />
    </UserContext.Provider>
  );
}

function GrandChild() {
  const user = useContext(UserContext);
  return <p>Hello, {user.name}!</p>;
}
```

#### useReducer
```javascript
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  return (
    <>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  );
}
```

### Advanced Features
- `useCallback` – Returns a memoized version of a callback function
- `useMemo` – Returns a memoized result to avoid recalculating on every render
- `useLayoutEffect` – Runs synchronously after DOM mutations, before browser paint
- `React.memo` – Caching technique to prevent unnecessary re-renders
- Lazy Loading – Loads components when needed to reduce initial load time
- Redux Toolkit – Simplified way to write Redux logic
- Error Boundary – Catches JS errors in its subtree
- HOC (Higher Order Component) – Function that returns a new component

### Security
- Keep API keys on server
- Keep dependencies updated
- Validate forms on frontend and APIs on server
- Use HTTP-only cookies for access tokens

## React Native

### Threading
- JS thread: Runs app logic
- Shadow thread: Handles layout
- Main/UI thread: Handles rendering

### Features
- Bridging: Connects JS to native modules via async communication
- JSI: New way to interact with native modules using C++
- FlatList: High-performance list view for large data sets

### FlatList Optimization
- `keyExtractor`: Identify list items uniquely
- `initialNumToRender`: Reduce first render time
- `maxToRenderPerBatch`: Control render rate
- `windowSize`: Optimize memory usage
- `removeClippedSubviews`: Free up memory
- `getItemLayout`: Improve scroll for fixed height items
- `React.memo`: Prevent unnecessary re-renders
- `useCallback`: Avoid recreating render functions

### Development Tools
- Optimization: Lazy loading, avoiding unnecessary re-renders
- Debugging: Flipper, Chrome Debugger, React DevTools
- React Navigation: Handles navigation stacks, tabs, transitions
- Security: Protect app data, code, and API endpoints

## TypeScript (TS)

### Types
Enforces expected structure and data types at compile time.

### Special Types
- `unknown`: Type-safe version of `any` (must assert type before use)
- `never`: Functions that never return
- `any`: Opts out of type checking (use cautiously)

### Type Definitions
- Interface: Declares object shape, including optional properties
- Enum: Defines named constants (numeric or string)
- Union: Variable can be one of several types (`string | number`)
- Intersection: Combines multiple types (`TypeA & TypeB`)
- Tuple: Array with fixed number and types (`[string, number]`)

### Type Features
- Type inference: Compiler guesses the type
- Explicit typing: Developer defines the type
- Optional parameters: `param?: string`
- Default parameters: Fallback values
- Rest parameters: Variable number of arguments
- Generics: Type-safe, reusable components (`<T>`)

### Utility Types
- `Partial<T>`: All properties optional
- `Required<T>`: All properties required
- `Record<K,T>`: Object type with keys K, values T
- `Omit<T,K>`: Remove keys
- `Pick<T,K>`: Select keys
- `Exclude<T,U>`: Exclude union members
- `Readonly<T>`: Make properties immutable

### Type Casting
Tells compiler to treat variable as specific type (`value as string`)

## Regular Expressions (Regex)

### Basic Syntax
- `.` – Any character
- `^` – Start of string
- `$` – End of string
- `*` – 0 or more of previous element
- `+` – 1 or more
- `?` – 0 or 1 (optional)
- `[]` – Character class (e.g., [a-z])
- `[^]` – Negated character class
- `()` – Grouping
- `|` – OR operator

### Special Characters
- `\d` – Digit (0–9)
- `\D` – Non-digit
- `\w` – Word character (a-z, A-Z, 0-9, _)
- `\W` – Non-word character
- `\s` – Whitespace
- `\S` – Non-whitespace

### Common Use Cases
```javascript
// Match date (DD-MM-YYYY)
"10-04-2025".match(/^\d{2}-\d{2}-\d{4}$/);

// Validate username
"user_123".match(/^[a-zA-Z0-9_]{3,12}$/);

// Match words without digits
"hello".match(/^[^\d]+$/);

// Optional country code in phone
"+91 9876543210".match(/^(\+\d{1,3}\s)?\d{10}$/);

// Match "cat" or "dog"
"cat".match(/^(cat|dog)$/);

// Match quoted strings
'"hello world"'.match(/^".*"$/);

// Check for word characters
"  hello_123  ".trim().match(/^\w+$/);

// Replace non-letters
"abc123!@#".replace(/[^a-zA-Z]/g, "");  // "abc"
```

## Git Commands

### Basic Operations
- `git init` – Initialize repository
- `git clone <repo>` – Clone remote repository
- `git status` – Show working directory status
- `git add <file>` – Stage changes
- `git commit -m "message"` – Commit changes
- `git push origin main` – Push to remote
- `git pull origin main` – Pull latest changes

### Branch Operations
- `git branch` / `git checkout -b <branch>` – Create/switch branches
- `git merge <branch>` – Merge branches
- `git stash` / `git stash pop` – Store/retrieve changes (removing)
- `git stash` / `git stash apply` – Store/retrieve changes (keeping)

### Remote Operations
- `git remote -v` – View remotes
- `git remote add origin <url>` – Add origin
- `git remote set-url origin <new-url>` – Change origin
- `git remote remove origin` – Remove origin
- `git push -u origin main` – Set upstream

## Testing

### Snapshot Testing
```javascript
const tree = renderer.create(<MyComponent />).toJSON();
expect(tree).toMatchSnapshot();
```

### Mock AsyncStorage
```javascript
jest.mock('@react-native-async-storage/async-storage', () => ({
  setItem: jest.fn(),
  getItem: jest.fn(),
  removeItem: jest.fn(),
}));
```


