Here’s the translation of your provided section into English, maintaining the structure and formatting:

---

# Complete Course to Learn React

## Table of Contents

1. [Introduction to React](#1-introduction-to-react)
2. [Environment Setup](#2-environment-setup)
3. [Components and JSX](#3-components-and-jsx)
4. [Props and State](#4-props-and-state)
5. [Event Handling](#5-event-handling)
6. [Conditional Rendering](#6-conditional-rendering)
7. [Lists and Keys](#7-lists-and-keys)
8. [Forms](#8-forms)
9. [Hooks](#9-hooks)
10. [Context API](#10-context-api)
11. [Routing with React Router](#11-routing-with-react-router)
12. [API Calls and Data Management](#12-api-calls-and-data-management)
13. [Optimization and Best Practices](#13-optimization-and-best-practices)
14. [Final Project](#14-final-project)

---

## 1. Introduction to React

### What is React?

React is a JavaScript library developed by Facebook for building interactive user interfaces (UI). Unlike a full-fledged framework, React focuses solely on the view layer of your application.

### Why Use React?

- **Declarative Approach**: You describe what your UI should look like, and React efficiently updates it for you.
- **Component-Based**: You build interfaces by assembling reusable components.
- **Learn Once, Write Anywhere**: React can be used for the web (React), mobile (React Native), and even virtual reality (React VR).
- **Large Community**: A rich ecosystem and strong community support.

### Core Concepts

- **Components**: Reusable building blocks for your interface.
- **JSX**: A syntactic extension of JavaScript that resembles HTML.
- **Virtual DOM**: An in-memory representation of the real DOM to optimize updates.
- **Unidirectional Data Flow**: Data flows from parent components to child components.

---

## 2. Environment Setup

### Method 1: Create React App (Recommended for Beginners)

```bash
npx create-react-app my-react-app
cd my-react-app
npm start
```

### Method 2: Vite (Faster and Lighter)

```shellscript
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

### Basic Structure of a React Project

```plaintext
my-react-app/
  ├── node_modules/
  ├── public/
  │   ├── index.html
  │   └── favicon.ico
  ├── src/
  │   ├── App.js
  │   ├── index.js
  │   ├── components/
  │   └── assets/
  ├── package.json
  └── README.md
```

---

## 3. Components and JSX

### What is JSX?

JSX is a syntactic extension of JavaScript that resembles HTML but has the power of JavaScript. It is transformed into standard JavaScript by Babel.

```jsx
// This is JSX
const element = <h1>Hello, world!</h1>;

// It is transformed into this by Babel
// const element = React.createElement('h1', null, 'Hello, world!');
```

### Types of Components

#### Functional Components

```jsx
import React from "react";

// Functional component (recommended)
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Greeting;
```

#### Class Components (Less Used in Modern React)

```jsx
import React, { Component } from "react";

// Class component
class Greeting extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default Greeting;
```

### Component Composition

```jsx
import React from "react";
import Greeting from "./Greeting";
import Profile from "./Profile";

function App() {
  return (
    <div>
      <Greeting name="Marie" />
      <Profile user="marie123" />
    </div>
  );
}

export default App;
```

---

## 4. Props and State

### Props

Props are data passed from a parent component to a child component. They are read-only.

```jsx
import React from "react";

// Parent component
function App() {
  return <Card title="My Title" content="My Content" />;
}

// Child component
function Card(props) {
  return (
    <div className="card">
      <h2>{props.title}</h2>
      <p>{props.content}</p>
    </div>
  );
}

export default App;
```

### State

State is managed within a component and can change over time.

```jsx
import React, { useState } from "react";

function Counter() {
  // Declare a state variable with useState
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click here</button>
    </div>
  );
}

export default Counter;
```

### Difference Between Props and State

| Props                             | State                                     |
| --------------------------------- | ----------------------------------------- |
| Passed to the component           | Defined within the component              |
| Immutable                         | Can be modified                           |
| Read-only access                  | Can be updated with setState or setX      |
| Can be passed to child components | Generally not passed directly to children |

---

## 5. Event Handling

### Event Syntax in React

```jsx
import React, { useState } from "react";

function Button() {
  const [isActive, setIsActive] = useState(false);

  // Event handler
  function handleClick() {
    setIsActive(!isActive);
  }

  return (
    <button onClick={handleClick} className={isActive ? "active" : "inactive"}>
      {isActive ? "Active" : "Inactive"}
    </button>
  );
}

export default Button;
```

### Common Events

- `onClick`: Triggered on click
- `onChange`: Triggered when a value changes (forms)
- `onSubmit`: Triggered on form submission
- `onMouseOver`: Triggered when the mouse hovers over
- `onKeyDown`: Triggered when a key is pressed

### Passing Parameters to Event Handlers

```jsx
import React from "react";

function ButtonList() {
  // With parameter
  function handleClick(id) {
    console.log("Button clicked:", id);
  }

  return (
    <div>
      {/* Using an arrow function to pass parameters */}
      <button onClick={() => handleClick(1)}>Button 1</button>
      <button onClick={() => handleClick(2)}>Button 2</button>
      <button onClick={() => handleClick(3)}>Button 3</button>
    </div>
  );
}

export default ButtonList;
```

---

## 6. Conditional Rendering

### Using Logical Operators

```jsx
import React, { useState } from "react";

function WelcomeMessage() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <div>
      {/* Using the && operator */}
      {isLoggedIn && <h1>Welcome, user!</h1>}

      {/* Button to toggle state */}
      <button onClick={() => setIsLoggedIn(!isLoggedIn)}>{isLoggedIn ? "Log out" : "Log in"}</button>
    </div>
  );
}

export default WelcomeMessage;
```

### Using the Ternary Operator

```jsx
import React, { useState } from "react";

function Notification() {
  const [messages, setMessages] = useState(5);

  return (
    <div>
      {/* Using the ternary operator */}
      {messages > 0 ? <p>You have {messages} new messages</p> : <p>You have no new messages</p>}

      {/* Button to reduce message count */}
      <button onClick={() => setMessages(messages > 0 ? messages - 1 : 0)}>Read a message</button>
    </div>
  );
}

export default Notification;
```

### Using Variables to Store JSX Elements

```jsx
import React, { useState } from "react";

function UserPage() {
  const [role, setRole] = useState("user"); // 'user' or 'admin'

  let content;

  if (role === "admin") {
    content = (
      <div>
        <h1>Admin Panel</h1>
        <p>Welcome to the admin panel</p>
      </div>
    );
  } else {
    content = (
      <div>
        <h1>User Profile</h1>
        <p>Welcome to your profile</p>
      </div>
    );
  }

  return (
    <div>
      {content}
      <button onClick={() => setRole(role === "user" ? "admin" : "user")}>Switch role</button>
    </div>
  );
}

export default UserPage;
```

---

## 7. Lists and Keys

### Rendering Lists with map()

```jsx
import React from "react";

function FruitList() {
  const fruits = ["Apple", "Banana", "Orange", "Mango", "Pineapple"];

  return (
    <div>
      <h1>List of Fruits</h1>
      <ul>
        {fruits.map((fruit, index) => (
          <li key={index}>{fruit}</li>
        ))}
      </ul>
    </div>
  );
}

export default FruitList;
```

### Importance of Keys

Keys help React identify which items have changed, been added, or removed. They must be unique among siblings.

```jsx
import React from "react";

function UserList() {
  const users = [
    { id: 1, name: "Alice", email: "alice@example.com" },
    { id: 2, name: "Bob", email: "bob@example.com" },
    { id: 3, name: "Charlie", email: "charlie@example.com" },
  ];

  return (
    <div>
      <h1>List of Users</h1>
      <ul>
        {users.map((user) => (
          // Using the ID as the key (best practice)
          <li key={user.id}>
            <strong>{user.name}</strong>: {user.email}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default UserList;
```

---

## 8. Forms

### Controlled Components

```jsx
import React, { useState } from "react";

function ContactForm() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
    console.log("Form submitted:", { name, email, message });
    // Here, you could send the data to a server

    // Reset the form
    setName("");
    setEmail("");
    setMessage("");
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="name">Name:</label>
        <input type="text" id="name" value={name} onChange={(e) => setName(e.target.value)} required />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input type="email" id="email" value={email} onChange={(e) => setEmail(e.target.value)} required />
      </div>

      <div>
        <label htmlFor="message">Message:</label>
        <textarea id="message" value={message} onChange={(e) => setMessage(e.target.value)} required />
      </div>

      <button type="submit">Submit</button>
    </form>
  );
}

export default ContactForm;
```

### Managing Multiple Fields with a Single State

```jsx
import React, { useState } from "react";

function RegistrationForm() {
  const [formData, setFormData] = useState({
    firstName: "",
    lastName: "",
    email: "",
    password: "",
    age: "",
  });

  function handleChange(event) {
    const { name, value } = event.target;
    setFormData({
      ...formData, // Keep existing values
      [name]: value, // Update only the changed field
    });
  }

  function handleSubmit(event) {
    event.preventDefault();
    console.log("Form data:", formData);
    // Process the data...
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="firstName">First Name:</label>
        <input type="text" id="firstName" name="firstName" value={formData.firstName} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="lastName">Last Name:</label>
        <input type="text" id="lastName" name="lastName" value={formData.lastName} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input type="email" id="email" name="email" value={formData.email} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="password">Password:</label>
        <input type="password" id="password" name="password" value={formData.password} onChange={handleChange} />
      </div>

      <div>
        <label htmlFor="age">Age:</label>
        <input type="number" id="age" name="age" value={formData.age} onChange={handleChange} />
      </div>

      <button type="submit">Register</button>
    </form>
  );
}

export default RegistrationForm;
```

---

## 9. Hooks

### useState

Allows adding local state to a functional component.

```jsx
import React, { useState } from "react";

function Counter() {
  // Declare a state variable "count" initialized to 0
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click</button>
    </div>
  );
}

export default Counter;
```

### useEffect

Allows performing side effects in functional components (similar to lifecycle methods in class components).

```jsx
import React, { useState, useEffect } from "react";

function UseEffectExample() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("");

  // Runs after every render
  useEffect(() => {
    document.title = `You clicked ${count} times`;

    // Cleanup function (optional)
    return () => {
      document.title = "React App";
    };
  }, [count]); // Dependency: runs only if count changes

  return (
    <div>
      <input value={name} onChange={(e) => setName(e.target.value)} placeholder="Enter your name" />
      <p>Hello, {name || "Guest"}</p>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click</button>
    </div>
  );
}

export default UseEffectExample;
```

### useRef

Allows creating a mutable reference that persists across the component’s lifetime.

```jsx
import React, { useRef, useState } from "react";

function UseRefExample() {
  const inputRef = useRef(null);
  const [message, setMessage] = useState("");

  function focusInput() {
    // Direct DOM access
    inputRef.current.focus();
  }

  function getInputValue() {
    setMessage(`Current value: ${inputRef.current.value}`);
  }

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Type something" />
      <button onClick={focusInput}>Focus the input</button>
      <button onClick={getInputValue}>Get value</button>
      <p>{message}</p>
    </div>
  );
}

export default UseRefExample;
```

### Other Important Hooks

- `useContext`: Access a React context
- `useReducer`: Alternative to useState for complex state logic
- `useMemo`: Memoize a computed value
- `useCallback`: Memoize a function
- `useLayoutEffect`: Synchronous version of useEffect
- `useId`: Generate unique IDs for accessibility

---

## 10. Context API

### Creating and Using a Context

```jsx
import React, { createContext, useContext, useState } from "react";

// Create the context
const ThemeContext = createContext();

// Provider component
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme(theme === "light" ? "dark" : "light");
  };

  // Value provided by the context
  const value = {
    theme,
    toggleTheme,
  };

  return <ThemeContext.Provider value={value}>{children}</ThemeContext.Provider>;
}

// Custom hook to use the context
function useTheme() {
  const context = useContext(ThemeContext);
  if (context === undefined) {
    throw new Error("useTheme must be used within a ThemeProvider");
  }
  return context;
}

// Component that uses the context
function ThemedButton() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button
      onClick={toggleTheme}
      style={{
        backgroundColor: theme === "light" ? "#fff" : "#333",
        color: theme === "light" ? "#333" : "#fff",
        padding: "10px 15px",
        border: "1px solid #ccc",
        borderRadius: "4px",
      }}
    >
      Toggle Theme ({theme})
    </button>
  );
}

// App component
function App() {
  return (
    <ThemeProvider>
      <div style={{ padding: "20px" }}>
        <h1>Context API Example</h1>
        <ThemedButton />
      </div>
    </ThemeProvider>
  );
}

export default App;
```

---

## 11. Routing with React Router

### Installation

```shellscript
npm install react-router-dom
```

### Basic Configuration

```jsx
import React from "react";
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

// Page components
function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Us</h2>;
}

function Contact() {
  return <h2>Contact Us</h2>;
}

function NotFound() {
  return <h2>404 - Page Not Found</h2>;
}

// App component with routing
function App() {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/contact">Contact</Link>
            </li>
          </ul>
        </nav>

        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

### URL Parameters and Programmatic Navigation

```jsx
import React from "react";
import { BrowserRouter, Routes, Route, Link, useParams, useNavigate } from "react-router-dom";

// Simulated product list
const products = [
  { id: 1, name: "Laptop", price: 999 },
  { id: 2, name: "Smartphone", price: 699 },
  { id: 3, name: "Tablet", price: 499 },
];

// Home page with product list
function ProductList() {
  return (
    <div>
      <h2>Our Products</h2>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            <Link to={`/product/${product.id}`}>{product.name}</Link>
          </li>
        ))}
      </ul>
    </div>
  );
}

// Product detail page
function ProductDetail() {
  const { id } = useParams();
  const navigate = useNavigate();

  // Find product by ID
  const product = products.find((p) => p.id === parseInt(id));

  if (!product) {
    return <div>Product not found</div>;
  }

  return (
    <div>
      <h2>{product.name}</h2>
      <p>Price: ${product.price}</p>
      <button onClick={() => navigate("/")}>Back to list</button>
    </div>
  );
}

// App component
function App() {
  return (
    <BrowserRouter>
      <div>
        <header>
          <h1>My Online Store</h1>
          <nav>
            <Link to="/">Home</Link>
          </nav>
        </header>

        <main>
          <Routes>
            <Route path="/" element={<ProductList />} />
            <Route path="/product/:id" element={<ProductDetail />} />
          </Routes>
        </main>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

---

## 12. API Calls and Data Management

### Using fetch with useEffect

```jsx
import React, { useState, useEffect } from "react";

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Function to fetch data
    async function fetchUsers() {
      try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");

        if (!response.ok) {
          throw new Error(`HTTP Error: ${response.status}`);
        }

        const data = await response.json();
        setUsers(data);
        setLoading(false);
      } catch (error) {
        setError(error.message);
        setLoading(false);
      }
    }

    fetchUsers();
  }, []); // Empty dependency array = runs once on mount

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return (
    <div>
      <h2>User List</h2>
      <ul>
        {users.map((user) => (
          <li key={user.id}>
            <strong>{user.name}</strong> ({user.email})
          </li>
        ))}
      </ul>
    </div>
  );
}

export default UserList;
```

### Creating a Custom Hook for API Calls

```jsx
import { useState, useEffect } from "react";

// Custom hook for API calls
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Flag to cancel request if component unmounts
    let isMounted = true;

    async function fetchData() {
      try {
        const response = await fetch(url);

        if (!response.ok) {
          throw new Error(`HTTP Error: ${response.status}`);
        }

        const result = await response.json();

        if (isMounted) {
          setData(result);
          setLoading(false);
        }
      } catch (error) {
        if (isMounted) {
          setError(error.message);
          setLoading(false);
        }
      }
    }

    fetchData();

    // Cleanup function
    return () => {
      isMounted = false;
    };
  }, [url]); // Request re-runs if URL changes

  return { data, loading, error };
}

