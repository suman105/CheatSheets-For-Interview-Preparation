# React.js Cheatsheet

## React Basics

### Functional Component (Primary Approach)

```jsx
// Basic React app with functional component using JSX
import React from 'react';
import { createRoot } from 'react-dom/client';

// Functional component: Modern, lightweight
function App() {
  return (
    // JSX: HTML-like syntax for UI
    <div>
      <h1>Hello, React!</h1>
    </div>
  );
}

// Render to DOM
const root = createRoot(document.getElementById('root'));
root.render(<App />);
```

### Class Component (Alternative Approach)

```jsx
import React, { Component } from 'react';
import { createRoot } from 'react-dom/client';

// Class component: Legacy, more verbose
class App extends Component {
  render() {
    return (
      <div>
        <h1>Hello, React!</h1>
      </div>
    );
  }
}

// Render to DOM
const root = createRoot(document.getElementById('root'));
root.render(<App />);
```

- **React Overview**: React is a JavaScript library for building user interfaces using components and a virtual DOM for efficient updates.
- **JSX**: JavaScript XML, compiled to `React.createElement` calls.
- **Setup**:
  - Use `create-react-app`, Vite, or Next.js for project initialization.
  - Requires `react` and `react-dom` packages.
- **Functional vs. Class Components**:
  - **Functional**: Preferred for simplicity, hooks, and modern React.
  - **Class**: Legacy, used for error boundaries or older codebases.
- **Best Practices**:
  - Use functional components unless class-specific features (e.g., error boundaries) are needed.
  - Keep components focused and reusable.
  - Avoid inline styles; use CSS modules or styled-components.

**Explanation**:
- Functional components are concise and leverage hooks, making them the standard.
- Class components are verbose, requiring `this` binding for methods, but necessary for error boundaries.
- JSX allows HTML-like syntax but requires a single root element.
- Use tools like Vite for faster development over `create-react-app`.

---

## React Components & Props

### Functional Component with Props

```jsx
// Functional component with props
function Greeting({ name, age }) {
  // Destructure props for readability
  return <h1>Hello, {name}! You are {age} years old.</h1>;
}

// Parent component passing props
function App() {
  return (
    <div>
      <Greeting name="Suman" age={25} />
    </div>
  );
}

// Default props
Greeting.defaultProps = {
  age: 18,
};

// PropTypes for runtime validation
import PropTypes from 'prop-types';
Greeting.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number,
};
```

### Class Component with Props

```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Greeting extends Component {
  // Default props
  static defaultProps = {
    age: 18,
  };

  // PropTypes
  static propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number,
  };

  render() {
    const { name, age } = this.props;
    return <h1>Hello, {name}! You are {age} years old.</h1>;
  }
}

class App extends Component {
  render() {
    return (
      <div>
        <Greeting name="Suman" age={25} />
      </div>
    );
  }
}
```

### TypeScript Alternative

```jsx
// Functional component with TypeScript
interface GreetingProps {
  name: string;
  age?: number;
}

function Greeting({ name, age = 18 }: GreetingProps) {
  return <h1>Hello, {name}! You are {age} years old.</h1>;
}
```

- **Props**: Immutable data passed from parent to child.
- **Approaches**:
  - **Functional**: Destructuring props is concise.
  - **Class**: Requires `this.props`, more boilerplate.
  - **TypeScript**: Static type checking, eliminates PropTypes.
- **PropTypes**: Runtime validation, optional with TypeScript.
- **Best Practices**:
  - Validate props with PropTypes or TypeScript.
  - Use default props for optional values.
  - Avoid complex prop structures; prefer simple data.

**Explanation**:
- Functional components with destructuring are preferred for readability.
- Class components are viable for legacy code but less common.
- TypeScript provides compile-time safety, reducing runtime errors.
- PropTypes is useful for JavaScript projects without TypeScript.

---

## State & State Management

### useState Hook (Primary Approach)

```jsx
import { useState } from 'react';

function Counter() {
  // useState: Manage local state
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      {/* Functional update for safe state updates */}
      <button onClick={() => setCount(prev => prev + 1)}>Increment</button>
    </div>
  );
}
```

### Class Component State (Alternative)

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  state = { count: 0 };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

### useReducer Hook (Alternative for Complex State)

