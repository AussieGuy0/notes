# Postgres
## Common Commands
### Sign in
`sudo -u postgres psql`

### List Databases
`\l`

### Connect To Database
`\c DB_NAME`

### Show Tables in DB
`\dt`

### Create User
`CREATE USER davide WITH PASSWORD 'jw8s0F4';`

### Give Database Creation to User
`ALTER USER miriam CREATEDB;`

### Disconnect All Users From Database
```sql
SELECT pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE datname = 'my';
```

### Drop database
`DROP DATABASE mydb;`

### Create Database
`CREATE DATABASE mydb;`

### Delete all tables in database
```sql
DROP SCHEMA public CASCADE;
CREATE SCHEMA public;

GRANT ALL ON SCHEMA public TO postgres;
GRANT ALL ON SCHEMA public TO public;
```

### Load SQL
`psql --username=postgres db_name < db_dump.sql`

## Potential Problems
### Mixed case
If a database has a relation with a mixed case name (e.g. `downloadTypes`), you **MUST** quote it's name in queries. 
e.g: 
```sql
SELECT * FROM "downloadTypes"; 
```
Not putting it's name in quotes will result in a *infuriating* 'relation does not exist error'