// Example usage of the hook
import React from "react";

function PostList() {
  const { data: posts, loading, error } = useFetch("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return (
    <div>
      <h2>Post List</h2>
      <ul>
        {posts &&
          posts.map((post) => (
            <li key={post.id}>
              <h3>{post.title}</h3>
              <p>{post.body}</p>
            </li>
          ))}
      </ul>
    </div>
  );
}

export default PostList;
```

---

## 13. Optimization and Best Practices

### Memoization with React.memo, useMemo, and useCallback

```jsx
import React, { useState, useMemo, useCallback, memo } from "react";

// Memoized child component
const ExpensiveComponent = memo(function ExpensiveComponent({ onClick, value }) {
  console.log("Rendering ExpensiveComponent");

  return (
    <div>
      <p>Computed value: {value}</p>
      <button onClick={onClick}>Click me</button>
    </div>
  );
});

function App() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  // Expensive computation memoized with useMemo
  const expensiveValue = useMemo(() => {
    console.log("Expensive computation executed");
    let result = 0;
    for (let i = 0; i < 1000000; i++) {
      result += count;
    }
    return result;
  }, [count]); // Recalculates only if count changes

  // Memoized function with useCallback
  const handleClick = useCallback(() => {
    console.log("Button clicked");
    setCount(count + 1);
  }, [count]); // Recrates function only if count changes

  return (
    <div>
      <h1>Optimization Example</h1>

      <input type="text" value={text} onChange={(e) => setText(e.target.value)} placeholder="Type something..." />

      <p>Text: {text}</p>
      <p>Counter: {count}</p>

      {/* Component won't re-render if props haven't changed */}
      <ExpensiveComponent value={expensiveValue} onClick={handleClick} />
    </div>
  );
}