```jsx
import { useReducer } from 'react';

// Reducer for complex state logic
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}
```

- **State**: Local data that triggers re-renders when updated.
- **Approaches**:
  - **useState**: Simple state management for primitive values or small objects.
  - **Class State**: Legacy, uses `setState` with merging behavior.
  - **useReducer**: Ideal for complex state transitions or state machines.
- **Best Practices**:
  - Use functional updates (`prev => ...`) for `useState`/`setState`.
  - Avoid redundant state; derive values when possible.
  - Use `useReducer` for multi-step or interdependent state updates.

**Explanation**:
- `useState` is the go-to for most state needs due to simplicity.
- Class-based `setState` merges updates, unlike `useState` which replaces.
- `useReducer` mirrors Redux-like patterns, suitable for complex logic.
- Combine `useReducer` with Context for global state without external libraries.

---

## Event Handling

### Functional Component

```jsx
function Button() {
  // Event handler
  const handleClick = event => {
    console.log('Clicked!', event.target);
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```

### Class Component

```jsx
import React, { Component } from 'react';

class Button extends Component {
  // Bind in constructor or use arrow function
  handleClick = event => {
    console.log('Clicked!', event.target);
  };

  render() {
    return <button onClick={this.handleClick}>Click Me</button>;
  }
}
```

### Inline Handler (Alternative, Less Preferred)

```jsx
function Button() {
  return (
    <button
      onClick={event => console.log('Clicked!', event.target)}
    >
      Click Me
    </button>
  );
}
```

- **Events**: React uses synthetic events (`SyntheticEvent`) for cross-browser consistency.
- **Approaches**:
  - **Named Handler**: Reusable, memoizable with `useCallback`.
  - **Class Handler**: Requires binding or arrow functions to preserve `this`.
  - **Inline Handler**: Quick but can cause performance issues if passed as props.
- **Common Events**: `onClick`, `onChange`, `onSubmit`, `onKeyDown`, `onMouseOver`.
- **Best Practices**:
  - Use named handlers for clarity and performance.
  - Prevent default behavior with `event.preventDefault()`.
  - Memoize handlers with `useCallback` when passed to memoized components.

**Explanation**:
- Named handlers are preferred for maintainability and optimization.
- Class components require binding (`this.handleClick = this.handleClick.bind(this)`) unless using arrow functions.
- Inline handlers are convenient for prototyping but avoid in production due to re-creation on each render.
- Synthetic events are pooled; access properties synchronously or persist with `event.persist()`.

---

## Conditional Rendering

### Ternary Operator

```jsx
function UserStatus({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <p>Welcome, User!</p> : <p>Please log in.</p>}
    </div>
  );
}
```

### Logical AND

```jsx
function UserStatus({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn && <p>Welcome, User!</p>}
      {!isLoggedIn && <p>Please log in.</p>}
    </div>
  );
}
```

### Early Return

```jsx
function UserStatus({ isLoggedIn }) {
  if (!isLoggedIn) {
    return <p>Please log in.</p>;
  }
  return <p>Welcome, User!</p>;
}
```

- **Techniques**:
  - **Ternary**: Concise for simple either/or conditions.
  - **Logical AND**: Ideal for rendering single elements conditionally.
  - **Early Return**: Clear for complex conditions, reduces nesting.
- **Best Practices**:
  - Keep JSX clean; extract complex logic to variables or functions.
  - Use fragments (`<>...</>`) to avoid wrapper elements.
  - Ensure accessibility with fallback content (e.g., empty states).

**Explanation**:
- Ternary operators are readable for binary choices but can become unwieldy with nested conditions.
- Logical AND is succinct but limited to single conditions.
- Early returns improve readability for multiple conditions or validation checks.
- All approaches are equivalent in functionality; choose based on clarity.

---

## Lists & Keys

### Functional Component

```jsx
function TodoList({ items }) {
  return (
    <ul>
      {items.map(item => (
        // Key: Unique identifier for each item
        <li key={item.id}>{item.text}</li>
      ))}
    </ul>
  );
}
```

### Class Component

```jsx
import React, { Component } from 'react';

class TodoList extends Component {
  render() {
    const { items } = this.props;
    return (
      <ul>
        {items.map(item => (
          <li key={item.id}>{item.text}</li>
        ))}
      </ul>
    );
  }
}
```

