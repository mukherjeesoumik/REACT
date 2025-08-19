Complete React.js Course - Beginner Friendly 🚀
Table of Contents
What is React?
Setting Up Development Environment
JSX - JavaScript XML
Components
Props
State
Event Handling
Conditional Rendering
Lists and Keys
Forms
Hooks
Component Lifecycle
Context API
Routing
Best Practices
What is React?
React is a JavaScript library for building user interfaces, especially web applications. Think of it like building blocks for websites - you create small pieces (components) and combine them to build complex applications.
Why React?
Problem: Traditional web development meant writing lots of repetitive code and manually updating the DOM (webpage elements) whenever data changed. This was slow and error-prone.
Solution: React solves this by:
Creating reusable UI components (like Lego blocks)
Automatically updating the webpage when data changes
Making code easier to organize and maintain
Key Features:
Component-Based: Build encapsulated components that manage their own state
Virtual DOM: React creates a virtual copy of your webpage in memory, compares changes, and updates only what's necessary - making it super fast!
Reusable: Write a component once, use it everywhere
Declarative: Just describe what you want the UI to look like, React handles the "how"
Real-World Analogy:
Think of React like a restaurant kitchen:
Components = Different stations (salad station, grill, dessert station)
Props = Ingredients passed between stations
State = Current status of each dish being prepared
Virtual DOM = The head chef who coordinates everything efficiently
Setting Up Development Environment
Option 1: Create React App (Recommended for beginners)
npx create-react-app my-first-app
cd my-first-app
npm start
Option 2: Online Playground
CodeSandbox
CodePen
Repl.it
Project Structure:
my-first-app/
  public/
    index.html
  src/
    App.js
    index.js
    App.css
  package.json
