# Complete React.js Course - Beginner Friendly 🚀

[![React](https://img.shields.io/badge/React-18.0+-blue.svg)](https://reactjs.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A comprehensive guide to learning React.js from scratch. This repository contains everything you need to become proficient in React development.

## 📚 Table of Contents

- [What is React?](#what-is-react)
- [Getting Started](#getting-started)
- [Core Concepts](#core-concepts)
  - [JSX - JavaScript XML](#jsx---javascript-xml)
  - [Components](#components)
  - [Props](#props)
  - [State](#state)
  - [Event Handling](#event-handling)
  - [Conditional Rendering](#conditional-rendering)
  - [Lists and Keys](#lists-and-keys)
  - [Forms](#forms)
- [Advanced Concepts](#advanced-concepts)
  - [Hooks](#hooks)
  - [Component Lifecycle](#component-lifecycle)
  - [Context API](#context-api)
  - [Error Boundaries](#error-boundaries)
  - [Higher-Order Components (HOCs)](#higher-order-components-hocs)
  - [Render Props](#render-props)
- [Routing](#routing)
- [State Management](#state-management)
- [Testing](#testing)
- [Performance Optimization](#performance-optimization)
- [Best Practices](#best-practices)
- [Project Structure](#project-structure)
- [Deployment](#deployment)
- [Resources](#resources)

## What is React?

React is a JavaScript library for building user interfaces, especially web applications. Think of it like building blocks for websites - you create small pieces (components) and combine them to build complex applications.

### Why React?

**Problem:** Traditional web development meant writing lots of repetitive code and manually updating the DOM (webpage elements) whenever data changed. This was slow and error-prone.

**Solution:** React solves this by:
- Creating reusable UI components (like Lego blocks)
- Automatically updating the webpage when data changes
- Making code easier to organize and maintain

### Key Features

- **Component-Based:** Build encapsulated components that manage their own state
- **Virtual DOM:** React creates a virtual copy of your webpage in memory, compares changes, and updates only what's necessary - making it super fast!
- **Reusable:** Write a component once, use it everywhere
- **Declarative:** Just describe what you want the UI to look like, React handles the "how"

### Real-World Analogy

Think of React like a restaurant kitchen:
- **Components** = Different stations (salad station, grill, dessert station)
- **Props** = Ingredients passed between stations
- **State** = Current status of each dish being prepared
- **Virtual DOM** = The head chef who coordinates everything efficiently

## Getting Started

### Prerequisites

- Basic knowledge of HTML, CSS, and JavaScript
- Node.js (version 14 or higher)
- Code editor (VS Code recommended)

### Installation

#### Option 1: Create React App Vite (Faster alternative)

```bash
# Create new project (Vite will show options)
npm create vite@latest my-react-app # project name is "my-react-app"
 
# When prompted, select:
# ✔ Select a framework: › React
# ✔ Select a variant: › TypeScript + SWC (or JavaScript + SWC for JS only)
 
cd my-react-app
npm install # npm i
```

#### Option 2: Online Playground

- [CodeSandbox](https://codesandbox.io)
- [CodePen](https://codepen.io)
- [StackBlitz](https://stackblitz.com)

### Project Structure

```
my-first-app/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── components/
│   ├── hooks/
│   ├── utils/
│   ├── App.js
│   ├── App.css
│   ├── index.js
│   └── index.css
├── package.json
└── README.md
```

## Core Concepts

### JSX - JavaScript XML

JSX lets you write HTML-like code in JavaScript. It's like mixing HTML and JavaScript together!

#### Why JSX?

**Problem:** Creating HTML elements in JavaScript was messy and hard to read:

```javascript
const element = React.createElement('div', null, 
  React.createElement('h1', null, 'Hello'),
  React.createElement('p', null, 'Welcome to React')
);
```

**Solution:** JSX makes it look like HTML:

```jsx
const element = (
  <div>
    <h1>Hello</h1>
    <p>Welcome to React</p>
  </div>
);
```

#### JSX Rules

1. **Single Parent Element:** Wrap multiple elements in one parent

```jsx
// ❌ Wrong
const element = (
  <h1>Title</h1>
  <p>Description</p>
);

// ✅ Correct
const element = (
  <div>
    <h1>Title</h1>
    <p>Description</p>
  </div>
);

// ✅ Or use Fragment
const element = (
  <>
    <h1>Title</h1>
    <p>Description</p>
  </>
);
```

2. **JavaScript Expressions:** Use curly braces `{}`

```jsx
const name = "John";
const age = 25;

const element = (
  <div>
    <h1>Hello, {name}!</h1>
    <p>You are {age} years old</p>
    <p>Next year you'll be {age + 1}</p>
  </div>
);
```

3. **HTML Attributes in camelCase**

```jsx
// ❌ HTML way
<div class="container" onclick="handleClick()">

// ✅ JSX way
<div className="container" onClick={handleClick}>
```

### Components

Components are like custom HTML elements. Think of them as reusable pieces of UI.

#### Why Components?

**Problem:** Copying and pasting the same HTML code everywhere. If you need to change something, you have to update it in multiple places.

**Solution:** Create a component once, use it anywhere. Change it once, updates everywhere!

#### Types of Components

1. **Presentational Components** - Just show data (like a business card)
2. **Container Components** - Handle logic and pass data to other components (like a form controller)
3. **Reusable Components** - Can be used anywhere (like buttons, inputs)

#### Functional Components (Modern Way)

```jsx
// Simple component
function Welcome() {
  return <h1>Hello, World!</h1>;
}

// Arrow function component
const Welcome = () => {
  return <h1>Hello, World!</h1>;
};

// Using the component
function App() {
  return (
    <div>
      <Welcome />
      <Welcome />
      <Welcome />
    </div>
  );
}
```

#### Real-World Example: User Card

```jsx
function UserCard() {
  return (
    <div className="user-card">
      <img src="https://via.placeholder.com/100" alt="User Avatar" />
      <h3>John Doe</h3>
      <p>Software Developer</p>
      <button>Follow</button>
    </div>
  );
}

// CSS
.user-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  max-width: 200px;
}
```

### Props

Props (properties) are how you pass data from parent to child components. Think of them like function parameters.

#### Why Props?

**Problem:** Components need different data to display. A UserCard component should show different users, not the same person every time!

**Solution:** Props let you pass data into components, making them flexible and reusable.

#### Key Points

- Props flow downward (parent → child)
- Props are read-only (child cannot change them)
- Props make components reusable

#### Basic Props Example

```jsx
// Child component that receives props
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Parent component that passes props
function App() {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
      <Greeting name="Charlie" />
    </div>
  );
}
```

#### Props with Destructuring

```jsx
// Instead of props.name, props.age
function UserInfo({ name, age, city }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>City: {city}</p>
    </div>
  );
}

function App() {
  return (
    <UserInfo 
      name="Sarah" 
      age={28} 
      city="New York" 
    />
  );
}
```

### State

State is data that can change over time. When state changes, React re-renders the component.

#### Why State?

**Problem:** Web applications need to respond to user interactions. Clicking buttons, typing in forms, loading data - the webpage needs to update!

**Solution:** State lets components "remember" information and update the UI when that information changes.

#### When to Use State

- User input (form fields, checkboxes)
- Current selection (active tab, selected item)
- Loading status (is data being fetched?)
- Toggle states (show/hide, on/off)

#### useState Hook

```jsx
import React, { useState } from 'react';

function Counter() {
  // useState returns [currentValue, functionToUpdateValue]
  const [count, setCount] = useState(0); // 0 is initial value

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
      <button onClick={() => setCount(count - 1)}>
        Decrease
      </button>
      <button onClick={() => setCount(0)}>
        Reset
      </button>
    </div>
  );
}
```

### Event Handling

React handles events using synthetic events, which work the same across all browsers.

#### Common Events

- `onClick` - Mouse clicks
- `onChange` - Input field changes
- `onSubmit` - Form submissions
- `onMouseOver/onMouseOut` - Hover effects
- `onKeyPress` - Keyboard input

#### Click Events

```jsx
function ButtonExample() {
  const handleClick = () => {
    alert("Button clicked!");
  };

  const handleClickWithParameter = (message) => {
    alert(message);
  };

  return (
    <div>
      <button onClick={handleClick}>
        Simple Click
      </button>
      
      <button onClick={() => handleClickWithParameter("Hello!")}>
        Click with Parameter
      </button>
    </div>
  );
}
```

#### Form Events

```jsx
function FormExample() {
  const [inputValue, setInputValue] = useState("");

  const handleSubmit = (event) => {
    event.preventDefault(); // Prevent page refresh
    console.log("Submitted:", inputValue);
  };

  const handleChange = (event) => {
    setInputValue(event.target.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text"
        value={inputValue}
        onChange={handleChange}
        placeholder="Enter something..."
      />
      <button type="submit">Submit</button>
      <p>You typed: {inputValue}</p>
    </form>
  );
}
```

### Conditional Rendering

Show different content based on conditions, like if-else statements for your UI.

#### If-Else with &&

```jsx
function WelcomeMessage({ isLoggedIn, username }) {
  return (
    <div>
      {isLoggedIn && <h1>Welcome back, {username}!</h1>}
      {!isLoggedIn && <h1>Please log in</h1>}
    </div>
  );
}
```

#### Ternary Operator

```jsx
function LoginButton({ isLoggedIn, onLogin, onLogout }) {
  return (
    <button onClick={isLoggedIn ? onLogout : onLogin}>
      {isLoggedIn ? "Logout" : "Login"}
    </button>
  );
}
```

### Lists and Keys

Render arrays of data as lists. Keys help React identify which items have changed.

#### Basic List

```jsx
function FruitList() {
  const fruits = ["Apple", "Banana", "Orange", "Grape"];

  return (
    <ul>
      {fruits.map((fruit, index) => (
        <li key={index}>{fruit}</li>
      ))}
    </ul>
  );
}
```

#### List with Objects

```jsx
function UserList() {
  const users = [
    { id: 1, name: "Alice", age: 25 },
    { id: 2, name: "Bob", age: 30 },
    { id: 3, name: "Charlie", age: 28 }
  ];

  return (
    <div>
      {users.map(user => (
        <div key={user.id} className="user-card">
          <h3>{user.name}</h3>
          <p>Age: {user.age}</p>
        </div>
      ))}
    </div>
  );
}
```

### Forms

Handle user input with controlled components.

#### Controlled Components

```jsx
function ContactForm() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    message: "",
    subscribe: false
  });

  const handleInputChange = (event) => {
    const { name, value, type, checked } = event.target;
    setFormData(prev => ({
      ...prev,
      [name]: type === 'checkbox' ? checked : value
    }));
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log("Form submitted:", formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          Name:
          <input
            type="text"
            name="name"
            value={formData.name}
            onChange={handleInputChange}
            required
          />
        </label>
      </div>
      <div>
        <label>
          Email:
          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={handleInputChange}
            required
          />
        </label>
      </div>
      <div>
        <label>
          Message:
          <textarea
            name="message"
            value={formData.message}
            onChange={handleInputChange}
            rows="4"
          />
        </label>
      </div>
      <div>
        <label>
          <input
            type="checkbox"
            name="subscribe"
            checked={formData.subscribe}
            onChange={handleInputChange}
          />
          Subscribe to newsletter
        </label>
      </div>
      <button type="submit">Submit</button>
    </form>
  );
}
```

## Advanced Concepts

### Hooks

Hooks let you use state and other React features in functional components.

#### Hook Rules (Very Important!)

1. Only call hooks at the top level - Not inside loops, conditions, or nested functions
2. Only call hooks from React functions - Functional components or custom hooks

#### useEffect Hook

```jsx
import React, { useState, useEffect } from 'react';

// Effect that runs after every render
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    // Cleanup function
    return () => clearInterval(interval);
  }, []); // Empty dependency array means effect runs once

  return <h1>Timer: {seconds} seconds</h1>;
}
```

#### Custom Hooks

```jsx
// Custom hook for fetching data
function useApi(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then(response => response.json())
      .then(data => {
        setData(data);
        setLoading(false);
      })
      .catch(error => {
        setError(error);
        setLoading(false);
      });
  }, [url]);

  return { data, loading, error };
}

// Using the custom hook
function PostList() {
  const { data, loading, error } = useApi('https://jsonplaceholder.typicode.com/posts');

  if (loading) return <p>Loading posts...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <div>
      {data.slice(0, 5).map(post => (
        <div key={post.id}>
          <h3>{post.title}</h3>
          <p>{post.body}</p>
        </div>
      ))}
    </div>
  );
}
```

### Component Lifecycle

Understanding when components mount, update, and unmount.

#### The Three Phases

1. **Mounting** = Birth 👶 - Component is created and added to the DOM
2. **Updating** = Growing/Living 🌱 - Component receives new props or state changes
3. **Unmounting** = Death 💀 - Component is removed from the DOM

#### Lifecycle with useEffect

```jsx
function LifecycleExample({ name }) {
  const [count, setCount] = useState(0);

  // Component did mount (runs once)
  useEffect(() => {
    console.log("Component mounted");
    
    // Component will unmount (cleanup)
    return () => {
      console.log("Component will unmount");
    };
  }, []);

  // Component did update (runs when count changes)
  useEffect(() => {
    console.log("Count updated to:", count);
  }, [count]);

  return (
    <div>
      <h2>Hello, {name}</h2>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### Context API

Share data between components without passing props down manually.

#### Complete Context Example

```jsx
import React, { createContext, useContext, useReducer } from 'react';

// Create contexts
const UserContext = createContext();
const CartContext = createContext();

// Reducer for cart
function cartReducer(state, action) {
  switch (action.type) {
    case 'ADD_ITEM':
      return {
        ...state,
        items: [...state.items, action.payload],
        total: state.total + action.payload.price
      };
    case 'REMOVE_ITEM':
      const itemToRemove = state.items.find(item => item.id === action.payload);
      return {
        ...state,
        items: state.items.filter(item => item.id !== action.payload),
        total: state.total - (itemToRemove ? itemToRemove.price : 0)
      };
    default:
      return state;
  }
}

// Providers
function AppProvider({ children }) {
  const [user, setUser] = useState({ name: "John Doe", email: "john@example.com" });
  const [cart, dispatch] = useReducer(cartReducer, { items: [], total: 0 });

  return (
    <UserContext.Provider value={{ user, setUser }}>
      <CartContext.Provider value={{ cart, dispatch }}>
        {children}
      </CartContext.Provider>
    </UserContext.Provider>
  );
}

// Components using context
function UserProfile() {
  const { user } = useContext(UserContext);
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}

function ShoppingCart() {
  const { cart, dispatch } = useContext(CartContext);

  const addItem = () => {
    dispatch({
      type: 'ADD_ITEM',
      payload: { id: Date.now(), name: 'New Item', price: 10 }
    });
  };

  return (
    <div>
      <h3>Cart ({cart.items.length} items)</h3>
      <p>Total: ${cart.total}</p>
      <button onClick={addItem}>Add Item</button>
      <ul>
        {cart.items.map(item => (
          <li key={item.id}>
            {item.name} - ${item.price}
            <button onClick={() => dispatch({ type: 'REMOVE_ITEM', payload: item.id })}>
              Remove
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### Error Boundaries

Error boundaries are React components that catch JavaScript errors in their child component tree.

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null, errorInfo: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    this.setState({
      error: error,
      errorInfo: errorInfo
    });
  }

  render() {
    if (this.state.hasError) {
      return (
        <div style={{ padding: '20px', border: '1px solid red', borderRadius: '5px' }}>
          <h2>Something went wrong!</h2>
          <details style={{ whiteSpace: 'pre-wrap' }}>
            {this.state.error && this.state.error.toString()}
            <br />
            {this.state.errorInfo.componentStack}
          </details>
        </div>
      );
    }

    return this.props.children;
  }
}

// Usage
function App() {
  return (
    <ErrorBoundary>
      <Header />
      <MainContent />
      <Footer />
    </ErrorBoundary>
  );
}
```

### Higher-Order Components (HOCs)

A higher-order component is a function that takes a component and returns a new component with additional functionality.

```jsx
// HOC for authentication
function withAuth(WrappedComponent) {
  return function AuthenticatedComponent(props) {
    const [user, setUser] = useState(null);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
      // Check authentication status
      checkAuth().then(user => {
        setUser(user);
        setLoading(false);
      });
    }, []);

    if (loading) {
      return <div>Loading...</div>;
    }

    if (!user) {
      return <div>Please log in to access this content.</div>;
    }

    return <WrappedComponent {...props} user={user} />;
  };
}

// Usage
const ProtectedDashboard = withAuth(Dashboard);

function App() {
  return (
    <div>
      <ProtectedDashboard />
    </div>
  );
}
```

### Render Props

A component with a render prop takes a function that returns a React element and calls it.

```jsx
// Mouse tracker component using render props
function Mouse({ render }) {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  const handleMouseMove = (event) => {
    setPosition({
      x: event.clientX,
      y: event.clientY
    });
  };

  return (
    <div onMouseMove={handleMouseMove} style={{ height: '100vh' }}>
      {render(position)}
    </div>
  );
}

// Usage
function App() {
  return (
    <Mouse
      render={({ x, y }) => (
        <h1>The mouse position is ({x}, {y})</h1>
      )}
    />
  );
}
```

## Routing

Navigate between different pages/views in your app using React Router.

### Installation

```bash
npm install react-router-dom
```

### Basic Routing Setup

```jsx
import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link, useParams, Navigate } from 'react-router-dom';

// Page components
function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <p>Welcome to our website!</p>
    </div>
  );
}

function About() {
  return (
    <div>
      <h1>About Page</h1>
      <p>Learn more about us!</p>
    </div>
  );
}

function Contact() {
  return (
    <div>
      <h1>Contact Page</h1>
      <p>Get in touch with us!</p>
    </div>
  );
}

function UserProfile() {
  const { userId } = useParams();
  return (
    <div>
      <h1>User Profile</h1>
      <p>Viewing profile for user: {userId}</p>
    </div>
  );
}

function NotFound() {
  return (
    <div>
      <h1>404 - Page Not Found</h1>
      <Link to="/">Go Home</Link>
    </div>
  );
}

// Navigation component
function Navigation() {
  return (
    <nav style={{ padding: '20px', backgroundColor: '#f0f0f0', marginBottom: '20px' }}>
      <Link to="/" style={{ marginRight: '20px' }}>Home</Link>
      <Link to="/about" style={{ marginRight: '20px' }}>About</Link>
      <Link to="/contact" style={{ marginRight: '20px' }}>Contact</Link>
      <Link to="/user/123">User Profile</Link>
    </nav>
  );
}

// Main App with routing
function App() {
  return (
    <Router>
      <div>
        <Navigation />
        <div style={{ padding: '20px' }}>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/contact" element={<Contact />} />
            <Route path="/user/:userId" element={<UserProfile />} />
            <Route path="/404" element={<NotFound />} />
            <Route path="*" element={<Navigate to="/404" />} />
          </Routes>
        </div>
      </div>
    </Router>
  );
}
```

### Protected Routes

```jsx
function ProtectedRoute({ children }) {
  const isAuthenticated = useAuth(); // Custom hook for auth

  return isAuthenticated ? children : <Navigate to="/login" />;
}

// Usage
<Route
  path="/dashboard"
  element={
    <ProtectedRoute>
      <Dashboard />
    </ProtectedRoute>
  }
/>
```

## State Management

### Local State vs Global State

- **Local State**: Data that only one component needs (form inputs, toggles)
- **Global State**: Data that multiple components need (user info, theme, shopping cart)

### Options for Global State

1. **Context API** - Built into React, good for medium apps
2. **Redux** - Most popular, best for large apps
3. **Zustand** - Lightweight alternative to Redux
4. **Recoil** - Facebook's experimental state management

### Redux Example

#### Installation
```bash
npm install @reduxjs/toolkit react-redux
```

#### Setting up Redux

```jsx
// store.js
import { configureStore, createSlice } from '@reduxjs/toolkit';

// Create a slice
const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    }
  }
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

// Configure store
export const store = configureStore({
  reducer: {
    counter: counterSlice.reducer
  }
});
```

```jsx
// App.js
import { Provider } from 'react-redux';
import { store } from './store';
import Counter from './Counter';

function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}
```

```jsx
// Counter.js
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement, incrementByAmount } from './store';

function Counter() {
  const count = useSelector(state => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <span>{count}</span>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
      <button onClick={() => dispatch(incrementByAmount(5))}>+5</button>
    </div>
  );
}
```

## Testing

### Testing Libraries

- **Jest**: JavaScript testing framework (comes with Create React App)
- **React Testing Library**: Simple utilities for testing React components
- **Enzyme**: Alternative to React Testing Library (older)

### Installation

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

### Basic Component Test

```jsx
// Button.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import '@testing-library/jest-dom';
import Button from './Button';

describe('Button Component', () => {
  test('renders button with correct text', () => {
    render(<Button>Click me</Button>);
    const buttonElement = screen.getByText(/click me/i);
    expect(buttonElement).toBeInTheDocument();
  });

  test('calls onClick handler when clicked', () => {
    const handleClick = jest.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    
    const buttonElement = screen.getByText(/click me/i);
    fireEvent.click(buttonElement);
    
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  test('is disabled when disabled prop is true', () => {
    render(<Button disabled>Click me</Button>);
    const buttonElement = screen.getByText(/click me/i);
    expect(buttonElement).toBeDisabled();
  });
});
```

### Testing Hooks

```jsx
// useCounter.test.js
import { renderHook, act } from '@testing-library/react';
import useCounter from './useCounter';

describe('useCounter', () => {
  test('should initialize with 0', () => {
    const { result } = renderHook(() => useCounter());
    expect(result.current.count).toBe(0);
  });

  test('should increment counter', () => {
    const { result } = renderHook(() => useCounter());

    act(() => {
      result.current.increment();
    });

    expect(result.current.count).toBe(1);
  });
});
```

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm test -- --watch

# Run tests with coverage
npm test -- --coverage
```

## Performance Optimization

### React.memo

Memoize components to prevent unnecessary re-renders:

```jsx
import React, { memo } from 'react';

const ExpensiveComponent = memo(function ExpensiveComponent({ name, age }) {
  console.log('ExpensiveComponent rendered');
  return (
    <div>
      <h3>{name}</h3>
      <p>Age: {age}</p>
    </div>
  );
});

// Only re-renders if name or age changes
```

### useMemo

Memoize expensive calculations:

```jsx
import { useMemo } from 'react';

function ExpensiveList({ items, filter }) {
  const filteredItems = useMemo(() => {
    console.log('Filtering items...');
    return items.filter(item => 
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
  }, [items, filter]);

  return (
    <ul>
      {filteredItems.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

### useCallback

Memoize callback functions:

```jsx
import { useCallback } from 'react';

function TodoList({ todos, onToggle }) {
  const handleToggle = useCallback((id) => {
    onToggle(id);
  }, [onToggle]);

  return (
    <div>
      {todos.map(todo => (
        <TodoItem 
          key={todo.id} 
          todo={todo} 
          onToggle={handleToggle} 
        />
      ))}
    </div>
  );
}
```

### Code Splitting

Split your code into smaller chunks for better performance:

```jsx
import { lazy, Suspense } from 'react';

// Lazy load components
const LazyComponent = lazy(() => import('./LazyComponent'));
const Dashboard = lazy(() => import('./Dashboard'));

function App() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <Routes>
          <Route path="/dashboard" element={<Dashboard />} />
          <Route path="/lazy" element={<LazyComponent />} />
        </Routes>
      </Suspense>
    </div>
  );
}
```

### Virtual Scrolling

For large lists, use virtual scrolling:

```jsx
import { FixedSizeList as List } from 'react-window';

function VirtualizedList({ items }) {
  const Row = ({ index, style }) => (
    <div style={style}>
      {items[index].name}
    </div>
  );

  return (
    <List
      height={400}
      itemCount={items.length}
      itemSize={50}
    >
      {Row}
    </List>
  );
}
```

## Best Practices

### 1. Component Structure

```jsx
// Good: Small, focused components
function Button({ onClick, children, variant = 'primary', disabled = false }) {
  const className = `btn btn-${variant} ${disabled ? 'btn-disabled' : ''}`;
  
  return (
    <button 
      className={className} 
      onClick={onClick} 
      disabled={disabled}
      aria-label={typeof children === 'string' ? children : 'Button'}
    >
      {children}
    </button>
  );
}

// Good: Separate concerns
function UserCard({ user, onEdit, onDelete }) {
  return (
    <div className="user-card">
      <UserAvatar src={user.avatar} alt={`${user.name}'s avatar`} />
      <UserInfo name={user.name} email={user.email} />
      <UserActions 
        onEdit={() => onEdit(user.id)} 
        onDelete={() => onDelete(user.id)} 
      />
    </div>
  );
}
```

### 2. State Management

```jsx
// Good: Keep state as simple as possible
function TodoList() {
  const [todos, setTodos] = useState([]);
  const [filter, setFilter] = useState('all');
  const [newTodo, setNewTodo] = useState('');

  // Good: Use functional updates
  const addTodo = (text) => {
    if (text.trim()) {
      setTodos(prev => [
        ...prev, 
        { id: Date.now(), text: text.trim(), completed: false }
      ]);
      setNewTodo('');
    }
  };

  // Good: Compute derived state
  const filteredTodos = useMemo(() => {
    return todos.filter(todo => {
      if (filter === 'completed') return todo.completed;
      if (filter === 'active') return !todo.completed;
      return true;
    });
  }, [todos, filter]);

  return (
    <div className="todo-app">
      <TodoInput value={newTodo} onChange={setNewTodo} onSubmit={addTodo} />
      <TodoFilter currentFilter={filter} onFilterChange={setFilter} />
      <TodoItems todos={filteredTodos} onToggle={toggleTodo} />
    </div>
  );
}
```

### 3. Error Handling

```jsx
// Good: Handle errors gracefully
function DataFetcher({ url }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        setError(null);
        const response = await fetch(url);
        
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage message={error} onRetry={() => window.location.reload()} />;
  if (!data) return <EmptyState />;

  return <DataDisplay data={data} />;
}
```

### 4. Accessibility

```jsx
// Good: Accessible components
function Modal({ isOpen, onClose, title, children }) {
  const modalRef = useRef();

  useEffect(() => {
    if (isOpen) {
      modalRef.current?.focus();
    }
  }, [isOpen]);

  const handleKeyDown = (event) => {
    if (event.key === 'Escape') {
      onClose();
    }
  };

  if (!isOpen) return null;

  return (
    <div 
      className="modal-overlay" 
      onClick={onClose}
      role="dialog"
      aria-modal="true"
      aria-labelledby="modal-title"
    >
      <div 
        className="modal-content" 
        onClick={(e) => e.stopPropagation()}
        ref={modalRef}
        tabIndex={-1}
        onKeyDown={handleKeyDown}
      >
        <div className="modal-header">
          <h2 id="modal-title">{title}</h2>
          <button 
            onClick={onClose}
            aria-label="Close modal"
            className="modal-close"
          >
            ×
          </button>
        </div>
        <div className="modal-body">
          {children}
        </div>
      </div>
    </div>
  );
}
```

### 5. Code Organization

```jsx
// Good: Custom hooks for reusable logic
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(`Error reading localStorage key "${key}":`, error);
      return initialValue;
    }
  });

  const setValue = useCallback((value) => {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(`Error setting localStorage key "${key}":`, error);
    }
  }, [key, storedValue]);

  return [storedValue, setValue];
}

// Usage
function Settings() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  const [language, setLanguage] = useLocalStorage('language', 'en');

  return (
    <div>
      <ThemeSelector value={theme} onChange={setTheme} />
      <LanguageSelector value={language} onChange={setLanguage} />
    </div>
  );
}
```

## Project Structure

### Recommended Folder Structure

```
src/
├── components/           # Reusable UI components
│   ├── common/          # Common components (Button, Input, Modal)
│   ├── forms/           # Form-specific components
│   └── layout/          # Layout components (Header, Footer, Sidebar)
├── pages/               # Page components
│   ├── Home/
│   ├── About/
│   └── Contact/
├── hooks/               # Custom hooks
│   ├── useAuth.js
│   ├── useApi.js
│   └── useLocalStorage.js
├── context/             # Context providers
│   ├── AuthContext.js
│   └── ThemeContext.js
├── services/            # API calls and external services
│   ├── api.js
│   └── auth.js
├── utils/               # Utility functions
│   ├── helpers.js
│   ├── constants.js
│   └── validators.js
├── styles/              # Global styles
│   ├── globals.css
│   ├── variables.css
│   └── components.css
├── assets/              # Static assets
│   ├── images/
│   ├── icons/
│   └── fonts/
├── types/               # TypeScript type definitions (if using TS)
├── __tests__/           # Test files
├── App.js
├── index.js
└── setupTests.js
```

### Component File Structure

```jsx
// components/UserCard/index.js
export { default } from './UserCard';

// components/UserCard/UserCard.js
import React from 'react';
import './UserCard.css';
import { useUser } from '../../hooks/useUser';
import Button from '../common/Button';

function UserCard({ userId, onEdit, onDelete }) {
  const { user, loading, error } = useUser(userId);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return (
    <div className="user-card">
      <div className="user-card__header">
        <img 
          src={user.avatar} 
          alt={`${user.name}'s avatar`}
          className="user-card__avatar"
        />
        <h3 className="user-card__name">{user.name}</h3>
      </div>
      <div className="user-card__body">
        <p className="user-card__email">{user.email}</p>
        <p className="user-card__role">{user.role}</p>
      </div>
      <div className="user-card__actions">
        <Button variant="secondary" onClick={() => onEdit(user.id)}>
          Edit
        </Button>
        <Button variant="danger" onClick={() => onDelete(user.id)}>
          Delete
        </Button>
      </div>
    </div>
  );
}

export default UserCard;

// components/UserCard/UserCard.css
.user-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.user-card__header {
  display: flex;
  align-items: center;
  margin-bottom: 12px;
}

.user-card__avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  margin-right: 12px;
}

.user-card__name {
  margin: 0;
  font-size: 1.2em;
  color: #333;
}

.user-card__actions {
  display: flex;
  gap: 8px;
  margin-top: 12px;
}
```

## Deployment

### Build for Production

```bash
# Create optimized production build
npm run build

# Serve production build locally (for testing)
npx serve -s build
```

### Deployment Options

#### 1. Netlify (Easy)

1. Build your app: `npm run build`
2. Drag and drop the `build` folder to [Netlify](https://netlify.com)
3. Or connect your GitHub repository for automatic deployments

#### 2. Vercel (Easy)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Or connect GitHub repository at vercel.com
```

#### 3. GitHub Pages

```bash
# Install gh-pages
npm install --save-dev gh-pages

# Add to package.json
"homepage": "https://yourusername.github.io/your-repo-name",
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}

# Deploy
npm run deploy
```

#### 4. AWS S3 + CloudFront

```bash
# Install AWS CLI and configure credentials
aws configure

# Build and sync to S3
npm run build
aws s3 sync build/ s3://your-bucket-name --delete

# Invalidate CloudFront cache
aws cloudfront create-invalidation --distribution-id YOUR_ID --paths "/*"
```

#### 5. Docker

```dockerfile
# Dockerfile
FROM node:16-alpine as build

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

COPY . ./
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

```bash
# Build and run Docker container
docker build -t my-react-app .
docker run -p 80:80 my-react-app
```

### Environment Variables

```bash
# .env.local
REACT_APP_API_URL=https://api.example.com
REACT_APP_API_KEY=your-api-key
REACT_APP_VERSION=1.0.0
```

```jsx
// Using environment variables
const apiUrl = process.env.REACT_APP_API_URL;
const apiKey = process.env.REACT_APP_API_KEY;

console.log('App version:', process.env.REACT_APP_VERSION);
```

## Resources

### Official Documentation

- [React Official Docs](https://react.dev/)
- [Create React App](https://create-react-app.dev/)
- [React Router](https://reactrouter.com/)
- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

### Popular Libraries

- **State Management**: [Redux Toolkit](https://redux-toolkit.js.org/), [Zustand](https://github.com/pmndrs/zustand), [Recoil](https://recoiljs.org/)
- **UI Libraries**: [Material-UI](https://mui.com/), [Ant Design](https://ant.design/), [Chakra UI](https://chakra-ui.com/)
- **Styling**: [Styled Components](https://styled-components.com/), [Emotion](https://emotion.sh/), [Tailwind CSS](https://tailwindcss.com/)
- **Forms**: [Formik](https://formik.org/), [React Hook Form](https://react-hook-form.com/)
- **HTTP Client**: [Axios](https://axios-http.com/), [React Query](https://tanstack.com/query/)
- **Animation**: [Framer Motion](https://www.framer.com/motion/), [React Spring](https://react-spring.io/)

### Learning Resources

- **Interactive**: [React Tutorial](https://react.dev/learn/tutorial-tic-tac-toe)
- **Video Courses**: [freeCodeCamp](https://www.freecodecamp.org/), [The Odin Project](https://www.theodinproject.com/)
- **Practice**: [Frontend Mentor](https://www.frontendmentor.io/), [Codewars](https://www.codewars.com/)
- **Books**: "Learning React" by Alex Banks & Eve Porcello

### Tools and Extensions

#### VS Code Extensions
- ES7+ React/Redux/React-Native snippets
- Bracket Pair Colorizer
- Auto Rename Tag
- Prettier - Code formatter
- ESLint
- GitLens

#### Browser Extensions
- React Developer Tools
- Redux DevTools

#### Development Tools
- [Storybook](https://storybook.js.org/) - Component development environment
- [React Devtools Profiler](https://react.dev/reference/react/Profiler) - Performance profiling
- [Why Did You Render](https://github.com/welldone-software/why-did-you-render) - Performance debugging

### TypeScript with React

```bash
# Create React app with TypeScript
npx create-react-app my-app --template typescript

# Or add TypeScript to existing project
npm install --save-dev typescript @types/node @types/react @types/react-dom
```

```tsx
// TypeScript component example
interface User {
  id: number;
  name: string;
  email: string;
}

interface UserCardProps {
  user: User;
  onEdit: (id: number) => void;
  onDelete: (id: number) => void;
}

const UserCard: React.FC<UserCardProps> = ({ user, onEdit, onDelete }) => {
  return (
    <div className="user-card">
      <h3>{user.name}</h3>
      <p>{user.email}</p>
      <button onClick={() => onEdit(user.id)}>Edit</button>
      <button onClick={() => onDelete(user.id)}>Delete</button>
    </div>
  );
};

export default UserCard;
```

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Add tests for your changes
5. Ensure all tests pass: `npm test`
6. Commit your changes: `git commit -am 'Add some feature'`
7. Push to the branch: `git push origin feature-name`
8. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- React team for creating an amazing library
- The open-source community for continuous contributions
- All the developers who have shared their knowledge and experiences

---

## Quick Start Checklist

- [ ] Install Node.js (version 14+)
- [ ] Create a new React app: `npx create-react-app my-app`
- [ ] Navigate to the project: `cd my-app`
- [ ] Start development server: `npm start`
- [ ] Open http://localhost:3000 in your browser
- [ ] Start building your first component!

## Next Steps

1. Complete the official [React tutorial](https://react.dev/learn/tutorial-tic-tac-tac-toe)
2. Build a small project (Todo app, Calculator, Weather app)
3. Learn React Router for multi-page applications
4. Explore state management solutions (Context API, Redux)
5. Learn testing with Jest and React Testing Library
6. Deploy your first React application
7. Join the React community and contribute to open source!

**Happy Coding! 🚀**

---

*If you find this guide helpful, please give it a ⭐ and share it with others!*