- **Keys**: Unique IDs for list items to optimize rendering.
- **Approaches**:
  - **Functional**: Same as class but more concise.
  - **Class**: Identical logic, more boilerplate.
- **Best Practices**:
  - Use stable IDs (e.g., database IDs); avoid array indices for dynamic lists.
  - Extract list items to separate components for complex rendering.
  - Ensure keys are unique among siblings.

**Explanation**:
- Keys help React track elements during re-renders, preventing UI bugs.
- Both functional and class components handle lists identically.
- Indices as keys (`key={index}`) are problematic if items reorder or change.
- Use `React.Fragment` or components for complex list items to maintain clean JSX.

---

## useEffect Hook

### Functional Component

```jsx
import { useState, useEffect } from 'react';

function DataFetcher() {
  const [data, setData] = useState(null);

  // useEffect: Handle side effects like fetching
  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(res => res.json())
      .then(setData);

    // Cleanup: Prevent memory leaks
    return () => {
      console.log('Cleanup');
    };
  }, []); // Empty deps: Run once on mount

  return <div>{data ? data.name : 'Loading...'}</div>;
}
```

### Class Component (componentDidMount/componentWillUnmount)

```jsx
import React, { Component } from 'react';

class DataFetcher extends Component {
  state = { data: null };

  componentDidMount() {
    fetch('https://api.example.com/data')
      .then(res => res.json())
      .then(data => this.setState({ data }));
  }

  componentWillUnmount() {
    console.log('Cleanup');
  }

  render() {
    const { data } = this.state;
    return <div>{data ? data.name : 'Loading...'}</div>;
  }
}
```

- **useEffect**: Manages side effects in functional components.
- **Class Lifecycle**:
  - `componentDidMount`: Runs after mount.
  - `componentWillUnmount`: Runs before unmount.
  - `componentDidUpdate`: Handles updates (not shown here).
- **Best Practices**:
  - Include all dependencies in `useEffect` dependency array.
  - Use cleanup functions to prevent memory leaks.
  - Avoid fetching in `useEffect` without cleanup for cancellable requests.

**Explanation**:
- `useEffect` combines lifecycle methods into a single API, more flexible than class methods.
- Class lifecycle methods are more explicit but verbose.
- Cleanup is critical for async operations or subscriptions (e.g., WebSockets).
- Use libraries like `axios` with cancellation for robust fetching.

---

## Other Common Hooks

### useRef

```jsx
import { useRef, useEffect } from 'react';

function InputFocus() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} type="text" />;
}
```

### Class Equivalent (createRef)

```jsx
import React, { Component } from 'react';

class InputFocus extends Component {
  inputRef = React.createRef();

  componentDidMount() {
    this.inputRef.current.focus();
  }

  render() {
    return <input ref={this.inputRef} type="text" />;
  }
}
```

### useMemo & useCallback

```jsx
import { useMemo, useCallback } from 'react';

function ExpensiveComponent({ items }) {
  // useMemo: Cache sorted array
  const sortedItems = useMemo(() => [...items].sort(), [items]);

  // useCallback: Cache callback
  const handleSelect = useCallback(id => console.log(id), []);

  return sortedItems.map(item => (
    <div key={item.id} onClick={() => handleSelect(item.id)}>
      {item.name}
    </div>
  ));
}
```

### Class Equivalent (Manual Memoization)

```jsx
import React, { Component } from 'react';

class ExpensiveComponent extends Component {
  sortedItems = null;

  handleSelect = id => console.log(id);

  componentDidUpdate(prevProps) {
    if (prevProps.items !== this.props.items) {
      this.sortedItems = [...this.props.items].sort();
    }
  }

  render() {
    const { items } = this.props;
    this.sortedItems = this.sortedItems || [...items].sort();
    return this.sortedItems.map(item => (
      <div key={item.id} onClick={() => this.handleSelect(item.id)}>
        {item.name}
      </div>
    ));
  }
}
```

- **useRef**: Persistent, mutable reference without re-renders.
- **createRef**: Class-based equivalent, re-created each render.
- **useMemo**: Caches values; `useCallback`: Caches functions.
- **Class Memoization**: Manual caching in lifecycle methods, error-prone.
- **Best Practices**:
  - Use `useRef` for DOM access or non-rendering state.
  - Memoize only when performance is an issue (profile first).
  - Avoid overusing `useMemo`/`useCallback` to prevent complexity.