export default App;
```

### Code Splitting and Lazy Loading

```jsx
import React, { Suspense, lazy, useState } from "react";

// Dynamic import with lazy
const HeavyComponent = lazy(() => import("./HeavyComponent"));
const AnotherHeavyComponent = lazy(() => import("./AnotherHeavyComponent"));

function App() {
  const [showHeavy, setShowHeavy] = useState(false);
  const [showAnother, setShowAnother] = useState(false);

  return (
    <div>
      <h1>Code Splitting Example</h1>

      <button onClick={() => setShowHeavy(!showHeavy)}>{showHeavy ? "Hide" : "Show"} Heavy Component</button>

      <button onClick={() => setShowAnother(!showAnother)}>{showAnother ? "Hide" : "Show"} Another Heavy Component</button>

      {/* Suspense displays a fallback during loading */}
      <Suspense fallback={<div>Loading...</div>}>
        {showHeavy && <HeavyComponent />}
        {showAnother && <AnotherHeavyComponent />}
      </Suspense>
    </div>
  );
}

export default App;
```

### Best Practices

1. **Organized Project Structure**

   - Group files by feature or type
   - Use `index.js` files to simplify imports

2. **Consistent Naming**

   - PascalCase for components
   - camelCase for variables and functions
   - UPPER_SNAKE_CASE for constants

3. **Avoid Prop Drilling**

   - Use Context API or a state management solution

4. **Optimize Performance**

   - Use `React.memo` for pure components
   - Use `useMemo` and `useCallback` to avoid unnecessary recalculations
   - Implement code splitting to reduce bundle size

5. **Error Handling**

   - Use Error Boundaries to catch errors
   - Implement loading and error states

---

## 14. Final Project

### Todo List Application

#### App.jsx

```jsx
import React from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { TaskProvider } from "./contexts/TaskContext";
import Header from "./components/Header";
import TaskList from "./components/TaskList";
import TaskForm from "./components/TaskForm";
import TaskDetails from "./components/TaskDetails";
import NotFound from "./components/NotFound";
import "./App.css";

