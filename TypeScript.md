
## TypeScript (TS)

### Types
Enforces expected structure and data types at compile time.

### Special Types
- `unknown`: Type-safe version of `any` (must assert type before use)
```typescript
let value: unknown = "Rajan";
value.toUpperCase(); // ❌ Error
if (typeof value === "string") {
  value.toUpperCase(); // ✅ Safe
}
```

- `never`: Functions that never return
- `any`: Opts out of type checking (use cautiously)

### Type Definitions
- Interface: Declares object shape, declaration merging, and extends other interfaces
- Type: Can be useful for single type or union of types unlike interface
```typescript
type UserID = string | number;
```

- Enum: Defines named constants (numeric or string)

```typescript
enum Color {
  Red, // 0
  Green, // 1
}
enum Role {
  Admin = "ADMIN",
  User = "USER"
}
```

- Union: Variable can be one of several types (`string | number`)
- Intersection: Combines multiple types (`TypeA & TypeB`)
- Tuple: Array with fixed number and types (`[string, number]`)
```typescript
const [name, setName] = useState("Rajan");
```

### Type Features
- Type inference: Compiler guesses the type
```typescript
let name = "Rajan"; // inferred as string
```
- Explicit typing: Developer defines the type
```typescript
let name: string = "Rajan"; // explicit typing
```
- Optional parameters: `param?: string`
- Default parameters: Fallback values
- Rest parameters: Variable number of arguments
```typescript
function sum(a: number, b: number, ...rest: number[]) {
  return a + b + rest.reduce((sum, num) => sum + num, 0);
}
```
- Generics: Type-safe, reusable components (`<T>`)
```typescript
function identity<T>(value: T): T {
  return value;
}
identity<string>("Rajan");
```

### Utility Types
- `Readonly<T>`: Make properties immutable
- `Partial<T>`: All properties optional
- `Required<T>`: All properties required
- `Record<K,T>`: Object type with keys K, values T
```typescript
type Language = "en" | "fr";

type Translation = {
  welcome: string;
};

const messages: Record<Language, Translation> = {
  en: { welcome: "Hello" },
  fr: { welcome: "Bonjour" },
};
```

- `Omit<T,K>`: Remove keys
```typescript
type User = {
  id: number;
  name: string;
  email: string;
};

type UserWithoutEmail = Omit<User, "email">;
```
- `Pick<T,K>`: Select keys
```typescript
type User = {
  id: number;
  name: string;
  email: string;
};

type UserWithOnlyNameAndId = Pick<User, "name" | "id">;
```

- `Exclude<T,U>`: Exclude union members
```typescript
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

type PublicUser = Pick<User, Exclude<keyof User, "password">>;

const user: PublicUser = {
  id: 1,
  name: "Rajan",
  email: "rajan@example.com",
  // password: "secret", ❌ Not allowed
};

```

### Type Casting
Tells compiler to treat variable as specific type (`value as string`)