**Explanation**:
- `useRef` is more flexible than `createRef`, which is limited to class components.
- `useMemo`/`useCallback` simplify optimization compared to manual class logic.
- Class-based memoization requires careful lifecycle management, prone to bugs.
- Use React DevTools to identify unnecessary re-renders before memoizing.

---

## Context & useContext

### Functional with useContext

```jsx
import { createContext, useContext } from 'react';

const ThemeContext = createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedComponent />
    </ThemeContext.Provider>
  );
}

function ThemedComponent() {
  const theme = useContext(ThemeContext);
  return <div>Theme: {theme}</div>;
}
```

### Class with Context Consumer

```jsx
import React, { Component, createContext } from 'react';

const ThemeContext = createContext('light');

class App extends Component {
  render() {
    return (
      <ThemeContext.Provider value="dark">
        <ThemedComponent />
      </ThemeContext.Provider>
    );
  }
}

class ThemedComponent extends Component {
  render() {
    return (
      <ThemeContext.Consumer>
        {theme => <div>Theme: {theme}</div>}
      </ThemeContext.Consumer>
    );
  }
}
```

- **Context**: Shares data without prop drilling.
- **Approaches**:
  - **useContext**: Simple, functional hook.
  - **Consumer**: Class-based, more verbose.
- **Best Practices**:
  - Use for global state (e.g., theme, auth).
  - Combine with `useReducer` for complex state.
  - Avoid overuse; prefer props for local data.

**Explanation**:
- `useContext` is cleaner and integrates with hooks.
- `Consumer` is necessary for class components or complex rendering logic.
- Context updates cause re-renders; memoize values to optimize.
- Use libraries like Redux or Zustand for large-scale state management.

---

## Error Boundaries

### Class Component (Only Approach)

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.error('Error:', error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}

function App() {
  return (
    <ErrorBoundary>
      <BuggyComponent />
    </ErrorBoundary>
  );
}
```

- **Error Boundaries**: Catch JavaScript errors in child components.
- **Limitation**: Only class components support error boundaries.
- **Alternative**: Use try-catch for event handlers or async code.
- **Best Practices**:
  - Wrap critical components to prevent crashes.
  - Log errors to services like Sentry.
  - Provide user-friendly fallback UI.

**Explanation**:
- No functional equivalent exists for error boundaries yet.
- Try-catch blocks handle non-rendering errors (e.g., in `useEffect`).
- Error boundaries are essential for robust applications.
- Test error scenarios to ensure graceful recovery.

---

## Performance Optimization

### React.memo (Functional)

```jsx
import { memo } from 'react';

const Child = memo(function Child({ value }) {
  console.log('Child rendered');
  return <div>{value}</div>;
});
```

### Class PureComponent (Alternative)

```jsx
import React, { PureComponent } from 'react';

class Child extends PureComponent {
  render() {
    console.log('Child rendered');
    return <div>{this.props.value}</div>;
  }
}
```

### useMemo & useCallback (Revisited)

```jsx
function List({ items }) {
  const sortedItems = useMemo(() => [...items].sort(), [items]);
  const handleSelect = useCallback(id => console.log(id), []);
  return sortedItems.map(item => (
    <div key={item.id} onClick={() => handleSelect(item.id)}>
      {item.name}
    </div>
  ));
}
```

- **Approaches**:
  - **React.memo**: Prevents re-renders for functional components.
  - **PureComponent**: Shallow prop/state comparison for classes.
  - **useMemo/useCallback**: Fine-grained control for values/functions.
- **Best Practices**:
  - Profile with React DevTools before optimizing.
  - Use `memo` for components with frequent parent re-renders.
  - Avoid premature optimization; measure impact first.

**Explanation**:
- `React.memo` is simpler than `PureComponent`, which requires class boilerplate.
- `useMemo`/`useCallback` offer precise control but increase complexity.
- Shallow comparisons (`memo`, `PureComponent`) may miss deep object changes.
- Use `React.Profiler` to quantify render costs.

---

## Concurrent Rendering & Suspense

### Suspense with use (Experimental)

```jsx
import { Suspense, use } from 'react';