function App() {
  return (
    <TaskProvider>
      <BrowserRouter>
        <div className="app">
          <Header />
          <main className="container">
            <Routes>
              <Route
                path="/"
                element={
                  <>
                    <TaskForm />
                    <TaskList />
                  </>
                }
              />
              <Route path="/task/:id" element={<TaskDetails />} />
              <Route path="*" element={<NotFound />} />
            </Routes>
          </main>
          <footer className="footer">
            <p>React Todo List Application - {new Date().getFullYear()}</p>
          </footer>
        </div>
      </BrowserRouter>
    </TaskProvider>
  );
}

export default App;
```

#### contexts/TaskContext.jsx

```jsx
import React, { createContext, useContext, useReducer, useEffect } from "react";

// Create the context
const TaskContext = createContext();

// Actions
const ADD_TASK = "ADD_TASK";
const DELETE_TASK = "DELETE_TASK";
const TOGGLE_TASK = "TOGGLE_TASK";
const UPDATE_TASK = "UPDATE_TASK";

// Initial state
const initialState = {
  tasks: JSON.parse(localStorage.getItem("tasks")) || [],
};

// Reducer
function taskReducer(state, action) {
  switch (action.type) {
    case ADD_TASK:
      return {
        tasks: [...state.tasks, action.payload],
      };
    case DELETE_TASK:
      return {
        tasks: state.tasks.filter((task) => task.id !== action.payload),
      };
    case TOGGLE_TASK:
      return {
        tasks: state.tasks.map((task) => (task.id === action.payload ? { ...task, completed: !task.completed } : task)),
      };
    case UPDATE_TASK:
      return {
        tasks: state.tasks.map((task) => (task.id === action.payload.id ? { ...task, ...action.payload.updates } : task)),
      };
    default:
      return state;
  }
}

