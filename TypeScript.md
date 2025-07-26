
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