JSX - JavaScript XML
JSX lets you write HTML-like code in JavaScript. It's like mixing HTML and JavaScript together!
Why JSX?
Problem: Creating HTML elements in JavaScript was messy and hard to read:
const element = React.createElement('div', null, 
  React.createElement('h1', null, 'Hello'),
  React.createElement('p', null, 'Welcome to React')
);
Solution: JSX makes it look like HTML:
const element = (
  <div>
    <h1>Hello</h1>
    <p>Welcome to React</p>
  </div>
);
Think of JSX as:
A translator that converts HTML-like syntax into JavaScript
A way to write UI that looks familiar to web developers
The bridge between design (HTML/CSS) and logic (JavaScript)
Basic JSX Example:
// Instead of creating elements like this:
const element = React.createElement('h1', null, 'Hello, World!');
// We can write JSX like this:
const element = <h1>Hello, World!</h1>;
JSX Rules:
Single Parent Element: Wrap multiple elements in one parent
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
JavaScript Expressions: Use curly braces {}
const name = "John";
const age = 25;
const element = (
  <div>
    <h1>Hello, {name}!</h1>
    <p>You are {age} years old</p>
    <p>Next year you'll be {age + 1}</p>
  </div>
);
HTML Attributes in camelCase
// ❌ HTML way
<div class="container" onclick="handleClick()">
// ✅ JSX way
<div className="container" onClick={handleClick}>
Components
Components are like custom HTML elements. Think of them as reusable pieces of UI.
Why Components?
Problem: Copying and pasting the same HTML code everywhere. If you need to change something, you have to update it in multiple places.
Solution: Create a component once, use it anywhere. Change it once, updates everywhere!
Real-World Analogy:
Think of components like:
LEGO blocks - small pieces that you combine to build something bigger
Cookie cutters - one shape, many cookies
Car parts - headlights, wheels, doors that can be used in different car models
Types of Components:
1. Presentational Components - Just show data (like a business card)2. Container Components - Handle logic and pass data to other components (like a form controller)3. Reusable Components - Can be used anywhere (like buttons, inputs)
Functional Components (Modern Way)
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
Real-World Example: User Card
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
Props
Props (properties) are how you pass data from parent to child components. Think of them like function parameters.
Why Props?
Problem: Components need different data to display. A UserCard component should show different users, not the same person every time!
Solution: Props let you pass data into components, making them flexible and reusable.
Real-World Analogies:
Mail delivery - Props are like the address and contents of a package
Restaurant order - Props are like telling the chef what dish to make and how to customize it
Function parameters - Just like function greet(name), components receive props
Key Points:
Props flow downward (parent → child)
Props are read-only (child cannot change them)
Props make components reusable
Basic Props Example:
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
Props with Destructuring:
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
Props with Objects and Arrays:
function ProductCard({ product }) {
  return (
    <div className="product-card">
      <h3>{product.name}</h3>
      <p>${product.price}</p>
      <p>{product.description}</p>
    </div>
  );
}
function App() {
  const product = {
    name: "Laptop",
    price: 999,
    description: "High-performance laptop"
  };
  return <ProductCard product={product} />;
}
State
State is data that can change over time. When state changes, React re-renders the component.
Why State?
Problem: Web applications need to respond to user interactions. Clicking buttons, typing in forms, loading data - the webpage needs to update!
Solution: State lets components "remember" information and update the UI when that information changes.
Real-World Analogies:
Traffic light - Changes color based on its current state (red → yellow → green)
Bank account - Balance changes when you deposit or withdraw money
TV remote - Changes channels, volume, settings
State vs Props:
State	Props
Internal data	External data
Can be changed	Read-only
Component owns it	Parent passes it
Like variables in a function	Like function parameters
When to Use State:
User input (form fields, checkboxes)
Current selection (active tab, selected item)
Loading status (is data being fetched?)
Toggle states (show/hide, on/off)
useState Hook:
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
Multiple State Variables:
function UserProfile() {
  const [name, setName] = useState("John");
  const [age, setAge] = useState(25);
  const [email, setEmail] = useState("john@example.com");
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Email: {email}</p>
      
      <button onClick={() => setAge(age + 1)}>
        Birthday! 🎂
      </button>
    </div>
  );
}
State with Objects:
function UserForm() {
  const [user, setUser] = useState({
    name: "",
    email: "",
    age: 0
  });
  const updateName = (newName) => {
    setUser({ ...user, name: newName }); // Spread operator to keep other properties
  };
  return (
    <div>
      <input 
        type="text"
        placeholder="Name"
        value={user.name}
        onChange={(e) => updateName(e.target.value)}
      />
      <p>Current name: {user.name}</p>
    </div>
  );
}
Event Handling
React handles events using synthetic events, which work the same across all browsers.
Why Event Handling?
Problem: Websites need to respond to user actions - clicks, typing, scrolling, hovering. Without events, websites would be static and boring!
Solution: Event handlers let you define what happens when users interact with your components.
Real-World Analogy:
Think of events like:
Doorbell - When someone presses it (event), the bell rings (handler function)
Light switch - When you flip it (event), lights turn on/off (handler function)
Car horn - When you press it (event), it makes a sound (handler function)
Common Events:
onClick - Mouse clicks
onChange - Input field changes
onSubmit - Form submissions
onMouseOver/onMouseOut - Hover effects
onKeyPress - Keyboard input
Event Object:
Every event handler receives an "event object" with useful information:
event.target - The element that triggered the event
event.preventDefault() - Stops default browser behavior
event.value - Current value of input fields
Click Events:
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
Form Events:
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
Mouse Events:
function MouseExample() {
  const [position, setPosition] = useState({ x: 0, y: 0 });
  const handleMouseMove = (event) => {
    setPosition({
      x: event.clientX,
      y: event.clientY
    });
  };
  return (
    <div 
      onMouseMove={handleMouseMove}
      style={{ height: "200px", border: "1px solid black" }}
    >
      <p>Mouse position: ({position.x}, {position.y})</p>
    </div>
  );
}
Conditional Rendering
Show different content based on conditions, like if-else statements for your UI.
Why Conditional Rendering?
Problem: Your UI needs to change based on different situations. Show a loading spinner while data loads, display login button for guests, show user profile for logged-in users.
Solution: Conditional rendering lets you show different components or content based on your application's current state.
Real-World Analogies:
ATM machine - Shows different screens based on your account status
Weather app - Shows sun icon on sunny days, rain icon on rainy days
Restaurant menu - Shows "Available" or "Sold Out" based on inventory
Traffic sign - Shows "STOP" or "GO" based on conditions
Common Use Cases:
Authentication - Show different content for logged-in vs guest users
Loading states - Show spinner while data is being fetched
Error handling - Show error message when something goes wrong
Feature toggles - Show features based on user permissions
Empty states - Show "No items found" when list is empty
If-Else with &&:
function WelcomeMessage({ isLoggedIn, username }) {
  return (
    <div>
      {isLoggedIn && <h1>Welcome back, {username}!</h1>}
      {!isLoggedIn && <h1>Please log in</h1>}
    </div>
  );
}
// Usage
function App() {
  return (
    <div>
      <WelcomeMessage isLoggedIn={true} username="Alice" />
      <WelcomeMessage isLoggedIn={false} />
    </div>
  );
}
Ternary Operator:
function LoginButton({ isLoggedIn, onLogin, onLogout }) {
  return (
    <button onClick={isLoggedIn ? onLogout : onLogin}>
      {isLoggedIn ? "Logout" : "Login"}
    </button>
  );
}
Multiple Conditions:
function UserStatus({ user }) {
  const renderStatus = () => {
    if (!user) {
      return <p>No user found</p>;
    }
    
    if (user.isActive) {
      return <p style={{color: 'green'}}>User is active</p>;
    }
    
    if (user.isPending) {
      return <p style={{color: 'orange'}}>User is pending</p>;
    }
    
    return <p style={{color: 'red'}}>User is inactive</p>;
  };
  return (
    <div>
      <h3>{user?.name}</h3>
      {renderStatus()}
    </div>
  );
}
Lists and Keys
Render arrays of data as lists. Keys help React identify which items have changed.
Why Lists and Keys?
Problem: You often need to display multiple similar items - user lists, product catalogs, todo items, social media posts. Manually writing HTML for each item is impractical.
Solution: Use JavaScript's map() function to transform arrays of data into arrays of components.
Why Keys are Important:
Problem: When you add, remove, or reorder list items, React needs to know which items changed to update efficiently.
Solution: Keys act like unique ID cards for each list item, helping React track changes.
Real-World Analogies:
Student roster - Each student has a unique ID number (key) and information (data)
Library catalog - Each book has ISBN (key) and book details (data)
Playlist - Each song has unique identifier (key) and song info (data)
Shopping cart - Each item has product ID (key) and item details (data)
Key Rules:
Keys must be unique among siblings
Keys should be stable (same item = same key)
Don't use array index as key if list can change order
Use meaningful identifiers (like database IDs)
Basic List:
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
List with Objects:
function UserList() {
  const users = [
    { id: 1, name: "Alice", age: 25 },
    { id: 2, name: "Bob", age: 30 },
    { id: 3, name: "Charlie", age: 28 }
  ];
  return (
    <div>
      {users.map(user => (
        <div key={user.id} style={{ border: '1px solid #ccc', margin: '10px', padding: '10px' }}>
          <h3>{user.name}</h3>
          <p>Age: {user.age}</p>
        </div>
      ))}
    </div>
  );
}
Interactive List (Todo App):
function TodoApp() {
  const [todos, setTodos] = useState([
    { id: 1, text: "Learn React", completed: false },
    { id: 2, text: "Build a project", completed: false }
  ]);
  const toggleTodo = (id) => {
    setTodos(todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ));
  };
  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };
  return (
    <div>
      <h2>Todo List</h2>
      {todos.map(todo => (
        <div key={todo.id} style={{ display: 'flex', alignItems: 'center', margin: '10px' }}>
          <input
            type="checkbox"
            checked={todo.completed}
            onChange={() => toggleTodo(todo.id)}
          />
          <span style={{ 
            textDecoration: todo.completed ? 'line-through' : 'none',
            marginLeft: '10px',
            marginRight: '10px'
          }}>
            {todo.text}
          </span>
          <button onClick={() => deleteTodo(todo.id)}>Delete</button>
        </div>
      ))}
    </div>
  );
}
Forms
Handle user input with controlled components.
Why Controlled Components?
Problem: HTML form elements (input, select, textarea) naturally manage their own state. This makes it hard to validate, manipulate, or sync with your React component's state.
Solution: Controlled components let React control the form element's value through state, giving you full control over user input.
Controlled vs Uncontrolled:
Controlled Component (React controls the value):
const [name, setName] = useState("");
<input value={name} onChange={(e) => setName(e.target.value)} />
Uncontrolled Component (HTML element controls the value):
<input /> // React doesn't know or control the value
Real-World Analogy:
Controlled = Remote-controlled toy car (you control every movement)
Uncontrolled = Wind-up toy car (you start it, but it goes on its own)
Benefits of Controlled Components:
Validation - Check input as user types
Formatting - Format phone numbers, credit cards automatically
Synchronization - Keep multiple inputs in sync
Conditional logic - Enable/disable fields based on other inputs
Controlled Components:
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
    // Here you would typically send data to a server
  };
  return (
    <form onSubmit={handleSubmit} style={{ maxWidth: '400px', margin: '20px' }}>
      <div style={{ marginBottom: '15px' }}>
        <label>
          Name:
          <input
            type="text"
            name="name"
            value={formData.name}
            onChange={handleInputChange}
            required
            style={{ width: '100%', padding: '8px', marginTop: '5px' }}
          />
        </label>
      </div>
      <div style={{ marginBottom: '15px' }}>
        <label>
          Email:
          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={handleInputChange}
            required
            style={{ width: '100%', padding: '8px', marginTop: '5px' }}
          />
        </label>
      </div>
      <div style={{ marginBottom: '15px' }}>
        <label>
          Message:
          <textarea
            name="message"
            value={formData.message}
            onChange={handleInputChange}
            rows="4"
            style={{ width: '100%', padding: '8px', marginTop: '5px' }}
          />
        </label>
      </div>
      <div style={{ marginBottom: '15px' }}>
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
      <button type="submit" style={{ padding: '10px 20px', backgroundColor: '#007bff', color: 'white', border: 'none', borderRadius: '4px' }}>
        Submit
      </button>
    </form>
  );
}
Form Validation:
function LoginForm() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [errors, setErrors] = useState({});
  const validateForm = () => {
    const newErrors = {};
    
    if (!email) {
      newErrors.email = "Email is required";
    } else if (!/\S+@\S+\.\S+/.test(email)) {
      newErrors.email = "Email is invalid";
    }
    
    if (!password) {
      newErrors.password = "Password is required";
    } else if (password.length < 6) {
      newErrors.password = "Password must be at least 6 characters";
    }
    
    return newErrors;
  };
  const handleSubmit = (event) => {
    event.preventDefault();
    const newErrors = validateForm();
    
    if (Object.keys(newErrors).length === 0) {
      console.log("Login successful:", { email, password });
      // Proceed with login
    } else {
      setErrors(newErrors);
    }
  };
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input
          type="email"
          placeholder="Email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
        {errors.email && <p style={{color: 'red'}}>{errors.email}</p>}
      </div>
      <div>
        <input
          type="password"
          placeholder="Password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
        />
        {errors.password && <p style={{color: 'red'}}>{errors.password}</p>}
      </div>
      <button type="submit">Login</button>
    </form>
  );
}
Hooks
Hooks let you use state and other React features in functional components.
What are Hooks?
Hooks are special functions that "hook into" React features. They always start with the word "use" (useState, useEffect, useContext, etc.).
Why Hooks?
Before Hooks (Old Way): You needed class components to use state and lifecycle methods. This meant:
More complex code
Harder to reuse stateful logic
Confusing this keyword
Lifecycle methods scattered logic
After Hooks (New Way): You can use all React features in functional components:
Simpler, cleaner code
Easy to reuse logic between components
No this confusion
Logic grouped by concern, not lifecycle
Real-World Analogy:
Think of hooks like power outlets in your house:
useState = Light switch (turn state on/off, change brightness)
useEffect = Motion sensor (react to changes, cleanup when leaving)
useContext = Central heating system (shared throughout the house)
useReducer = Complex control panel (manage multiple related settings)
Hook Rules (Very Important!):
Only call hooks at the top level - Not inside loops, conditions, or nested functions
Only call hooks from React functions - Functional components or custom hooks
Why These Rules?
React relies on the order of hook calls to track state. Breaking the rules confuses React about which state belongs to which hook.
useState Hook (Already covered above)
const [state, setState] = useState(initialValue);
useEffect Hook:
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
// Effect that runs when specific values change
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    setLoading(true);
    // Simulate API call
    setTimeout(() => {
      setUser({ id: userId, name: `User ${userId}` });
      setLoading(false);
    }, 1000);
  }, [userId]); // Effect runs when userId changes
  if (loading) return <p>Loading...</p>;
  
  return (
    <div>
      <h2>{user.name}</h2>
      <p>ID: {user.id}</p>
    </div>
  );
}
Custom Hooks:
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
useContext Hook:
import React, { createContext, useContext, useState } from 'react';
// Create context
const ThemeContext = createContext();
// Provider component
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  const toggleTheme = () => {
    setTheme(prev => prev === 'light' ? 'dark' : 'light');
  };
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
// Component that uses context
function ThemedButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return (
    <button
      onClick={toggleTheme}
      style={{
        backgroundColor: theme === 'light' ? 'white' : 'black',
        color: theme === 'light' ? 'black' : 'white',
        padding: '10px 20px',
        border: '1px solid gray'
      }}
    >
      Toggle Theme (Current: {theme})
    </button>
  );
}
// App component
function App() {
  return (
    <ThemeProvider>
      <div style={{ padding: '20px' }}>
        <h1>Theme Example</h1>
        <ThemedButton />
      </div>
    </ThemeProvider>
  );
}
Component Lifecycle
Understanding when components mount, update, and unmount.
What is Component Lifecycle?
Components go through different phases during their existence, like the life stages of a person or the seasons of a year.
The Three Phases:
1. Mounting = Birth 👶
Component is created and added to the DOM
Like a person being born or a plant being planted
2. Updating = Growing/Living 🌱
Component receives new props or state changes
Like a person growing up or a plant getting water/sunlight
3. Unmounting = Death 💀
Component is removed from the DOM
Like a person passing away or a plant being removed
Real-World Analogies:
House Construction:
Mounting = Foundation is laid, house is built
Updating = Renovations, repainting, new furniture
Unmounting = House is demolished
TV Show:
Mounting = Show starts, actors appear on stage
Updating = Scene changes, actors move, dialogue happens
Unmounting = Show ends, actors leave stage
Why Care About Lifecycle?
Setup - Initialize data, start timers, subscribe to events
Cleanup - Clear timers, unsubscribe, prevent memory leaks
Optimization - Only update when necessary
Lifecycle with useEffect:
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
  // Component did update (runs when name changes)
  useEffect(() => {
    console.log("Name changed to:", name);
  }, [name]);
  // Runs after every render
  useEffect(() => {
    console.log("Component rendered");
  });
  return (
    <div>
      <h2>Hello, {name}</h2>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
Context API
Share data between components without passing props down manually.
What is the Context API?
Context provides a way to share data between components without having to pass props through every level of the component tree.
Why Context API?
Problem - "Prop Drilling": Imagine you have data at the top level that's needed by a component deep down. You have to pass it through every component in between, even if those middle components don't need the data.
App (has user data)
├── Header (doesn't need user data, but has to pass it)
│   └── Navigation (doesn't need user data, but has to pass it) 
│       └── UserMenu (NEEDS user data!)
└── Main
    └── Content (doesn't need user data, but has to pass it)
        └── UserProfile (NEEDS user data!)
Solution: Context is like a "global variable" that any component can access directly.
Real-World Analogies:
WiFi Network:
Without Context = Passing internet through cables to each device
With Context = WiFi broadcasts everywhere, devices connect directly
Hotel Room Service:
Without Context = Message passes through reception → manager → staff → your room
With Context = Direct phone line to room service
Company Announcements:
Without Context = CEO tells VP, VP tells managers, managers tell employees
With Context = Company-wide email/Slack channel
When to Use Context:
User authentication - Current user info needed everywhere
Theme/settings - Dark mode, language preferences
Shopping cart - Cart state needed in multiple components
Global application state - Data that many components need
Complete Context Example:
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
Routing
Navigate between different pages/views in your app using React Router.
What is Routing?
Routing allows you to create a multi-page application experience in a single-page application (SPA). Users can navigate to different URLs and see different content.
Why Routing?
Problem: Traditional websites reload the entire page when you click a link. This is slow and loses application state.
Solution: React Router changes the URL and shows different components without page refresh, creating a smooth, app-like experience.
Real-World Analogies:
TV Remote:
Different channels (routes) = Different content
Channel number (URL) = Current page
Remote control (Link/navigate) = Navigation
Office Building:
Different floors/rooms (routes) = Different pages
Room numbers (URLs) = Page addresses
Elevator/stairs (navigation) = Moving between pages
Directory (navigation menu) = List of available pages
Restaurant Menu:
Different sections (routes) = Appetizers, Main Course, Desserts
Page numbers (URLs) = /appetizers, /main-course, /desserts
Waiter (router) = Shows you the right section
Types of Routes:
Static routes - Fixed URLs like /about, /contact
Dynamic routes - Variable URLs like /user/:id, /product/:slug
Nested routes - Routes within routes like /dashboard/profile
Protected routes - Require authentication to access
Installation:
npm install react-router-dom
Basic Routing Setup:
import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link, useParams } from 'react-router-dom';
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
          </Routes>
        </div>
      </div>
    </Router>
  );
}
Best Practices
1. Component Structure:
// Good: Small, focused components
function Button({ onClick, children, variant = 'primary' }) {
  const className = `btn btn-${variant}`;
  return (
    <button className={className} onClick={onClick}>
      {children}
    </button>
  );
}
// Good: Separate concerns
function UserCard({ user, onEdit, onDelete }) {
  return (
    <div className="user-card">
      <UserAvatar src={user.avatar} />
      <UserInfo name={user.name} email={user.email} />
      <UserActions onEdit={onEdit} onDelete={onDelete} />
    </div>
  );
}
2. State Management:
// Good: Keep state as simple as possible
function TodoList() {
  const [todos, setTodos] = useState([]);
  const [filter, setFilter] = useState('all');
  // Good: Use functional updates
  const addTodo = (text) => {
    setTodos(prev => [...prev, { id: Date.now(), text, completed: false }]);
  };
  // Good: Compute derived state
  const filteredTodos = todos.filter(todo => {
    if (filter === 'completed') return todo.completed;
    if (filter === 'active') return !todo.completed;
    return true;
  });
  return (
    <div>
      {/* Component JSX */}
    </div>
  );
}
3. Performance Tips:
import React, { memo, useMemo, useCallback } from 'react';
// Memoize expensive calculations
function ExpensiveComponent({ data }) {
  const expensiveValue = useMemo(() => {
    return data.reduce((sum, item) => sum + item.value, 0);
  }, [data]);
  return <div>Total: {expensiveValue}</div>;
}
// Memoize callback functions
function TodoList({ todos }) {
  const [filter, setFilter] = useState('all');
  const handleToggle = useCallback((id) => {
    setTodos(prev => prev.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ));
  }, []);
  return (
    <div>
      {todos.map(todo => (
        <TodoItem key={todo.id} todo={todo} onToggle={handleToggle} />
      ))}
    </div>
  );
}
// Memoize components to prevent unnecessary re-renders
const TodoItem = memo(function TodoItem({ todo, onToggle }) {
  return (
    <div onClick={() => onToggle(todo.id)}>
      {todo.text}
    </div>
  );
});
4. Error Handling:
import React, { Component } from 'react';
// Error Boundary (Class Component)
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null
Claude
Talk with Claude, an AI assistant from Anthropic
 
