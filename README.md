# React Documentation

---

## Part-1 (Introduction to React)

---

### 1. Introduction to React

### 1.1 What is React?

- React is a flexible, efficent JavaScript Library.
- It is developed by Facebook in 2013 for building user interface.

### 1.2 Why React?

- It helps us to create reusable components (small and isloated pieces of code using html, css, js)
- think about html tag and creating your own tag with react
- Load fast
- Allows us to use external plugin
- Major brands like facebook, instragram, youtube, airbnb use react.js

### 2. Environment setup

---

- VSCode
- node.js (Download LTS: Long Term Support one) (npm is included in node.js by default)
- React Developer tools

### 3. First react app

---

### 3.1 Method 1: add React to a website with CDN

- Code Example - 1 (create React app)

---

### 3.2 useEffect Hook

- Example 1

# UseEffectHook Component

This component demonstrates the usage of the `useEffect` hook in React.

## Code Example

```javascript
import React, { useEffect, useState } from "react";

const UseEffectHook = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Runs on every render
  });

  useEffect(() => {
    // Runs only on the first render
  }, []);

  useEffect(() => {
    // Runs on the first render
    // And any time any dependency value changes
  }, [prop, state]);

  // Runs on every render
  useEffect(() => {
    console.log("useEffect: " + count);
  });

  // Runs only on the first render
  useEffect(() => {
    console.log(count);
  }, []);

  // Runs on the first render and also when the dependency value changes
  useEffect(() => {
    console.log(count);
  }, [count]);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button
        onClick={() => {
          setCount((count) => count + 1);
        }}
      >
        +
      </button>
    </div>
  );
};

export default UseEffectHook;

# AnotherExample Component

# This component showcases the usage of the `useEffect` hook in React with a dependency.

# Code Example

import React, { useState, useEffect } from "react";

const UseEffectExample = () => {
  const [count, setCount] = useState(0);
  const [loading, setIsLoading] = useState(false);

  useEffect(() => {
    console.log("useEffect");
    console.log("isLoading: " + loading);
  }, [count]);

  return (
    <div>
      {console.log("render")}
      <h2>Count: {count}</h2>
      <button
        onClick={() => {
          setCount((count) => count + 1);
        }}
      >
        +
      </button>
      <button
        onClick={() => {
          setIsLoading(!loading);
        }}
      >
        Change Loading
      </button>
    </div>
  );
};

export default UseEffectExample;

3.3 fatch data using useEffect Hook
import React, { useEffect, useState } from "react";

const UseEffectHook = () => {
  const [todos, setTodos] = useState(null);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("https://jsonplaceholde.typicode.com/todos")
      .then((res) => {
        if (!res.ok) {
          throw Error("error while fetching the data");
        }
        return res.json();
      })
      .then((data) => {
        setTodos(data);
        setIsLoading(false);
        setError(null);
      })
      .catch((error) => {
        setIsLoading(false);
        setError(error.message);
      });
  }, []);

  const errorMessage = error && <p> {error} </p>;
  const loadingMessage = isLoading && "data is loading";

  const todosElement =
    todos &&
    todos.map((todo) => (
      <div key={todo.id}>
        <p>{todo.title}</p>
      </div>
    ));

  return (
    <div>
      {errorMessage}
      {loadingMessage}
      {todosElement}
    </div>
  );
};

export default UseEffectHook;