// Provider
export function TaskProvider({ children }) {
  const [state, dispatch] = useReducer(taskReducer, initialState);

  // Save to localStorage on state change
  useEffect(() => {
    localStorage.setItem("tasks", JSON.stringify(state.tasks));
  }, [state.tasks]);

  // Actions
  const addTask = (title, description = "") => {
    dispatch({
      type: ADD_TASK,
      payload: {
        id: Date.now().toString(),
        title,
        description,
        completed: false,
        createdAt: new Date().toISOString(),
      },
    });
  };

  const deleteTask = (id) => {
    dispatch({
      type: DELETE_TASK,
      payload: id,
    });
  };

  const toggleTask = (id) => {
    dispatch({
      type: TOGGLE_TASK,
      payload: id,
    });
  };

  const updateTask = (id, updates) => {
    dispatch({
      type: UPDATE_TASK,
      payload: { id, updates },
    });
  };

  return (
    <TaskContext.Provider
      value={{
        tasks: state.tasks,
        addTask,
        deleteTask,
        toggleTask,
        updateTask,
      }}
    >
      {children}
    </TaskContext.Provider>
  );
}

// Custom hook to use the context
export function useTasks() {
  const context = useContext(TaskContext);
  if (context === undefined) {
    throw new Error("useTasks must be used within a TaskProvider");
  }
  return context;
}
```

#### components/Header.jsx

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";

function Header() {
  const { tasks } = useTasks();
  const completedTasks = tasks.filter((task) => task.completed).length;

  return (
    <header className="header">
      <div className="container header-content">
        <h1>
          <Link to="/">Todo List</Link>
        </h1>
        <div className="task-stats">
          <span>
            {completedTasks}/{tasks.length} tasks completed
          </span>
        </div>
      </div>
    </header>
  );
}

export default Header;
```

