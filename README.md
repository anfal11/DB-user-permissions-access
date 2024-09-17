# Managing Database User Permissions for Read/Write Access in MySQL, MSSQL, and PostgreSQL

In database administration, granting users specific read and write permissions on certain tables is common. I'll show you how to set up users with tailored permissions in **MySQL**, **Microsoft SQL Server (MSSQL)**, and **PostgreSQL**.

## MySQL: Granting Read and Write Access

### Step 1: Create a User

```sql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

### Step 2: Grant Read Access (SELECT) on a Table

```sql
GRANT SELECT ON database_name.table_name TO 'username'@'host';
```

### Step 3: Grant Write Access (INSERT/UPDATE/DELETE)

```sql
GRANT INSERT, UPDATE, DELETE ON database_name.table_name TO 'username'@'host';
```

### Step 4: Apply Changes

```sql
FLUSH PRIVILEGES;
```

---

## MSSQL: Granting Read and Write Access

### Step 1: Create a User with a Login

```sql
CREATE LOGIN username WITH PASSWORD = 'password';
USE database_name;
CREATE USER username FOR LOGIN username;
```

### Step 2: Grant Read Access (SELECT) on a Table

```sql
GRANT SELECT ON OBJECT::schema_name.table_name TO username;
```

### Step 3: Grant Write Access (INSERT/UPDATE/DELETE)

```sql
GRANT INSERT, UPDATE, DELETE ON OBJECT::schema_name.table_name TO username;
```

### Step 4: Verify Permissions

```sql
SELECT * FROM fn_my_permissions('schema_name.table_name', 'OBJECT');
```

---

## PostgreSQL: Granting Read and Write Access

### Step 1: Create a User

```sql
CREATE USER username WITH PASSWORD 'password';
```

### Step 2: Grant Read Access (SELECT) on a Table

```sql
GRANT SELECT ON table_name TO username;
```

### Step 3: Grant Write Access (INSERT/UPDATE/DELETE)

```sql
GRANT INSERT, UPDATE, DELETE ON table_name TO username;
```

### Step 4: (Optional) Grant Permissions at the Schema Level

```sql
GRANT SELECT ON ALL TABLES IN SCHEMA schema_name TO username;
GRANT INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA schema_name TO username;
```

---

## Summary

- **MySQL**: Use `GRANT SELECT` for read and `GRANT INSERT, UPDATE, DELETE` for write access.
- **MSSQL**: Use `GRANT SELECT` for read and `GRANT INSERT, UPDATE, DELETE` for write access on specific objects.
- **PostgreSQL**: Use `GRANT SELECT` for read and `GRANT INSERT, UPDATE, DELETE` for write access on specific tables.
