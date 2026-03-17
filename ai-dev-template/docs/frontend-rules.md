# Frontend Rules

## Framework
React (functional components only)

---

## Directory Structure

```
frontend/src/
 ├─ api/             # API client functions (fetch/axios wrappers)
 ├─ hooks/           # Custom React hooks
 ├─ components/      # Reusable UI components
 └─ pages/           # Route-level page components
```

---

## Component Rules

- Use **functional components** only — no class components
- Keep components **under 200 lines**
- One component per file
- Component filename matches the exported component name (PascalCase)

```jsx
// components/UserCard.jsx
export function UserCard({ user }) {
  return (
    <div className="user-card">
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}
```

---

## Hooks Rules

- Use **custom hooks** to encapsulate all business logic and side effects
- Hooks are prefixed with `use` (e.g., `useUsers`, `useAuth`)
- Keep hooks focused — one concern per hook
- Never put business logic directly in UI components

```js
// hooks/useUsers.js
import { useState, useEffect } from 'react';
import { fetchUsers } from '../api/usersApi';

export function useUsers() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetchUsers()
      .then(setUsers)
      .catch(setError)
      .finally(() => setLoading(false));
  }, []);

  return { users, loading, error };
}
```

---

## API Layer Rules

- All HTTP calls live in `src/api/`
- One file per resource/domain (e.g., `usersApi.js`, `ordersApi.js`)
- API functions return Promises
- Handle base URL and headers in a shared `apiClient` instance

```js
// api/usersApi.js
const BASE_URL = process.env.REACT_APP_API_URL;

export async function fetchUsers() {
  const res = await fetch(`${BASE_URL}/users`);
  if (!res.ok) throw new Error('Failed to fetch users');
  return res.json();
}

export async function createUser(data) {
  const res = await fetch(`${BASE_URL}/users`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data),
  });
  if (!res.ok) throw new Error('Failed to create user');
  return res.json();
}
```

---

## Prohibited Patterns

- ❌ No class components
- ❌ No business logic inside JSX / render functions
- ❌ No direct `fetch` calls inside components (use hooks)
- ❌ No inline styles — use CSS modules or a styling library
- ❌ No components exceeding 200 lines without splitting
