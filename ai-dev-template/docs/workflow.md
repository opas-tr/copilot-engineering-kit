# Development Workflow

This workflow defines the standard process for implementing a new feature end-to-end.

---

## 1. Understand the Feature

- Read the feature spec (`docs/spec.md` or ticket)
- Review `docs/architecture.md` to identify which layers are affected
- Identify required API endpoints and database changes

---

## 2. Plan Implementation

- Define API endpoint contract (method, path, request/response shape)
- Identify database schema changes (tables, columns, indexes)
- Create or update Liquibase migration file

---

## 3. Backend Implementation

**Order:** Resource → Service → DAO

1. Create **DAO** interface using JDBI3 SQL objects
2. Create **Service** class with business logic
3. Create **Resource** class to expose the REST endpoint
4. Create or update **DTO models** for request/response
5. Register resource in Dropwizard application class

---

## 4. Frontend Implementation

**Order:** API client → Hook → Component

1. Create **API client** function in `frontend/src/api/`
2. Create **custom hook** in `frontend/src/hooks/` to manage state and call API
3. Create or update **UI component** in `frontend/src/components/`
4. Wire component into the appropriate **page** in `frontend/src/pages/`

---

## 5. Database Migration

1. Add a new Liquibase changelog file in `backend/migrations/`
2. Follow the naming convention: `YYYYMMDD_NNN_description.xml`
3. Never modify existing migration files

---

## 6. Testing

- **Backend:** Write unit tests for Service and DAO layers
- **Frontend:** Write component tests using React Testing Library
- Run full test suite before opening a pull request

---

## Summary

| Step | Layer | Output |
|------|-------|--------|
| 1 | Planning | Feature understanding |
| 2 | Planning | API contract + migration plan |
| 3 | Backend | Resource + Service + DAO |
| 4 | Frontend | API client + Hook + Component |
| 5 | Database | Liquibase changelog |
| 6 | Testing | Unit + component tests |
