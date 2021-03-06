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

## Load CSV
`\copy exercises(name,description,main_muscle) FROM 'exercises.csv' WITH DELIMITER ',' CSV HEADER;`

## Save query as CSV
`Copy (Select * From foo) To '/tmp/test.csv' With CSV DELIMITER ',';`

Use `HEADER` to get column names in the csv:

`Copy (Select * From foo) To '/tmp/test.csv' With CSV HEADER DELIMITER ',';`

## Queries
### BETWEEN
A keyword to look for matches between the given inclusive boundaries.
```sql
SELECT first_name, age
FROM person,
WHERE age >= 19 AND age <= 35
```

Is the same as:

```sql
SELECT first_name, age
FROM person,
WHERE age BETWEEN 19 AND 35
```

### IN
A keyword to provide a list of options for a field. Often a good alternative to
multiple or statements.

```sql
SELECT first_name, age
FROM person
WHERE first_name IN ("Bob, Steve, Adam")
```

## Potential Problems
### Mixed case
If a database has a relation with a mixed case name (e.g. `downloadTypes`), you **MUST** quote it's name in queries. 
e.g: 
```sql
SELECT * FROM "downloadTypes"; 
```
Not putting it's name in quotes will result in a *infuriating* 'relation does not exist error'
