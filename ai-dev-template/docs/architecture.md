# System Architecture

## Pattern: Clean Architecture

---

## Backend Layers

```
Resource        (HTTP layer — handles routing, validation, serialization)
    ↓
Service         (Business logic layer)
    ↓
DAO             (Data access layer)
    ↓
Database        (PostgreSQL)
```

### Tech
- **Dropwizard** — REST API framework
- **JDBI3** — Data access (SQL objects pattern)
- **PostgreSQL** — Relational database
- **Liquibase** — Schema migration management

### Package Structure
```
com.example.app/
 ├─ resource/        # Dropwizard resources (REST endpoints)
 ├─ service/         # Business logic
 ├─ dao/             # Database access objects (JDBI)
 ├─ model/           # Domain models and DTOs
 └─ config/          # Dropwizard configuration classes
```

---

## Frontend Layers

**React SPA**

```
pages/          (Route-level views)
    ↓
components/     (Reusable UI components)
    ↑
hooks/          (Custom hooks — logic, state, side effects)
    ↑
api/            (API client functions — fetch/axios wrappers)
```

### Tech
- **React** — UI framework
- **React Hooks** — State and lifecycle management
- **Functional components** — No class components
- **Fetch / Axios** — HTTP client

---

## Data Flow

```
Frontend (React)
    │  HTTP/REST
    ▼
Dropwizard Resource
    │
    ▼
Service (business logic)
    │
    ▼
JDBI3 DAO
    │
    ▼
PostgreSQL
```

---

## Migration Strategy

All database schema changes are managed by **Liquibase** changelogs located in `backend/migrations/`.

- Every feature that requires schema changes must include a migration file.
- Migrations are applied in order and must never be edited after merging.
