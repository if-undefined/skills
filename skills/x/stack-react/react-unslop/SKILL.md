---
name: react-unslop
description: Idiomatic React state and effects. Use when writing or reviewing React components, component state or reducers, useEffect, derived state, or data fetching in components.
---

# React state and effects

## State

Plain `useState` and event handlers carry a component's logic until several handlers update the same pieces of state together. Then move those updates into a reducer.

## When NOT to Use Effects

Effects synchronize components with external systems. Many common use cases don't require them.

### Transforming Data for Rendering

Calculate derived values during render instead.

```typescript
// Avoid: redundant state and unnecessary Effect
function Form() {
  const [firstName, setFirstName] = useState("Taylor");
  const [lastName, setLastName] = useState("Swift");
  const [fullName, setFullName] = useState("");

  useEffect(() => {
    setFullName(firstName + " " + lastName);
  }, [firstName, lastName]);
}

// Good: calculated during rendering
function Form() {
  const [firstName, setFirstName] = useState("Taylor");
  const [lastName, setLastName] = useState("Swift");
  const fullName = firstName + " " + lastName;
}
```

### Caching Expensive Calculations

Use `useMemo` instead of Effects for expensive computations.

```typescript
// Avoid: unnecessary Effect for filtering
function TodoList({ todos, filter }) {
  const [visibleTodos, setVisibleTodos] = useState([]);

  useEffect(() => {
    setVisibleTodos(getFilteredTodos(todos, filter));
  }, [todos, filter]);
}

// Good: use useMemo for expensive calculations
function TodoList({ todos, filter }) {
  const visibleTodos = useMemo(() => {
    return getFilteredTodos(todos, filter);
  }, [todos, filter]);
}
```

### Handling User Events

Handle user interactions in event handlers, not Effects.

```typescript
// Avoid: Effect for user actions
function ProductPage({ product }) {
  useEffect(() => {
    if (product.isInCart) {
      showNotification(`Added ${product.name} to cart`);
    }
  }, [product]);
}

// Good: handle in event handler
function ProductPage({ product }) {
  function handleBuyClick() {
    addToCart(product.id);
    showNotification(`Added ${product.name} to cart`);
  }
}
```

### Resetting State When Props Change

Use the `key` prop to reset component state, or set state during render.

```typescript
// Avoid: Effect to reset state
function ProfilePage({ userId }) {
  const [comment, setComment] = useState('');

  useEffect(() => {
    setComment('');
  }, [userId]);
}

// Good: use key prop to reset entire component
<ProfilePage key={userId} userId={userId} />

// Good: or set state during render
function ProfilePage({ userId }) {
  const [comment, setComment] = useState('');
  const [prevUserId, setPrevUserId] = useState(userId);

  if (userId !== prevUserId) {
    setComment('');
    setPrevUserId(userId);
  }
}
```

### Sharing Logic Between Event Handlers

Extract shared logic into a function, don't use Effects.

```typescript
// Good: extract to function
function ProductPage({ product }) {
  function notifyAdded() {
    showNotification(`Added ${product.name} to cart`);
  }

  function handleBuyClick() {
    addToCart(product.id);
    notifyAdded();
  }

  function handleCheckoutClick() {
    addToCart(product.id);
    notifyAdded();
  }
}
```

## When TO Use Effects

### Synchronizing with External Systems

```typescript
// Good: synchronizing with browser API
function useOnlineStatus() {
  const [isOnline, setIsOnline] = useState(true);

  useEffect(() => {
    function handleOnline() {
      setIsOnline(true);
    }
    function handleOffline() {
      setIsOnline(false);
    }

    window.addEventListener("online", handleOnline);
    window.addEventListener("offline", handleOffline);

    return () => {
      window.removeEventListener("online", handleOnline);
      window.removeEventListener("offline", handleOffline);
    };
  }, []);

  return isOnline;
}
```

### Subscribing to External Stores

```typescript
// Good: subscribing to external store
function useOnlineStatus() {
  const [isOnline, setIsOnline] = useState(true);

  useEffect(() => {
    const unsubscribe = store.subscribe(() => {
      setIsOnline(store.getState().isOnline);
    });

    return () => unsubscribe();
  }, []);

  return isOnline;
}
```

## Summary

- If you can calculate something during render, you don't need an Effect
- To cache expensive calculations, add `useMemo` instead of `useEffect`
- To reset state, pass a different `key` to the component or set it during render
- Code that runs because a component was displayed should be in Effects; the rest should be in events
- Always add cleanup for Effects that fetch data or subscribe to external systems
- In Next.js, prefer Server Components and Server Actions over Effects for data fetching