const fetchData = () => Promise.resolve({ name: 'Suman' });

function DataComponent() {
  const data = use(fetchData());
  return <div>{data.name}</div>;
}

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <DataComponent />
    </Suspense>
  );
}
```

### Lazy Loading with React.lazy

```jsx
import { Suspense, lazy } from 'react';

const LazyComponent = lazy(() => import('./Component'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

- **Concurrent Features**:
  - **Suspense**: Handles async rendering with fallbacks.
  - **use**: Experimental for promise-based data (React 19).
  - **React.lazy**: Code splitting for dynamic imports.
- **Alternative**: Use libraries like React Query or SWR for data fetching.
- **Best Practices**:
  - Wrap async components in `Suspense`.
  - Provide meaningful fallback UI.
  - Test with slow networks to ensure good UX.

**Explanation**:
- `use` simplifies async data but is experimental; prefer stable libraries for production.
- `React.lazy` reduces initial bundle size, improving load times.
- Suspense integrates with Concurrent Rendering for responsive UIs.
- Libraries like React Query offer caching and refetching, complementing Suspense.

---

## State Management (Global)

### Context + useReducer

```jsx
import { createContext, useContext, useReducer } from 'react';

const CountContext = createContext();

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    default:
      return state;
  }
}

function App() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <CountContext.Provider value={{ state, dispatch }}>
      <Counter />
    </CountContext.Provider>
  );
}

function Counter() {
  const { state, dispatch } = useContext(CountContext);
  return (
    <div>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
    </div>
  );
}
```

### Zustand (Lightweight Library)

```jsx
import { create } from 'zustand';

const useStore = create(set => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
}));

function Counter() {
  const { count, increment } = useStore();
  return (
    <div>
      <p>{count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

### Redux Toolkit (Robust Library)

```jsx
import { configureStore, createSlice } from '@reduxjs/toolkit';
import { Provider, useDispatch, useSelector } from 'react-redux';

// Define slice
const counterSlice = createSlice({
  name: 'counter',
  initialState: { count: 0 },
  reducers: {
    increment: state => {
      state.count += 1;
    },
  },
});

const store = configureStore({
  reducer: { counter: counterSlice.reducer },
});

function Counter() {
  const count = useSelector(state => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => dispatch(counterSlice.actions.increment())}>
        Increment
      </button>
    </div>
  );
}

function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}
```

- **Approaches**:
  - **Context + useReducer**: Built-in, no dependencies, good for small apps.
  - **Zustand**: Lightweight, minimal boilerplate, scales well.
  - **Redux Toolkit**: Structured, ideal for large apps with complex state.
- **Other Libraries**: React Query (server state), MobX (reactive), Recoil (modern).
- **Best Practices**:
  - Use Context for simple global state; add libraries for complexity.
  - Optimize Context with memoization to prevent re-renders.
  - Choose based on app size: Zustand for medium, Redux for large.

**Explanation**:
- Context + `useReducer` is dependency-free but can cause re-renders if not optimized.
- Zustand is simpler than Redux, with a functional API.
- Redux Toolkit reduces boilerplate compared to classic Redux, with built-in immutability.
- React Query is ideal for server state, complementing client state solutions.

---

## Advanced Patterns

### Compound Components

```jsx
function Tabs({ children, activeTab = 0 }) {
  const [currentTab, setCurrentTab] = useState(activeTab);
  return React.Children.map(children, (child, index) =>
    React.cloneElement(child, { isActive: index === currentTab, onSelect: () => setCurrentTab(index) })
  );
}

function Tab({ isActive, onSelect, children }) {
  return (
    <div style={{ fontWeight: isActive ? 'bold' : 'normal' }} onClick={onSelect}>
      {children}
    </div>
  );
}

function App() {
  return (
    <Tabs>
      <Tab>Tab 1</Tab>
      <Tab>Tab 2</Tab>
    </Tabs>
  );
}
```

### Render Props

```jsx
function MouseTracker({ render }) {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  const handleMouseMove = e => setPosition({ x: e.clientX, y: e.clientY });

  return <div onMouseMove={handleMouseMove}>{render(position)}</div>;
}