#### components/TaskForm.jsx

```jsx
import React, { useState } from "react";
import { useTasks } from "../contexts/TaskContext";

function TaskForm() {
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");
  const { addTask } = useTasks();

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    addTask(title, description);
    setTitle("");
    setDescription("");
  };

  return (
    <div className="task-form-container">
      <h2>Add a Task</h2>
      <form onSubmit={handleSubmit} className="task-form">
        <div className="form-group">
          <label htmlFor="title">Title</label>
          <input type="text" id="title" value={title} onChange={(e) => setTitle(e.target.value)} placeholder="What do you need to do?" required />
        </div>

        <div className="form-group">
          <label htmlFor="description">Description (optional)</label>
          <textarea id="description" value={description} onChange={(e) => setDescription(e.target.value)} placeholder="Task details" rows="3" />
        </div>

        <button type="submit" className="btn btn-primary">
          Add
        </button>
      </form>
    </div>
  );
}

export default TaskForm;
```

#### components/TaskList.jsx

```jsx
import React, { useState } from "react";
import { Link } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";
import TaskItem from "./TaskItem";

function TaskList() {
  const { tasks } = useTasks();
  const [filter, setFilter] = useState("all"); // 'all', 'active', 'completed'

  // Filter tasks based on the active filter
  const filteredTasks = tasks.filter((task) => {
    if (filter === "active") return !task.completed;
    if (filter === "completed") return task.completed;
    return true; // 'all'
  });

  // Sort tasks by creation date (newest first)
  const sortedTasks = [...filteredTasks].sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));

  return (
    <div className="task-list-container">
      <div className="task-list-header">
        <h2>My Tasks ({filteredTasks.length})</h2>
        <div className="task-filters">
          <button className={`filter-btn ${filter === "all" ? "active" : ""}`} onClick={() => setFilter("all")}>
            All
          </button>
          <button className={`filter-btn ${filter === "active" ? "active" : ""}`} onClick={() => setFilter("active")}>
            To Do
          </button>
          <button className={`filter-btn ${filter === "completed" ? "active" : ""}`} onClick={() => setFilter("completed")}>
            Completed
          </button>
        </div>
      </div>

      {sortedTasks.length === 0 ? (
        <p className="no-tasks">No tasks to display.</p>
      ) : (
        <ul className="task-list">
          {sortedTasks.map((task) => (
            <TaskItem key={task.id} task={task} />
          ))}
        </ul>
      )}
    </div>
  );
}

export default TaskList;
```

#### components/TaskItem.jsx

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";

function TaskItem({ task }) {
  const { toggleTask, deleteTask } = useTasks();

  // Format date
  const formatDate = (dateString) => {
    const options = {
      year: "numeric",
      month: "long",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
    };
    return new Date(dateString).toLocaleDateString("en-US", options);
  };

  return (
    <li className={`task-item ${task.completed ? "completed" : ""}`}>
      <div className="task-item-content">
        <label className="checkbox-container">
          <input type="checkbox" checked={task.completed} onChange={() => toggleTask(task.id)} />
          <span className="checkmark"></span>
        </label>

        <div className="task-details">
          <h3 className="task-title">{task.title}</h3>
          {task.description && <p className="task-description">{task.description}</p>}
          <span className="task-date">Created on {formatDate(task.createdAt)}</span>
        </div>
      </div>

      <div className="task-actions">
        <Link to={`/task/${task.id}`} className="btn btn-info">
          Details
        </Link>
        <button onClick={() => deleteTask(task.id)} className="btn btn-danger">
          Delete
        </button>
      </div>
    </li>
  );
}

export default TaskItem;
```

#### components/TaskDetails.jsx

```jsx
import React, { useState, useEffect } from "react";
import { useParams, useNavigate } from "react-router-dom";
import { useTasks } from "../contexts/TaskContext";

