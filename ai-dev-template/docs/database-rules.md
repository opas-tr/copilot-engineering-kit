# Database Rules

## Database
PostgreSQL

## Migration Tool
Liquibase

---

## Migration Rules

- Every schema change (table, column, index, constraint) **must** have a Liquibase migration
- **Never edit** existing migration files after they have been merged/applied
- Use sequential, descriptive naming: `YYYYMMDD_NNN_description.xml`
- Each migration file must have a unique `id` and `author` in the changeset

### Example Migration File

```xml
<!-- backend/migrations/20240101_001_create_users_table.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog
    xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
        http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-4.0.xsd">

    <changeSet id="20240101_001" author="dev">
        <createTable tableName="users">
            <column name="id"         type="BIGSERIAL" autoIncrement="true">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <column name="name"       type="VARCHAR(255)">
                <constraints nullable="false"/>
            </column>
            <column name="email"      type="VARCHAR(255)">
                <constraints nullable="false" unique="true"/>
            </column>
            <column name="created_at" type="TIMESTAMP" defaultValueComputed="NOW()">
                <constraints nullable="false"/>
            </column>
        </createTable>

        <createIndex tableName="users" indexName="idx_users_email">
            <column name="email"/>
        </createIndex>
    </changeSet>

</databaseChangeLog>
```

---

## Schema Design Rules

- **Primary keys:** Use `BIGSERIAL` (auto-increment) for all primary keys
- **Foreign keys:** Always create an index on foreign key columns
- **Timestamps:** Include `created_at` and `updated_at` on all tables
- **Naming:** Use `snake_case` for all table and column names
- **Constraints:** Define NOT NULL, UNIQUE, and FK constraints in migration

---

## Query Rules

- **Avoid N+1 queries** — use JOINs or batch queries where needed
- Do not duplicate raw SQL — centralize queries in DAO layer
- Use parameterized queries always (JDBI3 `:param` binding)
- Prefer indexes on columns used in WHERE, JOIN, and ORDER BY clauses

---

## Prohibited Actions

- ❌ Do not run raw DDL outside of Liquibase migrations
- ❌ Do not modify or delete existing changeset entries
- ❌ Do not use `SELECT *` in production queries
- ❌ Do not store sensitive data (passwords, tokens) in plain text