function App() {
  return (
    <MouseTracker render={({ x, y }) => <p>Mouse: {x}, {y}</p>} />
  );
}
```

### Custom Hook (Alternative to Render Props)

```jsx
function useMousePosition() {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  useEffect(() => {
    const handleMouseMove = e => setPosition({ x: e.clientX, y: e.clientY });
    window.addEventListener('mousemove', handleMouseMove);
    return () => window.removeEventListener('mousemove', handleMouseMove);
  }, []);

  return position;
}

function App() {
  const { x, y } = useMousePosition();
  return <p>Mouse: {x}, {y}</p>;
}
```

- **Approaches**:
  - **Compound Components**: Implicit state sharing via props/context.
  - **Render Props**: Explicit data sharing via function prop.
  - **Custom Hook**: Modern, hook-based alternative to render props.
- **Best Practices**:
  - Use compound components for UI patterns (e.g., tabs, modals).
  - Prefer hooks over render props for logic reuse.
  - Ensure patterns are intuitive for other developers.

**Explanation**:
- Compound components are flexible for tightly coupled UI.
- Render props are powerful but verbose; hooks often replace them.
- Custom hooks are the modern standard for reusable logic, reducing component complexity.
- Choose patterns based on team familiarity and project needs.

---

## Routing with React Router

### React Router v6

```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

function Home() {
  return <h1>Home</h1>;
}
function About() {
  return <h1>About</h1>;
}
```

### Alternative: Next.js Routing

```jsx
// pages/index.js
export default function Home() {
  return (
    <div>
      <h1>Home</h1>
      <Link href="/about">About</Link>
    </div>
  );
}