function TaskDetails() {
  const { id } = useParams();
  const navigate = useNavigate();
  const { tasks, updateTask, deleteTask } = useTasks();

  const [task, setTask] = useState(null);
  const [isEditing, setIsEditing] = useState(false);
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");

  // Find the corresponding task
  useEffect(() => {
    const foundTask = tasks.find((t) => t.id === id);
    if (foundTask) {
      setTask(foundTask);
      setTitle(foundTask.title);
      setDescription(foundTask.description || "");
    }
  }, [id, tasks]);

  // If the task doesn’t exist, redirect to home
  if (!task) {
    return (
      <div className="task-details not-found">
        <h2>Task not found</h2>
        <button onClick={() => navigate("/")} className="btn btn-primary">
          Back to list
        </button>
      </div>
    );
  }

  // Handle form submission for editing
  const handleSubmit = (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    updateTask(task.id, { title, description });
    setIsEditing(false);
  };

  // Handle deletion and redirect
  const handleDelete = () => {
    deleteTask(task.id);
    navigate("/");
  };

  // Format date
  const formatDate = (dateString) => {
    const options = {
      year: "numeric",
      month: "long",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
    };
    return new Date(dateString).toLocaleDateString("en-US", options);
  };

  return (
    <div className="task-details">
      <button onClick={() => navigate("/")} className="btn btn-back">
        ← Back
      </button>

      {isEditing ? (
        <div className="edit-form">
          <h2>Edit Task</h2>
          <form onSubmit={handleSubmit}>
            <div className="form-group">
              <label htmlFor="edit-title">Title</label>
              <input type="text" id="edit-title" value={title} onChange={(e) => setTitle(e.target.value)} required />
            </div>

            <div className="form-group">
              <label htmlFor="edit-description">Description</label>
              <textarea id="edit-description" value={description} onChange={(e) => setDescription(e.target.value)} rows="5" />
            </div>

            <div className="form-actions">
              <button type="submit" className="btn btn-primary">
                Save
              </button>
              <button type="button" onClick={() => setIsEditing(false)} className="btn btn-secondary">
                Cancel
              </button>
            </div>
          </form>
        </div>
      ) : (
        <div className="task-info">
          <div className="task-header">
            <h2>{task.title}</h2>
            <span className={`task-status ${task.completed ? "completed" : "active"}`}>{task.completed ? "Completed" : "To Do"}</span>
          </div>

          <div className="task-body">
            <p className="task-description">{task.description || "No description provided."}</p>
            <p className="task-date">Created on {formatDate(task.createdAt)}</p>
          </div>

          <div className="task-actions">
            <button onClick={() => setIsEditing(true)} className="btn btn-primary">
              Edit
            </button>
            <button onClick={handleDelete} className="btn btn-danger">
              Delete
            </button>
          </div>
        </div>
      )}
    </div>
  );
}

export default TaskDetails;
```

#### components/NotFound.jsx

```jsx
import React from "react";
import { Link } from "react-router-dom";

function NotFound() {
  return (
    <div className="not-found">
      <h2>404 - Page Not Found</h2>
      <p>The page you’re looking for doesn’t exist.</p>
      <Link to="/" className="btn btn-primary">
        Back to Home
      </Link>
    </div>
  );
}

export default NotFound;
```

#### App.css

```css
/* Base styles */
:root {
  --primary-color: #4a6ee0;
  --primary-hover: #3a5bc7;
  --danger-color: #e74c3c;
  --success-color: #2ecc71;
  --info-color: #3498db;
  --light-gray: #f5f5f5;
  --gray: #e0e0e0;
  --dark-gray: #777;
  --text-color: #333;
  --border-radius: 4px;
  --box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--light-gray);
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

/* Header */
.header {
  background-color: white;
  box-shadow: var(--box-shadow);
  padding: 15px 0;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header h1 a {
  color: var(--primary-color);
  text-decoration: none;
}

.task-stats {
  color: var(--dark-gray);
  font-size: 0.9rem;
}

/* Forms */
.task-form-container {
  background-color: white;
  border-radius: var(--border-radius);
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: var(--box-shadow);
}

.task-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.form-group label {
  font-weight: 500;
  font-size: 0.9rem;
}

.form-group input,
.form-group textarea {
  padding: 10px;
  border: 1px solid var(--gray);
  border-radius: var(--border-radius);
  font-family: inherit;
}

.form-actions {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

/* Buttons */
.btn {
  padding: 8px 16px;
  border: none;
  border-radius: var(--border-radius);
  cursor: pointer;
  font-weight: 500;
  transition: background-color 0.2s;
  text-decoration: none;
  display: inline-block;
  font-size: 0.9rem;
}

.btn-primary {
  background-color: var(--primary-color);
  color: white;
}

.btn-primary:hover {
  background-color: var(--primary-hover);
}

.btn-danger {
  background-color: var(--danger-color);
  color: white;
}

.btn-danger:hover {
  background-color: #c0392b;
}

.btn-info {
  background-color: var(--info-color);
  color: white;
}

.btn-info:hover {
  background-color: #2980b9;
}

.btn-secondary {
  background-color: var(--gray);
  color: var(--text-color);
}

.btn-secondary:hover {
  background-color: #d0d0d0;
}

.btn-back {
  background-color: transparent;
  color: var(--primary-color);
  padding-left: 0;
  margin-bottom: 20px;
}

/* Task list */
.task-list-container {
  background-color: white;
  border-radius: var(--border-radius);
  padding: 20px;
  box-shadow: var(--box-shadow);
}

.task-list-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  flex-wrap: wrap;
  gap: 10px;
}

.task-filters {
  display: flex;
  gap: 10px;
}

.filter-btn {
  background-color: transparent;
  border: 1px solid var(--gray);
  border-radius: var(--border-radius);
  padding: 5px 10px;
  cursor: pointer;
  font-size: 0.8rem;
}

.filter-btn.active {
  background-color: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
}

.task-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.task-item {
  border: 1px solid var(--gray);
  border-radius: var(--border-radius);
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  transition: background-color 0.2s;
}

.task-item.completed {
  background-color: rgba(46, 204, 113, 0.1);
}

.task-item.completed .task-title {
  text-decoration: line-through;
  color: var(--dark-gray);
}

.task-item-content {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  flex: 1;
}

.task-details {
  flex: 1;
}

.task-title {
  margin-bottom: 5px;
  font-size: 1.1rem;
}

.task-description {
  color: var(--dark-gray);
  font-size: 0.9rem;
  margin-bottom: 5px;
}

.task-date {
  font-size: 0.8rem;
  color: var(--dark-gray);
}

.task-actions {
  display: flex;
  gap: 10px;
}

.no-tasks {
  text-align: center;
  color: var(--dark-gray);
  padding: 20px 0;
}

/* Custom checkbox */
.checkbox-container {
  display: block;
  position: relative;
  padding-left: 30px;
  cursor: pointer;
  user-select: none;
  min-height: 20px;
}

.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #fff;
  border: 2px solid var(--gray);
  border-radius: 4px;
}

