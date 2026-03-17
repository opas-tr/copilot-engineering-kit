# Backend Rules

## Language
Java

## Framework
Dropwizard

---

## Package Structure

```
src/main/java/com/example/app/
 ├─ resource/        # HTTP layer (Dropwizard resources)
 ├─ service/         # Business logic
 ├─ dao/             # Data access objects (JDBI3)
 ├─ model/           # Domain models and DTOs
 └─ config/          # Configuration classes
```

---

## Layer Responsibilities

### Resource
- Handles HTTP concerns only: routing, validation, serialization
- Maps incoming JSON to DTO objects
- Delegates to Service for all business logic
- Returns HTTP responses with appropriate status codes

```java
@Path("/users")
@Produces(MediaType.APPLICATION_JSON)
@Consumes(MediaType.APPLICATION_JSON)
public class UserResource {

    private final UserService userService;

    public UserResource(UserService userService) {
        this.userService = userService;
    }

    @GET
    @Path("/{id}")
    public Response getUser(@PathParam("id") long id) {
        return Response.ok(userService.getUser(id)).build();
    }
}
```

### Service
- Contains all business logic
- Validates business rules
- Orchestrates calls to one or more DAOs
- Throws domain-specific exceptions

```java
public class UserService {

    private final UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }

    public UserDto getUser(long id) {
        return userDao.findById(id)
            .orElseThrow(() -> new NotFoundException("User not found"));
    }
}
```

### DAO
- Contains all database access logic (JDBI3 SQL objects)
- No business logic in DAO
- Returns domain models or Optional

```java
@RegisterBeanMapper(User.class)
public interface UserDao {

    @SqlQuery("SELECT * FROM users WHERE id = :id")
    Optional<UserDto> findById(@Bind("id") long id);

    @SqlUpdate("INSERT INTO users (name, email) VALUES (:name, :email)")
    @GetGeneratedKeys
    long insert(@BindBean UserDto user);
}
```

---

## Rules

- Resource only handles HTTP — no business logic
- Service contains all business logic — no direct DB access
- DAO contains all database logic — use JDBI3 SQL objects
- Always return DTO models from endpoints (not raw entities)
- Register all JDBI DAOs via `jdbi.onDemand(XxxDao.class)`
- Use `@RegisterBeanMapper` or `@RegisterConstructorMapper` in DAOs
- Use `@BindBean` for binding POJO parameters in SQL updates
- Never expose internal domain model fields directly in responses

---

## DTOs

Create separate request and response DTOs:

```java
// Request DTO
public class CreateUserRequest {
    @NotEmpty private String name;
    @Email   private String email;
    // getters + setters
}

// Response DTO
public class UserDto {
    private long id;
    private String name;
    private String email;
    // getters + setters
}
```

---

## Exception Handling

- Use Dropwizard's built-in `WebApplicationException` subclasses
- Map domain exceptions to HTTP status codes in Resource layer
- Log errors at Service layer with appropriate level
