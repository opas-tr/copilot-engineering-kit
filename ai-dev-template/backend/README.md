# Backend — Java / Dropwizard / JDBI3

Place your Dropwizard application source here.

## Directory Layout

```
backend/
 ├─ src/
 │   └─ main/
 │       └─ java/
 │           └─ com/example/app/
 │               ├─ resource/
 │               ├─ service/
 │               ├─ dao/
 │               ├─ model/
 │               └─ config/
 ├─ resources/
 │   └─ config.yml          # Dropwizard configuration
 └─ migrations/
     └─ *.xml               # Liquibase changelogs
```

See `../docs/backend-rules.md` and `../docs/database-rules.md` for coding standards.