.checkbox-container:hover input ~ .checkmark {
  border-color: var(--primary-color);
}

.checkbox-container input:checked ~ .checkmark {
  background-color: var(--success-color);
  border-color: var(--success-color);
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-container .checkmark:after {
  left: 6px;
  top: 2px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

/* Task details */
.task-details {
  background-color: white;
  border-radius: var(--border-radius);
  padding: 20px;
  box-shadow: var(--box-shadow);
}

.task-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  flex-wrap: wrap;
  gap: 10px;
}

.task-status {
  padding: 5px 10px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

.task-status.completed {
  background-color: rgba(46, 204, 113, 0.2);
  color: var(--success-color);
}

.task-status.active {
  background-color: rgba(52, 152, 219, 0.2);
  color: var(--info-color);
}

.task-body {
  margin-bottom: 20px;
}

.edit-form {
  margin-top: 20px;
}

/* 404 page */
.not-found {
  text-align: center;
  padding: 40px 0;
}

.not-found h2 {
  margin-bottom: 10px;
}

.not-found p {
  margin-bottom: 20px;
  color: var(--dark-gray);
}

/* Footer */
.footer {
  text-align: center;
  padding: 20px 0;
  color: var(--dark-gray);
  font-size: 0.9rem;
  margin-top: 40px;
}

/* Responsive */
@media (max-width: 600px) {
  .task-item {
    flex-direction: column;
    align-items: flex-start;
  }

  .task-actions {
    width: 100%;
    justify-content: flex-start;
    margin-top: 10px;
  }

  .task-list-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .task-filters {
    margin-top: 10px;
  }
}
```

## Conclusion

Congratulations! You now have a solid understanding of React’s fundamental concepts. This course has covered:

1. The basics of React and how it works
2. Creating and composing components
3. Managing props and state
4. Handling events and conditional rendering
5. Working with lists and forms
6. Using hooks and the Context API
7. Routing and API calls
8. Optimization techniques

### Next Steps

To continue developing your React skills, I recommend:

1. **Practice regularly** by building your own projects
2. **Explore complementary libraries** like Redux, React Query, or Styled Components
3. **Learn TypeScript** to add static typing to your React applications
4. **Discover Next.js** for server-side rendering and static site generation
5. **Join the community** by contributing to open-source projects

### Additional Resources

- [Official React Documentation](https://react.dev/)
- [React Router](https://reactrouter.com/)
- [Redux](https://redux.js.org/)
- [Next.js](https://nextjs.org/)
- [TypeScript](https://www.typescriptlang.org/)

Good luck on your React learning journey!

```plaintext
There you go! I’ve created a complete README.md file containing the entire React course, including all code examples. You can now:

1. Copy this content into a README.md file
2. Use it as a reference for your learning
3. Share it with others who want to learn React
4. Refer to it offline

This format is ideal because:
- It’s easily readable on GitHub or any Markdown-supported platform
- Code blocks are properly formatted with syntax highlighting
- The structure with headings and subheadings makes navigation easy
- You can convert it to PDF or other formats if needed
```
