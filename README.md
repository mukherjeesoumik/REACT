# Complete React.js Course - Beginner Friendly 🚀

[![React](https://img.shields.io/badge/React-18.0+-blue.svg)](https://reactjs.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A comprehensive guide to learning React.js from scratch with real code examples, console outputs, and practical debugging tips.

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
  - [Higher-Order Components](#higher-order-components)
- [Routing](#routing)
- [State Management](#state-management)
- [Testing](#testing)
- [Performance Optimization](#performance-optimization)
- [Best Practices](#best-practices)
- [Deployment](#deployment)
- [Debugging Tips](#debugging-tips)
- [Resources](#resources)

## What is React?

React is a JavaScript library for building user interfaces, especially web applications. Think of it like building blocks for websites - you create small pieces (components) and combine them to build complex applications.

### Why React?

**Problem:** Traditional web development meant writing lots of repetitive code and manually updating the DOM (webpage elements) whenever data changed.

**Solution:** React solves this by:
- Creating reusable UI components (like Lego blocks)
- Automatically updating the webpage when data changes (Virtual DOM)
- Making code easier to organize and maintain

### Key Features with Examples

```jsx
// Component-Based Architecture
function WelcomeCard({ name, role }) {
  console.log(`Rendering WelcomeCard for ${name}`);
  // Output: Rendering WelcomeCard for John Doe
  
  return (
    <div className="welcome-card">
      <h2>Welcome, {name}!</h2>
      <p>Role: {role}</p>
    </div>
  );
}

// Virtual DOM in Action
function Counter() {
  const [count, setCount] = useState(0);
  
  console.log(`Counter component rendered. Current count: ${count}`);
  // Output: Counter component rendered. Current count: 0
  // Output: Counter component rendered. Current count: 1
  // Output: Counter component rendered. Current count: 2
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

## Getting Started

### Installation and Setup

```bash
# Create new project (Vite will show options)
npm create vite@latest my-react-app # project name is "my-react-app"
 
# When prompted, select:
# ✔ Select a framework: › React
# ✔ Select a variant: › TypeScript + SWC (or JavaScript + SWC for JS only)
 
cd my-react-app
npm install # or npm i
```

**Console Output:**
```
Compiled successfully!

You can now view my-react-app in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.1.100:3000

Note that the development build is not optimized.
To create a production build, use npm run build.

webpack compiled with 1 warning
```

### Project Structure with Explanations

```
my-react-app/
├── public/
│   ├── index.html          # Main HTML file
│   └── favicon.ico         # Browser tab icon
├── src/
│   ├── App.js             # Main component
│   ├── App.css            # App styles
│   ├── index.js           # Entry point
│   └── index.css          # Global styles
├── package.json           # Dependencies and scripts
└── README.md             # Project documentation
```

## Core Concepts

### JSX - JavaScript XML

JSX lets you write HTML-like code in JavaScript. It gets compiled to regular JavaScript.

```jsx
// JSX Code
const element = <h1>Hello, World!</h1>;

// Compiles to:
const element = React.createElement('h1', null, 'Hello, World!');

console.log(element);
// Output: 
// {
//   type: 'h1',
//   props: { children: 'Hello, World!' },
//   key: null,
//   ref: null
// }
```

#### JSX with JavaScript Expressions

```jsx
function UserGreeting() {
  const user = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25
  };
  
  const isAdult = user.age >= 18;
  
  console.log('User data:', user);
  console.log('Is adult:', isAdult);
  // Output: User data: {firstName: 'John', lastName: 'Doe', age: 25}
  // Output: Is adult: true
  
  return (
    <div>
      <h1>Hello, {user.firstName} {user.lastName}!</h1>
      <p>Age: {user.age}</p>
      <p>Status: {isAdult ? 'Adult' : 'Minor'}</p>
      <p>Birth Year: {new Date().getFullYear() - user.age}</p>
    </div>
  );
}
```

**Rendered Output:**
```html
<div>
  <h1>Hello, John Doe!</h1>
  <p>Age: 25</p>
  <p>Status: Adult</p>
  <p>Birth Year: 1999</p>
</div>
```

#### JSX Rules and Common Mistakes

```jsx
// ❌ WRONG: Multiple elements without wrapper
function WrongComponent() {
  return (
    <h1>Title</h1>
    <p>Description</p>
  );
}
// Error: Adjacent JSX elements must be wrapped in an enclosing tag

// ✅ CORRECT: Using Fragment
function CorrectComponent() {
  return (
    <>
      <h1>Title</h1>
      <p>Description</p>
    </>
  );
}

// ❌ WRONG: Using 'class' instead of 'className'
<div class="container">Content</div>
// Warning: Invalid DOM property `class`. Did you mean `className`?

// ✅ CORRECT: Using 'className'
<div className="container">Content</div>
```

### Components

Components are reusable pieces of UI. Think of them as custom HTML elements.

```jsx
// Simple Functional Component
function Button({ text, onClick, disabled = false }) {
  console.log(`Button component rendered with text: "${text}"`);
  // Output: Button component rendered with text: "Click Me"
  
  const handleClick = () => {
    console.log(`Button "${text}" was clicked!`);
    // Output: Button "Click Me" was clicked!
    onClick && onClick();
  };
  
  return (
    <button 
      onClick={handleClick} 
      disabled={disabled}
      className={`btn ${disabled ? 'btn-disabled' : 'btn-active'}`}
    >
      {text}
    </button>
  );
}

// Using the Button component
function App() {
  const handleSave = () => {
    console.log('Save operation triggered');
    // Output: Save operation triggered
  };
  
  const handleDelete = () => {
    console.log('Delete operation triggered');
    // Output: Delete operation triggered
  };
  
  return (
    <div>
      <Button text="Save" onClick={handleSave} />
      <Button text="Delete" onClick={handleDelete} />
      <Button text="Disabled Button" disabled={true} />
    </div>
  );
}
```

#### Component Composition Example

```jsx
// Card Component
function Card({ children, title, className = '' }) {
  console.log(`Rendering Card with title: ${title}`);
  // Output: Rendering Card with title: User Profile
  
  return (
    <div className={`card ${className}`}>
      {title && <div className="card-header">{title}</div>}
      <div className="card-body">
        {children}
      </div>
    </div>
  );
}

// UserProfile Component
function UserProfile({ user }) {
  console.log('User profile data:', user);
  // Output: User profile data: {name: 'Alice', email: 'alice@example.com', role: 'Developer'}
  
  return (
    <Card title="User Profile" className="user-card">
      <div className="user-info">
        <h3>{user.name}</h3>
        <p>Email: {user.email}</p>
        <p>Role: {user.role}</p>
      </div>
    </Card>
  );
}

// Usage
function Dashboard() {
  const userData = {
    name: 'Alice Johnson',
    email: 'alice@example.com',
    role: 'Senior Developer'
  };
  
  return (
    <div className="dashboard">
      <UserProfile user={userData} />
    </div>
  );
}
```

### Props

Props are how you pass data from parent to child components.

```jsx
// Child Component
function ProductCard({ product, onAddToCart, onViewDetails }) {
  console.log('Product received via props:', product);
  // Output: Product received via props: {id: 1, name: 'Laptop', price: 999, inStock: true}
  
  const handleAddToCart = () => {
    console.log(`Adding ${product.name} to cart`);
    // Output: Adding Laptop to cart
    onAddToCart(product.id);
  };
  
  const handleViewDetails = () => {
    console.log(`Viewing details for ${product.name}`);
    // Output: Viewing details for Laptop
    onViewDetails(product.id);
  };
  
  return (
    <div className="product-card">
      <h3>{product.name}</h3>
      <p className="price">${product.price}</p>
      <p className={`stock ${product.inStock ? 'in-stock' : 'out-of-stock'}`}>
        {product.inStock ? 'In Stock' : 'Out of Stock'}
      </p>
      <div className="actions">
        <button 
          onClick={handleAddToCart} 
          disabled={!product.inStock}
        >
          Add to Cart
        </button>
                  <button onClick={handleCheckout} className="checkout-btn">
            Checkout
          </button>
        </>
      )}
    </div>
  );
}

// Header component using context
function Header() {
  const { user, isAuthenticated, logout, cart, theme, setTheme } = useApp();
  
  console.log('Header rendered for user:', user?.name || 'Guest');
  // Output: Header rendered for user: John Doe
  // Output: Header rendered for user: Guest
  
  const handleThemeToggle = () => {
    const newTheme = theme === 'light' ? 'dark' : 'light';
    console.log('Toggling theme to:', newTheme);
    // Output: Toggling theme to: dark
    setTheme(newTheme);
  };
  
  return (
    <header className={`app-header theme-${theme}`}>
      <div className="header-left">
        <h1>My Store</h1>
      </div>
      
      <div className="header-center">
        <nav>
          <a href="/">Home</a>
          <a href="/products">Products</a>
          <a href="/about">About</a>
        </nav>
      </div>
      
      <div className="header-right">
        <button onClick={handleThemeToggle}>
          {theme === 'light' ? '🌙' : '☀️'}
        </button>
        
        <div className="cart-icon">
          🛒 ({cart.items.length})
        </div>
        
        {isAuthenticated ? (
          <div className="user-menu">
            <span>Welcome, {user.name}</span>
            <button onClick={logout}>Logout</button>
          </div>
        ) : (
          <button onClick={() => console.log('Navigate to login')}>
            Login
          </button>
        )}
      </div>
    </header>
  );
}
```

## Performance Optimization

### React.memo and Optimization Patterns

```jsx
// Expensive component that should be memoized
const ExpensiveUserList = memo(function ExpensiveUserList({ users, onUserClick, sortOrder }) {
  console.log('ExpensiveUserList rendered with', users.length, 'users, sort:', sortOrder);
  // Output: ExpensiveUserList rendered with 1000 users, sort: name
  // This will only log when users or sortOrder actually changes
  
  const sortedUsers = useMemo(() => {
    console.log('Computing sorted users...');
    // Output: Computing sorted users...
    // This expensive computation only runs when users or sortOrder changes
    
    return users.sort((a, b) => {
      switch (sortOrder) {
        case 'name':
          return a.name.localeCompare(b.name);
        case 'email':
          return a.email.localeCompare(b.email);
        case 'joinDate':
          return new Date(b.joinDate) - new Date(a.joinDate);
        default:
          return 0;
      }
    });
  }, [users, sortOrder]);
  
  return (
    <div className="user-list">
      <p>Displaying {sortedUsers.length} users</p>
      {sortedUsers.map(user => (
        <UserCard
          key={user.id}
          user={user}
          onClick={onUserClick}
        />
      ))}
    </div>
  );
});

// Memoized user card component
const UserCard = memo(function UserCard({ user, onClick }) {
  console.log('UserCard rendered for:', user.name);
  // Output: UserCard rendered for: John Doe
  // This only logs when user prop actually changes
  
  const handleClick = useCallback(() => {
    console.log('User card clicked:', user.id);
    // Output: User card clicked: 123
    onClick(user.id);
  }, [user.id, onClick]);
  
  return (
    <div className="user-card" onClick={handleClick}>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
      <span className="join-date">{user.joinDate}</span>
    </div>
  );
});

// Parent component with optimized callbacks
function UserManagement() {
  const [users, setUsers] = useState([]);
  const [sortOrder, setSortOrder] = useState('name');
  const [selectedUser, setSelectedUser] = useState(null);
  
  console.log('UserManagement rendered, users:', users.length, 'selected:', selectedUser?.id);
  // Output: UserManagement rendered, users: 1000 selected: undefined
  // Output: UserManagement rendered, users: 1000 selected: 123
  
  // Memoized callback to prevent unnecessary re-renders
  const handleUserClick = useCallback((userId) => {
    console.log('Parent handling user click:', userId);
    // Output: Parent handling user click: 123
    
    const user = users.find(u => u.id === userId);
    setSelectedUser(user);
  }, [users]);
  
  // Memoized callback for sort change
  const handleSortChange = useCallback((newSort) => {
    console.log('Sort order changed:', newSort);
    // Output: Sort order changed: email
    setSortOrder(newSort);
  }, []);
  
  return (
    <div className="user-management">
      <div className="controls">
        <label>
          Sort by:
          <select value={sortOrder} onChange={(e) => handleSortChange(e.target.value)}>
            <option value="name">Name</option>
            <option value="email">Email</option>
            <option value="joinDate">Join Date</option>
          </select>
        </label>
      </div>
      
      <div className="content">
        <ExpensiveUserList
          users={users}
          onUserClick={handleUserClick}
          sortOrder={sortOrder}
        />
        
        {selectedUser && (
          <UserDetails user={selectedUser} />
        )}
      </div>
    </div>
  );
}
```

### Code Splitting and Lazy Loading

```jsx
import { lazy, Suspense, useState } from 'react';

// Lazy load components
const Dashboard = lazy(() => {
  console.log('Loading Dashboard component...');
  // Output: Loading Dashboard component...
  return import('./Dashboard');
});

const UserProfile = lazy(() => {
  console.log('Loading UserProfile component...');
  // Output: Loading UserProfile component...
  return import('./UserProfile');
});

const AdminPanel = lazy(() => {
  console.log('Loading AdminPanel component...');
  // Output: Loading AdminPanel component...
  return import('./AdminPanel');
});

function App() {
  const [currentView, setCurrentView] = useState('home');
  const [user] = useState({ role: 'admin' });
  
  console.log('App rendered, current view:', currentView);
  // Output: App rendered, current view: home
  // Output: App rendered, current view: dashboard
  
  const renderView = () => {
    console.log('Rendering view:', currentView);
    // Output: Rendering view: dashboard
    
    switch (currentView) {
      case 'dashboard':
        return <Dashboard />;
      case 'profile':
        return <UserProfile />;
      case 'admin':
        return user.role === 'admin' ? <AdminPanel /> : <div>Access denied</div>;
      default:
        return <div>Welcome to the Home Page</div>;
    }
  };
  
  return (
    <div className="app">
      <nav>
        <button onClick={() => setCurrentView('home')}>Home</button>
        <button onClick={() => setCurrentView('dashboard')}>Dashboard</button>
        <button onClick={() => setCurrentView('profile')}>Profile</button>
        {user.role === 'admin' && (
          <button onClick={() => setCurrentView('admin')}>Admin</button>
        )}
      </nav>
      
      <main>
        <Suspense
          fallback={
            <div className="loading">
              <p>Loading component...</p>
              <div className="spinner"></div>
            </div>
          }
        >
          {renderView()}
        </Suspense>
      </main>
    </div>
  );
}

// Example of preloading components
function NavigationWithPreload() {
  const [hoveredButton, setHoveredButton] = useState(null);
  
  const handleMouseEnter = (componentName) => {
    console.log('Preloading component:', componentName);
    // Output: Preloading component: dashboard
    
    setHoveredButton(componentName);
    
    // Preload component on hover
    switch (componentName) {
      case 'dashboard':
        import('./Dashboard');
        break;
      case 'profile':
        import('./UserProfile');
        break;
      case 'admin':
        import('./AdminPanel');
        break;
    }
  };
  
  return (
    <nav className="preload-nav">
      <button
        onMouseEnter={() => handleMouseEnter('dashboard')}
        onMouseLeave={() => setHoveredButton(null)}
        className={hoveredButton === 'dashboard' ? 'preloading' : ''}
      >
        Dashboard
      </button>
      <button
        onMouseEnter={() => handleMouseEnter('profile')}
        onMouseLeave={() => setHoveredButton(null)}
        className={hoveredButton === 'profile' ? 'preloading' : ''}
      >
        Profile
      </button>
    </nav>
  );
}
```

### Virtual Scrolling for Large Lists

```jsx
import { FixedSizeList as List } from 'react-window';

function VirtualizedDataGrid({ data }) {
  console.log('VirtualizedDataGrid with', data.length, 'items');
  // Output: VirtualizedDataGrid with 50000 items
  
  const [visibleRange, setVisibleRange] = useState({ start: 0, end: 0 });
  
  const Row = ({ index, style }) => {
    const item = data[index];
    
    // Only log for first few items to avoid console spam
    if (index < 5) {
      console.log('Rendering virtual row', index, ':', item.name);
      // Output: Rendering virtual row 0 : Item 1
      // Output: Rendering virtual row 1 : Item 2
    }
    
    return (
      <div style={style} className="virtual-row">
        <div className="item-id">#{item.id}</div>
        <div className="item-name">{item.name}</div>
        <div className="item-value">${item.value}</div>
        <div className="item-date">{item.date}</div>
      </div>
    );
  };
  
  const handleItemsRendered = ({ visibleStartIndex, visibleStopIndex }) => {
    console.log(`Visible items: ${visibleStartIndex} to ${visibleStopIndex}`);
    // Output: Visible items: 0 to 15
    // Output: Visible items: 10 to 25 (when scrolling)
    
    setVisibleRange({ start: visibleStartIndex, end: visibleStopIndex });
  };
  
  return (
    <div className="virtualized-grid">
      <div className="grid-header">
        <h2>Data Grid ({data.length.toLocaleString()} items)</h2>
        <p>Showing rows {visibleRange.start + 1} - {visibleRange.end + 1}</p>
      </div>
      
      <List
        height={600}
        itemCount={data.length}
        itemSize={50}
        onItemsRendered={handleItemsRendered}
        className="virtual-list"
      >
        {Row}
      </List>
    </div>
  );
}

// Generate large dataset for testing
function generateLargeDataset(count = 50000) {
  console.log('Generating dataset with', count, 'items');
  // Output: Generating dataset with 50000 items
  
  const startTime = performance.now();
  
  const data = Array.from({ length: count }, (_, index) => ({
    id: index + 1,
    name: `Item ${index + 1}`,
    value: Math.floor(Math.random() * 1000),
    date: new Date(Date.now() - Math.random() * 365 * 24 * 60 * 60 * 1000).toLocaleDateString()
  }));
  
  const endTime = performance.now();
  console.log(`Dataset generated in ${endTime - startTime}ms`);
  // Output: Dataset generated in 45.2ms
  
  return data;
}
```

## Error Boundaries and Error Handling

```jsx
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { 
      hasError: false, 
      error: null, 
      errorInfo: null,
      errorId: null 
    };
  }

  static getDerivedStateFromError(error) {
    console.log('ErrorBoundary: Error caught by getDerivedStateFromError');
    // Output: ErrorBoundary: Error caught by getDerivedStateFromError
    
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.error('ErrorBoundary: Full error details:');
    console.error('Error:', error);
    console.error('Error Info:', errorInfo);
    // Output: ErrorBoundary: Full error details:
    // Output: Error: Cannot read property 'name' of undefined
    // Output: Error Info: {componentStack: '    in BuggyComponent...'}
    
    const errorId = Date.now().toString();
    console.log('Generated error ID:', errorId);
    // Output: Generated error ID: 1642601234567
    
    this.setState({
      error: error,
      errorInfo: errorInfo,
      errorId: errorId
    });

    // Log to error reporting service
    this.logErrorToService(error, errorInfo, errorId);
  }

  logErrorToService = (error, errorInfo, errorId) => {
    console.log('Logging error to monitoring service...');
    // Output: Logging error to monitoring service...
    
    const errorData = {
      id: errorId,
      message: error.message,
      stack: error.stack,
      componentStack: errorInfo.componentStack,
      timestamp: new Date().toISOString(),
      url: window.location.href,
      userAgent: navigator.userAgent
    };
    
    console.log('Error data to be sent:', errorData);
    // Output: Error data to be sent: {id: '1642601234567', message: 'Cannot read...', ...}
    
    // In real app, send to service like Sentry, LogRocket, etc.
    // fetch('/api/errors', { method: 'POST', body: JSON.stringify(errorData) });
  };

  handleReset = () => {
    console.log('Resetting error boundary');
    // Output: Resetting error boundary
    
    this.setState({
      hasError: false,
      error: null,
      errorInfo: null,
      errorId: null
    });
  };

  render() {
    if (this.state.hasError) {
      console.log('ErrorBoundary: Rendering error UI');
      // Output: ErrorBoundary: Rendering error UI
      
      return (
        <div className="error-boundary">
          <div className="error-container">
            <h1>🚨 Something went wrong!</h1>
            <p>We're sorry, but something unexpected happened.</p>
            
            <details className="error-details">
              <summary>Error Details (Error ID: {this.state.errorId})</summary>
              <div className="error-info">
                <h3>Error Message:</h3>
                <p>{this.state.error?.message}</p>
                
                <h3>Stack Trace:</h3>
                <pre>{this.state.error?.stack}</pre>
                
                <h3>Component Stack:</h3>
                <pre>{this.state.errorInfo?.componentStack}</pre>
              </div>
            </details>
            
            <div className="error-actions">
              <button onClick={this.handleReset} className="retry-button">
                Try Again
              </button>
              <button onClick={() => window.location.reload()} className="reload-button">
                Reload Page
              </button>
            </div>
          </div>
        </div>
      );
    }

    return this.props.children;
  }
}

// Component that might throw errors
function BuggyCounter() {
  const [count, setCount] = useState(0);
  const [user, setUser] = useState(null);
  
  console.log('BuggyCounter rendered with count:', count);
  // Output: BuggyCounter rendered with count: 0
  // Output: BuggyCounter rendered with count: 5
  
  const handleClick = () => {
    console.log('Button clicked, incrementing count');
    // Output: Button clicked, incrementing count
    setCount(count + 1);
  };
  
  const handleBuggyAction = () => {
    console.log('Triggering intentional error...');
    // Output: Triggering intentional error...
    
    // This will throw an error and be caught by ErrorBoundary
    console.log(user.name); // user is null, so this throws
  };
  
  // Simulate random errors
  if (count === 5) {
    console.error('Simulated error: Count reached 5!');
    // Output: Simulated error: Count reached 5!
    throw new Error('I crashed when count reached 5!');
  }
  
  return (
    <div className="buggy-counter">
      <h2>Buggy Counter: {count}</h2>
      <p>Click 5 times to see error boundary in action</p>
      <button onClick={handleClick}>Increment</button>
      <button onClick={handleBuggyAction} className="danger-button">
        Trigger Error
      </button>
    </div>
  );
}

// Safe wrapper component
function SafeApp() {
  return (
    <div className="app">
      <h1>Error Boundary Demo</h1>
      
      <ErrorBoundary>
        <div className="safe-section">
          <h2>Safe Section</h2>
          <p>This section won't be affected by errors below.</p>
        </div>
      </ErrorBoundary>
      
      <ErrorBoundary>
        <div className="risky-section">
          <h2>Risky Section</h2>
          <BuggyCounter />
        </div>
      </ErrorBoundary>
      
      <ErrorBoundary>
        <div className="another-section">
          <h2>Another Safe Section</h2>
          <p>This section has its own error boundary.</p>
        </div>
      </ErrorBoundary>
    </div>
  );
}
```

## Debugging Tips and Console Techniques

### React DevTools Usage

```jsx
// Component with debugging helpers
function DebuggableComponent({ userId, theme }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  // Add display names for better DevTools experience
  DebuggableComponent.displayName = 'DebuggableComponent';
  
  console.group('🔍 DebuggableComponent Debug Info');
  console.log('Props received:', { userId, theme });
  console.log('Current state:', { user, loading });
  console.log('Render timestamp:', new Date().toLocaleTimeString());
  console.groupEnd();
  
  useEffect(() => {
    console.group('🔄 useEffect - User Data Fetch');
    console.log('Effect triggered for userId:', userId);
    
    const fetchUser = async () => {
      try {
        console.log('📡 Fetching user data...');
        setLoading(true);
        
        // Simulate API delay
        await new Promise(resolve => setTimeout(resolve, 1000));
        
        const userData = {
          id: userId,
          name: `User ${userId}`,
          email: `user${userId}@example.com`,
          preferences: { theme }
        };
        
        console.log('✅ User data received:', userData);
        setUser(userData);
      } catch (error) {
        console.error('❌ Failed to fetch user:', error);
      } finally {
        setLoading(false);
        console.log('🏁 Loading state set to false');
      }
    };
    
    fetchUser();
    
    return () => {
      console.log('🧹 Cleanup: User fetch effect');
    };
    
    console.groupEnd();
  }, [userId, theme]);
  
  // Performance measurement
  useEffect(() => {
    const renderStart = performance.now();
    
    return () => {
      const renderEnd = performance.now();
      console.log(`⏱️ Component render time: ${(renderEnd - renderStart).toFixed(2)}ms`);
    };
  });
  
  // Debug component updates
  useEffect(() => {
    console.table({
      'Component': 'DebuggableComponent',
      'User ID': userId,
      'Theme': theme,
      'Has User': !!user,
      'Is Loading': loading,
      'Timestamp': new Date().toISOString()
    });
  });
  
  return (
    <div className={`debuggable-component theme-${theme}`}>
      <div className="debug-header">
        <h2>Debuggable Component</h2>
        <div className="debug-info">
          <span>User ID: {userId}</span>
          <span>Theme: {theme}</span>
          <span>Loading: {loading ? 'Yes' : 'No'}</span>
        </div>
      </div>
      
      {loading ? (
        <div className="loading">Loading user...</div>
      ) : user ? (
        <UserProfile user={user} />
      ) : (
        <div className="error">Failed to load user</div>
      )}
    </div>
  );
}

// Enhanced UserProfile with debug info
function UserProfile({ user }) {
  console.log('👤 UserProfile rendered for:', user.name);
  
  const [expanded, setExpanded] = useState(false);
  
  return (
    <div className="user-profile">
      <h3>{user.name}</h3>
      <p>{user.email}</p>
      
      <button onClick={() => {
        console.log('🔧 Toggling expanded state:', !expanded);
        setExpanded(!expanded);
      }}>
        {expanded ? 'Hide' : 'Show'} Details
      </button>
      
      {expanded && (
        <div className="user-details">
          <h4>Debug Information:</h4>
          <pre>{JSON.stringify(user, null, 2)}</pre>
        </div>
      )}
    </div>
  );
}
```

### Performance Profiling

```jsx
// Performance monitoring hook
function usePerformanceMonitor(componentName) {
  const renderCount = useRef(0);
  const renderTimes = useRef([]);
  
  useEffect(() => {
    renderCount.current += 1;
    const renderTime = performance.now();
    renderTimes.current.push(renderTime);
    
    console.log(`🎯 ${componentName} - Render #${renderCount.current}`);
    
    if (renderCount.current % 10 === 0) {
      const avgRenderTime = renderTimes.current.slice(-10).reduce((a, b, i, arr) => 
        i === 0 ? 0 : a + (b - arr[i-1])
      ) / 9;
      
      console.log(`📊 ${componentName} - Average render time over last 10 renders: ${avgRenderTime.toFixed(2)}ms`);
    }
  });
  
  useEffect(() => {
    return () => {
      console.log(`📈 ${componentName} - Total renders: ${renderCount.current}`);
    };
  }, [componentName]);
}

// Component with performance monitoring
function PerformanceTestComponent({ data, filter }) {
  usePerformanceMonitor('PerformanceTestComponent');
  
  const startTime = performance.now();
  
  const filteredData = useMemo(() => {
    console.time('Data filtering');
    
    const result = data.filter(item => 
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
    
    console.timeEnd('Data filtering');
    console.log(`🔍 Filtered ${data.length} items down to ${result.length}`);
    
    return result;
  }, [data, filter]);
  
  const sortedData = useMemo(() => {
    console.time('Data sorting');
    
    const result = [...filteredData].sort((a, b) => a.name.localeCompare(b.name));
    
    console.timeEnd('Data sorting');
    console.log(`🔤 Sorted ${filteredData.length} items`);
    
    return result;
  }, [filteredData]);
  
  useEffect(() => {
    const endTime = performance.now();
    console.log(`⚡ Component processing time: ${(endTime - startTime).toFixed(2)}ms`);
  });
  
  return (
    <div className="performance-test">
      <h2>Performance Test Component</h2>
      <p>Showing {sortedData.length} of {data.length} items</p>
      
      <div className="items-list">
        {sortedData.map(item => (
          <div key={item.id} className="item">
            {item.name}
          </div>
        ))}
      </div>
    </div>
  );
}
```

### State Debugging

```jsx
// Custom hook for state debugging
function useDebugState(initialState, name) {
  const [state, setState] = useState(initialState);
  
  const setDebugState = useCallback((newState) => {
    console.group(`🔧 State Update: ${name}`);
    console.log('Previous state:', state);
    
    if (typeof newState === 'function') {
      const updatedState = newState(state);
      console.log('State updater function result:', updatedState);
      setState(updatedState);
    } else {
      console.log('New state:', newState);
      setState(newState);
    }
    
    console.log('Update timestamp:', new Date().toISOString());
    console.groupEnd();
  }, [state, name]);
  
  // Track state history
  const stateHistory = useRef([]);
  
  useEffect(() => {
    stateHistory.current.push({
      state,
      timestamp: Date.now()
    });
    
    // Keep only last 10 states
    if (stateHistory.current.length > 10) {
      stateHistory.current = stateHistory.current.slice(-10);
    }
    
    console.log(`📊 ${name} state history:`, stateHistory.current);
  }, [state, name]);
  
  return [state, setDebugState, stateHistory.current];
}

// Component using debug state
function DebuggableCounter() {
  const [count, setCount, countHistory] = useDebugState(0, 'Counter');
  const [step, setStep, stepHistory] = useDebugState(1, 'Step');
  
  const increment = () => {
    console.log('🔼 Incrementing counter by', step);
    setCount(prev => prev + step);
  };
  
  const decrement = () => {
    console.log('🔽 Decrementing counter by', step);
    setCount(prev => prev - step);
  };
  
  const reset = () => {
    console.log('🔄 Resetting counter to 0');
    setCount(0);
  };
  
  return (
    <div className="debuggable-counter">
      <h2>Debuggable Counter</h2>
      
      <div className="counter-display">
        <h3>Count: {count}</h3>
        <h4>Step: {step}</h4>
      </div>
      
      <div className="counter-controls">
        <button onClick={decrement}>- {step}</button>
        <button onClick={increment}>+ {step}</button>
        <button onClick={reset}>Reset</button>
      </div>
      
      <div className="step-controls">
        <label>
          Step size:
          <input
            type="number"
            value={step}
            onChange={(e) => {
              const newStep = parseInt(e.target.value) || 1;
              console.log('📐 Changing step size to:', newStep);
              setStep(newStep);
            }}
            min="1"
          />
        </label>
      </div>
      
      <div className="debug-panel">
        <details>
          <summary>Debug Information</summary>
          <div className="debug-info">
            <h4>Count History:</h4>
            <pre>{JSON.stringify(countHistory, null, 2)}</pre>
            
            <h4>Step History:</h4>
            <pre>{JSON.stringify(stepHistory, null, 2)}</pre>
          </div>
        </details>
      </div>
    </div>
  );
}
```

## Testing with Real Examples

### Component Testing

```jsx
// Button.test.js
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import '@testing-library/jest-dom';

import Button from './Button';

describe('Button Component', () => {
  beforeEach(() => {
    console.log('🧪 Setting up test...');
  });
  
  afterEach(() => {
    console.log('🧹 Cleaning up test...');
  });
  
  test('renders button with correct text', () => {
    console.log('✅ Test: renders button with correct text');
    
    render(<Button>Click me</Button>);
    
    const buttonElement = screen.getByText(/click me/i);
    expect(buttonElement).toBeInTheDocument();
    
    console.log('✅ Button found and rendered correctly');
  });
  
  test('calls onClick handler when clicked', async () => {
    console.log('✅ Test: calls onClick handler when clicked');
    
    const handleClick = jest.fn();
    const user = userEvent.setup();
    
    render(<Button onClick={handleClick}>Click me</Button>);
    
    const buttonElement = screen.getByText(/click me/i);
    await user.click(buttonElement);
    
    expect(handleClick).toHaveBeenCalledTimes(1);
    console.log('✅ onClick handler called once');
  });
  
  test('applies correct CSS classes for variants', () => {
    console.log('✅ Test: applies correct CSS classes for variants');
    
    const { rerender } = render(<Button variant="primary">Primary</Button>);
    
    let buttonElement = screen.getByText(/primary/i);
    expect(buttonElement).toHaveClass('btn-primary');
    console.log('✅ Primary variant class applied');
    
    rerender(<Button variant="secondary">Secondary</Button>);
    
    buttonElement = screen.getByText(/secondary/i);
    expect(buttonElement).toHaveClass('btn-secondary');
    console.log('✅ Secondary variant class applied');
  });
  
  test('is disabled when disabled prop is true', () => {
    console.log('✅ Test: is disabled when disabled prop is true');
    
    render(<Button disabled>Disabled Button</Button>);
    
    const buttonElement = screen.getByText(/disabled button/i);
    expect(buttonElement).toBeDisabled();
    console.log('✅ Button is properly disabled');
  });
  
  test('shows loading state correctly', async () => {
    console.log('✅ Test: shows loading state correctly');
    
    const AsyncButton = () => {
      const [loading, setLoading] = useState(false);
      
      const handleClick = async () => {
        setLoading(true);
        await new Promise(resolve => setTimeout(resolve, 100));
        setLoading(false);
      };
      
      return (
        <Button onClick={handleClick} loading={loading}>
          {loading ? 'Loading...' : 'Click me'}
        </Button>
      );
    };
    
    const user = userEvent.setup();
    render(<AsyncButton />);
    
    const buttonElement = screen.getByText(/click me/i);
    await user.click(buttonElement);
    
    expect(screen.getByText(/loading/i)).toBeInTheDocument();
    console.log('✅ Loading state displayed');
    
    await waitFor(() => {
      expect(screen.getByText(/click me/i)).toBeInTheDocument();
    });
    console.log('✅ Loading state cleared');
  });
});

// Hook testing example
// useCounter.test.js
import { renderHook, act } from '@testing-library/react';

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);
  
  console.log('useCounter hook called with initial value:', initialValue);
  console.log('Current count:', count);
  
  const increment = useCallback(() => {
    console.log('Incrementing count from', count);
    setCount(prev => {
      const newCount = prev + 1;
      console.log('Count incremented to', newCount);
      return newCount;
    });
  }, [count]);
  
  const decrement = useCallback(() => {
    console.log('Decrementing count from', count);
    setCount(prev => {
      const newCount = prev - 1;
      console.log('Count decremented to', newCount);
      return newCount;
    });
  }, [count]);
  
  const reset = useCallback(() => {
    console.log('Resetting count to', initialValue);
    setCount(initialValue);
  }, [initialValue]);
  
  return { count, increment, decrement, reset };
}

describe('useCounter Hook', () => {
  test('should initialize with default value', () => {
    console.log('🧪 Testing useCounter initialization');
    
    const { result } = renderHook(() => useCounter());
    
    expect(result.current.count).toBe(0);
    console.log('✅ Hook initialized with default value 0');
  });
  
  test('should initialize with custom value', () => {
    console.log('🧪 Testing useCounter with custom initial value');
    
    const { result } = renderHook(() => useCounter(10));
    
    expect(result.current.count).toBe(10);
    console.log('✅ Hook initialized with custom value 10');
  });
  
  test('should increment counter', () => {
    console.log('🧪 Testing counter increment');
    
    const { result } = renderHook(() => useCounter());
    
    act(() => {
      result.current.increment();
    });
    
    expect(result.current.count).toBe(1);
    console.log('✅ Counter incremented successfully');
  });
  
  test('should decrement counter', () => {
    console.log('🧪 Testing counter decrement');
    
    const { result } = renderHook(() => useCounter(5));
    
    act(() => {
      result.current.decrement();
    });
    
    expect(result.current.count).toBe(4);
    console.log('✅ Counter decremented successfully');
  });
  
  test('should reset counter to initial value', () => {
    console.log('🧪 Testing counter reset');
    
    const { result } = renderHook(() => useCounter(3));
    
    // Change the count first
    act(() => {
      result.current.increment();
      result.current.increment();
    });
    
    expect(result.current.count).toBe(5);
    console.log('✅ Counter modified to 5');
    
    // Reset
    act(() => {
      result.current.reset();
    });
    
    expect(result.current.count).toBe(3);
    console.log('✅ Counter reset to initial value');
  });
});

// Integration testing example
// App.integration.test.js
describe('TodoApp Integration Tests', () => {
  beforeEach(() => {
    // Mock localStorage
    const localStorageMock = {
      getItem: jest.fn(),
      setItem: jest.fn(),
      clear: jest.fn()
    };
    global.localStorage = localStorageMock;
    
    console.log('🔧 Integration test setup complete');
  });
  
  test('complete todo workflow', async () => {
    console.log('🧪 Testing complete todo workflow');
    
    const user = userEvent.setup();
    render(<TodoApp />);
    
    // Add a new todo
    console.log('📝 Adding new todo...');
    const input = screen.getByPlaceholderText(/add a todo/i);
    await user.type(input, 'Learn React Testing');
    await user.press('Enter');
    
    expect(screen.getByText('Learn React Testing')).toBeInTheDocument();
    console.log('✅ Todo added successfully');
    
    // Mark todo as complete
    console.log('✅ Marking todo as complete...');
    const checkbox = screen.getByRole('checkbox');
    await user.click(checkbox);
    
    expect(checkbox).toBeChecked();
    console.log('✅ Todo marked as complete');
    
    // Filter to show only completed todos
    console.log('🔍 Filtering completed todos...');
    const completedFilter = screen.getByText(/completed/i);
    await user.click(completedFilter);
    
    expect(screen.getByText('Learn React Testing')).toBeInTheDocument();
    console.log('✅ Completed filter working');
    
    // Delete todo
    console.log('🗑️ Deleting todo...');
    const deleteButton = screen.getByText(/delete/i);
    await user.click(deleteButton);
    
    expect(screen.queryByText('Learn React Testing')).not.toBeInTheDocument();
    console.log('✅ Todo deleted successfully');
  });
  
  test('handles API errors gracefully', async () => {
    console.log('🧪 Testing API error handling');
    
    // Mock failed API call
    jest.spyOn(global, 'fetch').mockRejectedValueOnce(
      new Error('API Error: Network failure')
    );
    
    render(<TodoApp />);
    
    await waitFor(() => {
      expect(screen.getByText(/error/i)).toBeInTheDocument();
    });
    
    console.log('✅ Error state displayed correctly');
    
    // Test retry functionality
    const retryButton = screen.getByText(/retry/i);
    
    // Mock successful retry
    global.fetch.mockResolvedValueOnce({
      ok: true,
      json: async () => ([
        { id: 1, text: 'Sample todo', completed: false }
      ])
    });
    
    const user = userEvent.setup();
    await user.click(retryButton);
    
    await waitFor(() => {
      expect(screen.getByText('Sample todo')).toBeInTheDocument();
    });
    
    console.log('✅ Retry functionality working');
    
    global.fetch.mockRestore();
  });
});
```

## Deployment and Build Optimization

### Environment-specific Builds

```jsx
// config/environment.js
const getEnvironmentConfig = () => {
  const env = process.env.NODE_ENV || 'development';
  
  console.log('🌍 Current environment:', env);
  // Output: 🌍 Current environment: production
  
  const baseConfig = {
    appName: 'My React App',
    version: process.env.REACT_APP_VERSION || '1.0.0'
  };
  
  const environmentConfigs = {
    development: {
      ...baseConfig,
      apiUrl: 'http://localhost:3001/api',
      enableDevTools: true,
      logLevel: 'debug',
      enableMocking: true
    },
    
    staging: {
      ...baseConfig,
      apiUrl: 'https://staging-api.myapp.com/api',
      enableDevTools: true,
      logLevel: 'info',
      enableMocking: false
    },
    
    production: {
      ...baseConfig,
      apiUrl: 'https://api.myapp.com/api',
      enableDevTools: false,
      logLevel: 'error',
      enableMocking: false
    }
  };
  
  const config = environmentConfigs[env] || environmentConfigs.development;
  
  console.log('⚙️ Environment configuration:', config);
  // Output: ⚙️ Environment configuration: {appName: 'My React App', apiUrl: 'https://api.myapp.com/api', ...}
  
  return config;
};

export default getEnvironmentConfig();
```

### Build Analysis and Optimization

```jsx
// Build analysis component
function BuildInfo() {
  const buildInfo = {
    version: process.env.REACT_APP_VERSION,
    buildTime: process.env.REACT_APP_BUILD_TIME,
    gitCommit: process.env.REACT_APP_GIT_COMMIT,
    environment: process.env.NODE_ENV
  };
  
  console.log('📦 Build information:', buildInfo);
  // Output: 📦 Build information: {version: '1.2.3', buildTime: '2024-01-15T10:30:00Z', ...}
  
  useEffect(() => {
    // Log build info on app start
    console.table(buildInfo);
    
    // Send build info to analytics
    if (process.env.NODE_ENV === 'production') {
      console.log('📊 Sending build info to analytics...');
      // analytics.track('app_started', buildInfo);
    }
  }, []);
  
  return process.env.NODE_ENV === 'development' ? (
    <div className="build-info">
      <h4>🔧 Development Build Info</h4>
      <pre>{JSON.stringify(buildInfo, null, 2)}</pre>
    </div>
  ) : null;
}

// Performance monitoring
function PerformanceMonitor() {
  useEffect(() => {
    // Monitor Core Web Vitals
    const observer = new PerformanceObserver((list) => {
      list.getEntries().forEach((entry) => {
        console.log(`📊 ${entry.name}:`, entry.value);
        // Output: 📊 first-contentful-paint: 1234.5
        // Output: 📊 largest-contentful-paint: 2345.6
        
        if (process.env.NODE_ENV === 'production') {
          // Send to analytics service
          console.log('📈 Sending performance metric to analytics');
          // analytics.track('performance_metric', {
          //   name: entry.name,
          //   value: entry.value,
          //   rating: entry.rating
          // });
        }
      });
    });
    
    observer.observe({ entryTypes: ['paint', 'largest-contentful-paint', 'first-input'] });
    
    // Monitor bundle size
    if ('connection' in navigator) {
      console.log('🌐 Network information:', {
        effectiveType: navigator.connection.effectiveType,
        downlink: navigator.connection.downlink,
        rtt: navigator.connection.rtt
      });
      // Output: 🌐 Network information: {effectiveType: '4g', downlink: 10, rtt: 100}
    }
    
    return () => observer.disconnect();
  }, []);
  
  return null;
}
```

### Progressive Web App (PWA) Setup

```jsx
// serviceWorkerRegistration.js
const isLocalhost = Boolean(
  window.location.hostname === 'localhost' ||
  window.location.hostname === '[::1]' ||
  window.location.hostname.match(
    /^127(?:\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}$/
  )
);

export function register(config) {
  if ('serviceWorker' in navigator) {
    console.log('🔧 Service Worker supported');
    
    const publicUrl = new URL(process.env.PUBLIC_URL, window.location.href);
    if (publicUrl.origin !== window.location.origin) {
      console.log('❌ Service Worker not registered: origin mismatch');
      return;
    }

    window.addEventListener('load', () => {
      const swUrl = `${process.env.PUBLIC_URL}/service-worker.js`;

      if (isLocalhost) {
        console.log('🏠 Running on localhost, checking service worker');
        checkValidServiceWorker(swUrl, config);
        
        navigator.serviceWorker.ready.then(() => {
          console.log('🚀 App is being served cache-first by service worker');
        });
      } else {
        console.log('🌍 Registering service worker for production');
        registerValidSW(swUrl, config);
      }
    });
  } else {
    console.log('❌ Service Worker not supported');
  }
}

function registerValidSW(swUrl, config) {
  navigator.serviceWorker
    .register(swUrl)
    .then((registration) => {
      console.log('✅ Service Worker registered:', registration.scope);
      
      registration.onupdatefound = () => {
        const installingWorker = registration.installing;
        if (installingWorker == null) {
          return;
        }
        
        installingWorker.onstatechange = () => {
          if (installingWorker.state === 'installed') {
            if (navigator.serviceWorker.controller) {
              console.log('🔄 New content available, reload required');
              
              if (config && config.onUpdate) {
                config.onUpdate(registration);
              }
            } else {
              console.log('✨ Content cached for offline use');
              
              if (config && config.onSuccess) {
                config.onSuccess(registration);
              }
            }
          }
        };
      };
    })
    .catch((error) => {
      console.error('❌ Service Worker registration failed:', error);
    });
}

// PWA Update component
function PWAUpdateNotification() {
  const [showUpdate, setShowUpdate] = useState(false);
  const [registration, setRegistration] = useState(null);
  
  useEffect(() => {
    const config = {
      onUpdate: (registration) => {
        console.log('🔄 New app version available');
        setRegistration(registration);
        setShowUpdate(true);
      },
      onSuccess: (registration) => {
        console.log('✅ App cached successfully');
      }
    };
    
    register(config);
  }, []);
  
  const handleUpdate = () => {
    if (registration && registration.waiting) {
      console.log('🔄 Updating to new version...');
      registration.waiting.postMessage({ type: 'SKIP_WAITING' });
      
      registration.waiting.addEventListener('statechange', (e) => {
        if (e.target.state === 'activated') {
          console.log('✅ App updated, reloading...');
          window.location.reload();
        }
      });
    }
  };
  
  if (!showUpdate) return null;
  
  return (
    <div className="pwa-update-notification">
      <div className="notification-content">
        <h3>🚀 New version available!</h3>
        <p>Update now to get the latest features and improvements.</p>
        <div className="notification-actions">
          <button onClick={handleUpdate} className="update-btn">
            Update Now
          </button>
          <button onClick={() => setShowUpdate(false)} className="dismiss-btn">
            Later
          </button>
        </div>
      </div>
    </div>
  );
}
```

## Best Practices Summary

### Code Organization Checklist

```jsx
// ✅ Good component structure
function WellStructuredComponent({ 
  data, 
  onAction, 
  variant = 'default',
  className = '',
  ...restProps 
}) {
  // 1. Hooks at the top
  const [localState, setLocalState] = useState(null);
  const [loading, setLoading] = useState(false);
  
  // 2. Derived state and memoized values
  const processedData = useMemo(() => {
    console.log('🔄 Processing data...');
    return data?.filter(item => item.active) || [];
  }, [data]);
  
  // 3. Event handlers
  const handleAction = useCallback((item) => {
    console.log('🎯 Action triggered for:', item.id);
    onAction?.(item);
  }, [onAction]);
  
  // 4. Effects
  useEffect(() => {
    console.log('📡 Component mounted or data changed');
    
    return () => {
      console.log('🧹 Component cleanup');
    };
  }, [data]);
  
  // 5. Early returns
  if (loading) {
    return <LoadingSpinner />;
  }
  
  if (!data || data.length === 0) {
    return <EmptyState message="No data available" />;
  }
  
  // 6. Main render
  return (
    <div 
      className={`component-container ${variant} ${className}`}
      {...restProps}
    >
      {processedData.map(item => (
        <ItemComponent
          key={item.id}
          item={item}
          onAction={handleAction}
        />
      ))}
    </div>
  );
}

// ✅ Custom hook best practices
function useApiData(endpoint, options = {}) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  console.log('🔗 useApiData hook called for:', endpoint);
  
  const fetchData = useCallback(async () => {
    try {
      setLoading(true);
      setError(null);
      
      console.log('📡 Fetching data from:', endpoint);
      
      const response = await fetch(endpoint, {
        headers: {
          'Content-Type': 'application/json',
          ...options.headers
        },
        ...options
      });
      
      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }
      
      const result = await response.json();
      console.log('✅ Data fetched successfully:', result);
      
      setData(result);
    } catch (err) {
      console.error('❌ Fetch error:', err);
      setError(err);
    } finally {
      setLoading(false);
    }
  }, [endpoint, options]);
  
  useEffect(() => {
    fetchData();
  }, [fetchData]);
  
  return { 
    data, 
    loading, 
    error, 
    refetch: fetchData 
  };
}

// ✅ Error handling best practices
function ErrorBoundaryWithRetry({ children, fallback }) {
  const [hasError, setHasError] = useState(false);
  const [error, setError] = useState(null);
  
  const handleError = (error, errorInfo) => {
    console.error('🚨 Error caught by boundary:', error);
    console.error('📍 Error info:', errorInfo);
    
    setHasError(true);
    setError(error);
    
    // Log to error tracking service
    // errorTracking.captureException(error, { extra: errorInfo });
  };
  
  const handleRetry = () => {
    console.log('🔄 Retrying after error...');
    setHasError(false);
    setError(null);
  };
  
  if (hasError) {
    return fallback ? (
      fallback(error, handleRetry)
    ) : (
      <div className="error-fallback">
        <h2>Something went wrong</h2>
        <p>{error?.message}</p>
        <button onClick={handleRetry}>Try Again</button>
      </div>
    );
  }
  
  return children;
}
```

## Quick Reference

### Console Debug Commands

```jsx
// Browser console debugging commands
console.log('='.repeat(50));
console.log('🔍 REACT DEBUG COMMANDS');
console.log('='.repeat(50));

// 1. Access React DevTools
console.log('$r - Currently selected React component in DevTools');
console.log('$r.props - Component props');
console.log('$r.state - Component state (class components)');

// 2. Performance profiling
console.log('performance.mark("start") - Mark performance start');
console.log('performance.mark("end") - Mark performance end');
console.log('performance.measure("operation", "start", "end") - Measure performance');

// 3. React-specific debugging
console.log('React.version - Current React version');
console.log('window.React - Access React globally (dev mode)');

// 4. Component tree inspection
console.log('document.querySelector("[data-reactroot]") - Find React root');

console.log('='.repeat(50));

// Development helpers
if (process.env.NODE_ENV === 'development') {
  // Global debug helpers
  window.debugReact = {
    logProps: (component) => console.table(component.props),
    logState: (component) => console.table(component.state),
    findComponents: (name) => {
      // Find components by display name
      const components = [];
      const walker = document.createTreeWalker(
        document.body,
        NodeFilter.SHOW_ELEMENT,
        null,
        false
      );
      
      let node;
      while (node = walker.nextNode()) {
        const reactFiber = node._reactInternalFiber;
        if (reactFiber && reactFiber.type && reactFiber.type.name === name) {
          components.push(node);
        }
      }
      
      console.log(`Found ${components.length} ${name} components:`, components);
      return components;
    }
  };
  
  console.log('🛠️ Debug helpers available at window.debugReact');
}
```

## Resources and Next Steps

### Essential Learning Path

```jsx
// Learning progression tracker
const LearningTracker = () => {
  const [completedTopics, setCompletedTopics] = useState(() => {
    const saved = localStorage.getItem('react-learning-progress');
    return saved ? JSON.parse(saved) : [];
  });
  
  const learningPath = [
    { id: 1, topic: 'JSX and Components', difficulty: 'Beginner', estimated: '2-3 days' },
    { id: 2, topic: 'Props and State', difficulty: 'Beginner', estimated: '3-4 days' },
    { id: 3, topic: 'Event Handling', difficulty: 'Beginner', estimated: '2 days' },
    { id: 4, topic: 'Lists and Keys', difficulty: 'Beginner', estimated: '2 days' },
    { id: 5, topic: 'Forms and Controlled Components', difficulty: 'Intermediate', estimated: '3-4 days' },
    { id: 6, topic: 'Hooks (useState, useEffect)', difficulty: 'Intermediate', estimated: '5-7 days' },
    { id: 7, topic: 'Custom Hooks', difficulty: 'Intermediate', estimated: '3-4 days' },
    { id: 8, topic: 'Context API', difficulty: 'Intermediate', estimated: '4-5 days' },
    { id: 9, topic: 'React Router', difficulty: 'Intermediate', estimated: '3-4 days' },
    { id: 10, topic: 'State Management (Redux)', difficulty: 'Advanced', estimated: '7-10 days' },
    { id: 11, topic: 'Testing with Jest & RTL', difficulty: 'Advanced', estimated: '7-10 days' },
    { id: 12, topic: 'Performance Optimization', difficulty: 'Advanced', estimated: '5-7 days' },
    { id: 13, topic: 'TypeScript with React', difficulty: 'Advanced', estimated: '10-14 days' }
  ];
  
  const toggleTopic = (topicId) => {
    const newCompleted = completedTopics.includes(topicId)
      ? completedTopics.filter(id => id !== topicId)
      : [...completedTopics, topicId];
    
    setCompletedTopics(newCompleted);
    localStorage.setItem('react-learning-progress', JSON.stringify(newCompleted));
    
    console.log(`📚 Topic ${topicId} ${newCompleted.includes(topicId) ? 'completed' : 'unchecked'}`);
  };
  
  const progress = (completedTopics.length / learningPath.length) * 100;
  
  console.log(`📊 Learning progress: ${progress.toFixed(1)}%`);
  
  return (
    <div className="learning-tracker">
      <h2>🎯 React Learning Path</h2>
      
      <div className="progress-bar">
        <div 
          className="progress-fill" 
          style={{ width: `${progress}%` }}
        />
        <span className="progress-text">{progress.toFixed(1)}% Complete</span>
      </div>
      
      <div className="learning-path">
        {learningPath.map(item => (
          <div 
            key={item.id} 
            className={`topic-item ${completedTopics.includes(item.id) ? 'completed' : ''}`}
          >
            <input
              type="checkbox"
              checked={completedTopics.includes(item.id)}
              onChange={() => toggleTopic(item.id)}
            />
            <div className="topic-info">
              <h3>{item.topic}</h3>
              <span className={`difficulty ${item.difficulty.toLowerCase()}`}>
                {item.difficulty}
              </span>
              <span className="estimated-time">{item.estimated}</span>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};
```

---

## 🏁 Conclusion

This comprehensive React.js guide provides you with:

- **Real working examples** with actual console outputs
- **Debugging techniques** with practical console commands
- **Performance insights** with monitoring examples
- **Production-ready patterns** with error handling
- **Testing strategies** with complete test suites
- **Deployment guidance** with optimization tips

### Quick Start Commands

```bash
# Create new React app
npx create-react-app my-app
cd my-app

# Install additional packages
npm install react-router-dom @testing-library/user-event

# Start development
npm start

# Run tests
npm test

# Build for production
npm run build

# Analyze bundle size
npx webpack-bundle-analyzer build/static/js/*.js
```

### Essential Browser Extensions
- React Developer Tools
- Redux DevTools
- React Hook Form DevTools

### Recommended VS Code Extensions
- ES7+ React/Redux/React-Native snippets
- Bracket Pair Colorizer
- Auto Rename Tag
- Prettier - Code formatter
- ESLint

**Happy coding! 🚀 Remember to check the browser console for all the helpful debug information shown in this guide!**

---

*If you find this guide helpful, please ⭐ star it and share with other developers!*ViewDetails}>
          View Details
        </button>
      </div>
    </div>
  );
}

// Parent Component
function ProductList() {
  const products = [
    { id: 1, name: 'Laptop', price: 999, inStock: true },
    { id: 2, name: 'Phone', price: 599, inStock: false },
    { id: 3, name: 'Tablet', price: 399, inStock: true }
  ];
  
  console.log('Products array:', products);
  // Output: Products array: [{id: 1, name: 'Laptop'...}, {id: 2, name: 'Phone'...}, ...]
  
  const handleAddToCart = (productId) => {
    console.log(`Parent: Product ${productId} added to cart`);
    // Output: Parent: Product 1 added to cart
    // Here you would update cart state
  };
  
  const handleViewDetails = (productId) => {
    console.log(`Parent: Viewing product ${productId} details`);
    // Output: Parent: Viewing product 1 details
    // Here you would navigate to product details page
  };
  
  return (
    <div className="product-list">
      <h2>Products ({products.length})</h2>
      {products.map(product => (
        <ProductCard
          key={product.id}
          product={product}
          onAddToCart={handleAddToCart}
          onViewDetails={handleViewDetails}
        />
      ))}
    </div>
  );
}
```

#### Props Validation and Default Values

```jsx
// Using default parameters
function Avatar({ src, alt, size = 'medium', shape = 'circle' }) {
  console.log(`Avatar props:`, { src, alt, size, shape });
  // Output: Avatar props: {src: 'user.jpg', alt: 'John Doe', size: 'large', shape: 'circle'}
  
  const sizeClasses = {
    small: 'w-8 h-8',
    medium: 'w-12 h-12',
    large: 'w-16 h-16'
  };
  
  const shapeClasses = {
    circle: 'rounded-full',
    square: 'rounded-none',
    rounded: 'rounded-md'
  };
  
  return (
    <img
      src={src}
      alt={alt}
      className={`avatar ${sizeClasses[size]} ${shapeClasses[shape]}`}
      onError={(e) => {
        console.log(`Failed to load image: ${src}`);
        e.target.src = '/placeholder-avatar.png';
      }}
    />
  );
}

// Usage examples
function UserList() {
  return (
    <div>
      <Avatar src="/user1.jpg" alt="John" size="large" />
      <Avatar src="/user2.jpg" alt="Jane" />
      <Avatar src="/user3.jpg" alt="Bob" size="small" shape="square" />
    </div>
  );
}
```

### State

State allows components to remember information and trigger re-renders when data changes.

```jsx
import React, { useState, useEffect } from 'react';

function ShoppingCart() {
  const [items, setItems] = useState([]);
  const [total, setTotal] = useState(0);
  const [isLoading, setIsLoading] = useState(false);
  
  console.log('ShoppingCart rendered. Current state:', { 
    itemCount: items.length, 
    total, 
    isLoading 
  });
  // Output: ShoppingCart rendered. Current state: {itemCount: 0, total: 0, isLoading: false}
  // Output: ShoppingCart rendered. Current state: {itemCount: 1, total: 29.99, isLoading: false}
  
  // Calculate total whenever items change
  useEffect(() => {
    const newTotal = items.reduce((sum, item) => sum + item.price * item.quantity, 0);
    console.log('Calculating total:', newTotal);
    // Output: Calculating total: 29.99
    // Output: Calculating total: 59.98
    setTotal(newTotal);
  }, [items]);
  
  const addItem = async (product) => {
    console.log('Adding item:', product);
    // Output: Adding item: {id: 1, name: 'T-Shirt', price: 29.99}
    
    setIsLoading(true);
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 500));
    
    setItems(currentItems => {
      const existingItem = currentItems.find(item => item.id === product.id);
      
      if (existingItem) {
        console.log('Item already exists, updating quantity');
        // Output: Item already exists, updating quantity
        return currentItems.map(item =>
          item.id === product.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      } else {
        console.log('New item added to cart');
        // Output: New item added to cart
        return [...currentItems, { ...product, quantity: 1 }];
      }
    });
    
    setIsLoading(false);
  };
  
  const removeItem = (itemId) => {
    console.log('Removing item with ID:', itemId);
    // Output: Removing item with ID: 1
    
    setItems(currentItems => {
      const updatedItems = currentItems.filter(item => item.id !== itemId);
      console.log('Items after removal:', updatedItems);
      // Output: Items after removal: []
      return updatedItems;
    });
  };
  
  const updateQuantity = (itemId, newQuantity) => {
    console.log(`Updating item ${itemId} quantity to ${newQuantity}`);
    // Output: Updating item 1 quantity to 3
    
    if (newQuantity <= 0) {
      removeItem(itemId);
      return;
    }
    
    setItems(currentItems =>
      currentItems.map(item =>
        item.id === itemId
          ? { ...item, quantity: newQuantity }
          : item
      )
    );
  };
  
  return (
    <div className="shopping-cart">
      <h2>Shopping Cart ({items.length} items)</h2>
      
      {isLoading && <p>Loading...</p>}
      
      {items.length === 0 ? (
        <p>Your cart is empty</p>
      ) : (
        <div>
          {items.map(item => (
            <div key={item.id} className="cart-item">
              <span>{item.name}</span>
              <span>${item.price}</span>
              <div className="quantity-controls">
                <button onClick={() => updateQuantity(item.id, item.quantity - 1)}>
                  -
                </button>
                <span>{item.quantity}</span>
                <button onClick={() => updateQuantity(item.id, item.quantity + 1)}>
                  +
                </button>
              </div>
              <button onClick={() => removeItem(item.id)}>Remove</button>
            </div>
          ))}
          <div className="cart-total">
            <strong>Total: ${total.toFixed(2)}</strong>
          </div>
        </div>
      )}
      
      <button onClick={() => addItem({ id: Date.now(), name: 'T-Shirt', price: 29.99 })}>
        Add Sample Item
      </button>
    </div>
  );
}
```

#### State Management Patterns

```jsx
// Complex state with useReducer
function TodoApp() {
  const initialState = {
    todos: [],
    filter: 'all', // 'all', 'active', 'completed'
    nextId: 1
  };
  
  function todoReducer(state, action) {
    console.log('Reducer called with action:', action);
    // Output: Reducer called with action: {type: 'ADD_TODO', payload: 'Learn React'}
    
    switch (action.type) {
      case 'ADD_TODO':
        const newTodo = {
          id: state.nextId,
          text: action.payload,
          completed: false,
          createdAt: new Date().toISOString()
        };
        console.log('Adding new todo:', newTodo);
        // Output: Adding new todo: {id: 1, text: 'Learn React', completed: false, createdAt: '2024-01-15T10:30:00.000Z'}
        
        return {
          ...state,
          todos: [...state.todos, newTodo],
          nextId: state.nextId + 1
        };
        
      case 'TOGGLE_TODO':
        console.log('Toggling todo with ID:', action.payload);
        // Output: Toggling todo with ID: 1
        
        return {
          ...state,
          todos: state.todos.map(todo =>
            todo.id === action.payload
              ? { ...todo, completed: !todo.completed }
              : todo
          )
        };
        
      case 'DELETE_TODO':
        console.log('Deleting todo with ID:', action.payload);
        // Output: Deleting todo with ID: 1
        
        return {
          ...state,
          todos: state.todos.filter(todo => todo.id !== action.payload)
        };
        
      case 'SET_FILTER':
        console.log('Setting filter to:', action.payload);
        // Output: Setting filter to: completed
        
        return {
          ...state,
          filter: action.payload
        };
        
      default:
        console.log('Unknown action type:', action.type);
        return state;
    }
  }
  
  const [state, dispatch] = useReducer(todoReducer, initialState);
  
  console.log('Current state:', state);
  // Output: Current state: {todos: [...], filter: 'all', nextId: 2}
  
  const filteredTodos = useMemo(() => {
    console.log('Filtering todos with filter:', state.filter);
    // Output: Filtering todos with filter: all
    
    switch (state.filter) {
      case 'active':
        return state.todos.filter(todo => !todo.completed);
      case 'completed':
        return state.todos.filter(todo => todo.completed);
      default:
        return state.todos;
    }
  }, [state.todos, state.filter]);
  
  return (
    <div className="todo-app">
      <h1>Todo App</h1>
      
      <form onSubmit={(e) => {
        e.preventDefault();
        const formData = new FormData(e.target);
        const text = formData.get('todo');
        if (text.trim()) {
          dispatch({ type: 'ADD_TODO', payload: text.trim() });
          e.target.reset();
        }
      }}>
        <input name="todo" placeholder="Add a todo..." required />
        <button type="submit">Add</button>
      </form>
      
      <div className="filters">
        {['all', 'active', 'completed'].map(filter => (
          <button
            key={filter}
            onClick={() => dispatch({ type: 'SET_FILTER', payload: filter })}
            className={state.filter === filter ? 'active' : ''}
          >
            {filter.charAt(0).toUpperCase() + filter.slice(1)}
          </button>
        ))}
      </div>
      
      <ul className="todo-list">
        {filteredTodos.map(todo => (
          <li key={todo.id} className={todo.completed ? 'completed' : ''}>
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => dispatch({ type: 'TOGGLE_TODO', payload: todo.id })}
            />
            <span>{todo.text}</span>
            <button onClick={() => dispatch({ type: 'DELETE_TODO', payload: todo.id })}>
              Delete
            </button>
          </li>
        ))}
      </ul>
      
      <div className="stats">
        <p>Total: {state.todos.length}</p>
        <p>Active: {state.todos.filter(todo => !todo.completed).length}</p>
        <p>Completed: {state.todos.filter(todo => todo.completed).length}</p>
      </div>
    </div>
  );
}
```

### Event Handling

React uses SyntheticEvents to ensure consistent behavior across browsers.

```jsx
function InteractiveForm() {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: '',
    confirmPassword: '',
    agreeToTerms: false
  });
  
  const [errors, setErrors] = useState({});
  const [touchedFields, setTouchedFields] = useState({});
  
  console.log('Form state:', formData);
  // Output: Form state: {username: '', email: '', password: '', confirmPassword: '', agreeToTerms: false}
  // Output: Form state: {username: 'john', email: '', password: '', confirmPassword: '', agreeToTerms: false}
  
  const handleInputChange = (event) => {
    const { name, value, type, checked } = event.target;
    console.log('Input changed:', { name, value, type, checked });
    // Output: Input changed: {name: 'username', value: 'john', type: 'text', checked: false}
    // Output: Input changed: {name: 'agreeToTerms', value: 'on', type: 'checkbox', checked: true}
    
    const newValue = type === 'checkbox' ? checked : value;
    
    setFormData(prev => ({
      ...prev,
      [name]: newValue
    }));
    
    // Clear error when user starts typing
    if (errors[name]) {
      console.log(`Clearing error for field: ${name}`);
      // Output: Clearing error for field: username
      setErrors(prev => ({ ...prev, [name]: '' }));
    }
  };
  
  const handleBlur = (event) => {
    const { name } = event.target;
    console.log(`Field ${name} lost focus`);
    // Output: Field username lost focus
    
    setTouchedFields(prev => ({ ...prev, [name]: true }));
    validateField(name, formData[name]);
  };
  
  const validateField = (name, value) => {
    console.log(`Validating field ${name} with value:`, value);
    // Output: Validating field email with value: invalid-email
    
    let error = '';
    
    switch (name) {
      case 'username':
        if (!value) error = 'Username is required';
        else if (value.length < 3) error = 'Username must be at least 3 characters';
        break;
        
      case 'email':
        if (!value) error = 'Email is required';
        else if (!/\S+@\S+\.\S+/.test(value)) error = 'Email is invalid';
        break;
        
      case 'password':
        if (!value) error = 'Password is required';
        else if (value.length < 6) error = 'Password must be at least 6 characters';
        break;
        
      case 'confirmPassword':
        if (!value) error = 'Please confirm your password';
        else if (value !== formData.password) error = 'Passwords do not match';
        break;
    }
    
    if (error) {
      console.log(`Validation error for ${name}:`, error);
      // Output: Validation error for email: Email is invalid
    }
    
    setErrors(prev => ({ ...prev, [name]: error }));
    return !error;
  };
  
  const handleSubmit = async (event) => {
    event.preventDefault();
    console.log('Form submission prevented, validating...');
    // Output: Form submission prevented, validating...
    
    // Mark all fields as touched
    const allFields = Object.keys(formData);
    setTouchedFields(Object.fromEntries(allFields.map(field => [field, true])));
    
    // Validate all fields
    const isValid = allFields.every(field => validateField(field, formData[field]));
    
    if (!formData.agreeToTerms) {
      setErrors(prev => ({ ...prev, agreeToTerms: 'You must agree to the terms' }));
    }
    
    const finalValid = isValid && formData.agreeToTerms;
    
    console.log('Form validation result:', finalValid);
    // Output: Form validation result: true
    
    if (finalValid) {
      console.log('Submitting form data:', formData);
      // Output: Submitting form data: {username: 'johndoe', email: 'john@example.com', ...}
      
      try {
        // Simulate API call
        const response = await fetch('/api/register', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(formData)
        });
        
        if (response.ok) {
          console.log('Registration successful!');
          // Output: Registration successful!
          alert('Registration successful!');
        } else {
          const errorData = await response.json();
          console.error('Registration failed:', errorData);
          // Output: Registration failed: {message: 'Email already exists'}
        }
      } catch (error) {
        console.error('Network error:', error);
        // Output: Network error: TypeError: Failed to fetch
      }
    } else {
      console.log('Form validation failed. Errors:', errors);
      // Output: Form validation failed. Errors: {email: 'Email is invalid', password: 'Password must be at least 6 characters'}
    }
  };
  
  const handleKeyPress = (event) => {
    console.log('Key pressed:', event.key, 'in field:', event.target.name);
    // Output: Key pressed: Enter in field: password
    
    if (event.key === 'Enter' && event.target.type !== 'submit') {
      console.log('Enter pressed, focusing next field');
      // Output: Enter pressed, focusing next field
      
      const form = event.target.form;
      const inputs = Array.from(form.querySelectorAll('input'));
      const currentIndex = inputs.indexOf(event.target);
      const nextInput = inputs[currentIndex + 1];
      
      if (nextInput) {
        nextInput.focus();
      }
    }
  };
  
  return (
    <form onSubmit={handleSubmit} className="interactive-form">
      <h2>Registration Form</h2>
      
      <div className="field">
        <label htmlFor="username">Username:</label>
        <input
          id="username"
          name="username"
          type="text"
          value={formData.username}
          onChange={handleInputChange}
          onBlur={handleBlur}
          onKeyPress={handleKeyPress}
          className={errors.username && touchedFields.username ? 'error' : ''}
          placeholder="Enter username"
        />
        {errors.username && touchedFields.username && (
          <span className="error-message">{errors.username}</span>
        )}
      </div>
      
      <div className="field">
        <label htmlFor="email">Email:</label>
        <input
          id="email"
          name="email"
          type="email"
          value={formData.email}
          onChange={handleInputChange}
          onBlur={handleBlur}
          onKeyPress={handleKeyPress}
          className={errors.email && touchedFields.email ? 'error' : ''}
          placeholder="Enter email"
        />
        {errors.email && touchedFields.email && (
          <span className="error-message">{errors.email}</span>
        )}
      </div>
      
      <div className="field">
        <label htmlFor="password">Password:</label>
        <input
          id="password"
          name="password"
          type="password"
          value={formData.password}
          onChange={handleInputChange}
          onBlur={handleBlur}
          onKeyPress={handleKeyPress}
          className={errors.password && touchedFields.password ? 'error' : ''}
          placeholder="Enter password"
        />
        {errors.password && touchedFields.password && (
          <span className="error-message">{errors.password}</span>
        )}
      </div>
      
      <div className="field">
        <label htmlFor="confirmPassword">Confirm Password:</label>
        <input
          id="confirmPassword"
          name="confirmPassword"
          type="password"
          value={formData.confirmPassword}
          onChange={handleInputChange}
          onBlur={handleBlur}
          onKeyPress={handleKeyPress}
          className={errors.confirmPassword && touchedFields.confirmPassword ? 'error' : ''}
          placeholder="Confirm password"
        />
