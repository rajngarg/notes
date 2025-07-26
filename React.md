
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
