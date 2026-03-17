# Copilot Instructions

Act as a senior fullstack engineer.

## Tech Stack

### Backend
- Java
- Dropwizard
- JDBI3
- PostgreSQL
- Liquibase

### Frontend
- React
- React Hooks
- Functional components

---

## Rules

### Backend
- Follow clean architecture
- Separate resource, service, dao layers
- Use JDBI3 for all database access
- Write DTO objects for request/response
- Resource only handles HTTP (validation, routing)
- Service contains business logic
- DAO contains database logic only
- Return DTO models from all endpoints

### Frontend
- Use React hooks (functional components only)
- Keep components small (under 200 lines)
- Separate api layer from UI components
- Use custom hooks to encapsulate logic
- Avoid business logic inside UI components
- Use fetch or axios for API calls

### Database
- Every schema change must have a Liquibase migration
- Never edit existing migrations
- Use indexed columns for foreign keys
- Avoid N+1 queries

### Testing
- Generate unit tests when possible
- Backend: test service and dao layers independently
- Frontend: test components with React Testing Library