// pages/about.js
export default function About() {
  return <h1>About</h1>;
}
```

- **Approaches**:
  - **React Router**: Client-side routing for SPAs.
  - **Next.js**: File-based routing, server-side rendering support.
- **Best Practices**:
  - Use `Link` for navigation to avoid page reloads.
  - Lazy load routes with `React.lazy` and Suspense.
  - Handle 404s with a catch-all route (`<Route path="*" ... />`).

**Explanation**:
- React Router is flexible for single-page applications.
- Next.js simplifies routing with file-based structure and adds SSR/SSG.
- React Router supports dynamic routes (`:id`) and nested routes.
- Next.js is preferred for SEO and server-side features.

---

## Testing React Components

### React Testing Library

```jsx
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('increments count', () => {
  render(<Counter />);
  const button = screen.getByText('Increment');
  fireEvent.click(button);
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

### Enzyme (Alternative)

```jsx
import { shallow } from 'enzyme';
import Counter from './Counter';

test('increments count', () => {
  const wrapper = shallow(<Counter />);
  wrapper.find('button').simulate('click');
  expect(wrapper.find('p').text()).toBe('Count: 1');
});
```

- **Approaches**:
  - **React Testing Library**: Focuses on user behavior, modern standard.
  - **Enzyme**: Tests implementation details, less recommended.
- **Other Tools**:
  - **Jest**: Test runner and assertions.
  - **Vitest**: Faster alternative for Vite.
  - **Cypress**: End-to-end testing.
- **Best Practices**:
  - Test user interactions, not internal state.
  - Use `getByRole` for accessible queries.
  - Mock APIs with MSW for realistic tests.

**Explanation**:
- React Testing Library encourages testing as users interact, improving reliability.
- Enzyme allows deep inspection but couples tests to implementation.
- Jest/Vitest integrate well with React projects.
- Cypress is ideal for integration and E2E testing.

---

## Accessibility (a11y)

```jsx
function AccessibleForm() {
  return (
    <form aria-labelledby="form-title">
      <h2 id="form-title">User Info</h2>
      <label htmlFor="name">Name:</label>
      <input
        id="name"
        type="text"
        aria-required="true"
        aria-describedby="name-error"
      />
      <span id="name-error" role="alert">
        Name is required
      </span>
      <button type="submit" aria-label="Submit form">
        Submit
      </button>
    </form>
  );
}
```

- **Best Practices**:
  - Use semantic HTML and ARIA attributes.
  - Ensure keyboard navigability (`tabindex`, `:focus` styles).
  - Test with screen readers (NVDA, VoiceOver).
  - Use `eslint-plugin-jsx-a11y` for linting.
- **Tools**:
  - **axe**: Accessibility auditing.
  - **Lighthouse**: Browser-based audits.
- **Explanation**:
  - Accessibility ensures inclusivity, often a legal requirement.
  - ARIA enhances dynamic content for assistive technologies.
  - Semantic HTML reduces the need for ARIA in many cases.
  - Regular audits catch issues early.

---

## Advanced Features

### Server Components (React 19)

```jsx
async function ServerComponent() {
  const data = await fetchDataFromServer();
  return <div>{data.name}</div>;
}

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <ServerComponent />
    </Suspense>
  );
}
```

### Portals

```jsx
import { createPortal } from 'react-dom';

function Modal({ children }) {
  return createPortal(
    <div className="modal">{children}</div>,
    document.getElementById('modal-root')
  );
}
```

### Concurrent Mode (useTransition)

```jsx
import { useTransition } from 'react';

function App() {
  const [isPending, startTransition] = useTransition();
  const [tab, setTab] = useState('home');

  const handleTabChange = newTab => {
    startTransition(() => {
      setTab(newTab);
    });
  };

  return (
    <div>
      <button onClick={() => handleTabChange('about')}>About</button>
      {isPending ? 'Loading...' : tab}
    </div>
  );
}
```

- **Approaches**:
  - **Server Components**: Server-side rendering, Next.js 13+.
  - **Portals**: Render outside component hierarchy.
  - **useTransition**: Prioritize urgent updates.
- **Best Practices**:
  - Use Server Components for data-heavy pages.
  - Ensure portal target exists in DOM.
  - Test Concurrent Mode in `StrictMode`.

**Explanation**:
- Server Components reduce client-side JavaScript, improving performance.
- Portals are ideal for modals, maintaining React’s event system.
- `useTransition` enhances UX by keeping UI responsive during heavy updates.

---

## Best Practices

- **Code Organization**: Group components logically, use barrel files.
- **Performance**: Memoize selectively, use code splitting.
- **Accessibility**: Follow WCAG, test with assistive tools.
- **Testing**: Prioritize user behavior, mock dependencies.
- **Type Safety**: Use TypeScript for large projects.
- **Version Control**: Pin dependencies, test upgrades.

**Explanation**:
- Structured practices ensure scalability and maintainability.
- Accessibility and performance are critical for user satisfaction.
- TypeScript and testing reduce bugs in production.

---

## Common React APIs & Hooks

- **Core**: `React.createElement`, `React.Fragment`, `React.memo`, `React.lazy`, `React.createContext`, `React.forwardRef`.
- **Hooks**: `useState`, `useEffect`, `useRef`, `useMemo`, `useCallback`, `useContext`, `useReducer`, `useTransition`, `useId`.
- **Experimental**: `use`, `useOptimistic`.
- **Router**: `useParams`, `useNavigate`.

**Explanation**:
- Hooks are central to modern React, replacing class patterns.
- Experimental APIs require caution but offer future-ready features.
- Stay updated with React’s evolving ecosystem.

---

## React Shorthands & Patterns

```jsx
// Fragment shorthand
const Component = () => (
  <>
    <h1>Title</h1>
    <p>Content</p>
  </>
);

// Implicit return
const Button = ({ text }) => <button>{text}</button>;

// Spread props
function Input(props) {
  return <input {...props} />;
}

// Dynamic classes with clsx
import clsx from 'clsx';
function Status({ isActive }) {
  return <div className={clsx('status', { active: isActive })}>Status</div>;
}
```

**Explanation**:
- Shorthands reduce boilerplate, improving readability.
- `clsx` simplifies conditional class names.
- Spread props are powerful but use cautiously to avoid passing unnecessary props.

---

## Cheat Codes

```jsx
// Debug renders
function Component() {
  useEffect(() => console.log('Rendered'), []);
  return <div>Debug</div>;
}

// Strict Mode
import { StrictMode } from 'react';
function App() {
  return (
    <StrictMode>
      <Main />
    </StrictMode>
  );
}

// Visually hidden for a11y
const VisuallyHidden = ({ children }) => (
  <span style={{ position: 'absolute', width: 1, height: 1, clip: 'rect(0, 0, 0, 0)' }}>
    {children}
  </span>
);
```

**Explanation**:
- Debug logs help trace render issues.
- `StrictMode` ensures future compatibility.
- Visually hidden elements maintain accessibility without visual impact.