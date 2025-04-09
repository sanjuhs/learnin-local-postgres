## Connect to Postgres on Mac

Remember before anything you need to first use brew and start service for postgres.

```bash
brew install postgresql
brew services start postgresql

```

or

```bash
brew services start postgresql@15
```

Once the postgres service is started, you can connect to the postgres server using the following command:

Just type in psql postgres and press enter.

```bash
psql postgres
```

You should get something like this

```bash
psql (17.2, server 15.12 (Homebrew))
Type "help" for help.

postgres=#
```

This means you are inside the Postgres CLI / shell and you can run SQL commands inside this.

---

## Create a new database

Inside the PSQL shell, you can use the following command:

```bash
CREATE DATABASE mydatabase;
```

On the bash command line, you can use the following command:

```bash
createdb mydatabase
```

---

## Connect to a specific database

To connect to a specific database, you can use the following command:

``

## Connect to Postgres on Mac

Remember before anything, you need to first use Homebrew to install and start the PostgreSQL service.

```bash
brew install postgresql
brew services start postgresql
```

Or, if you're using a specific version (like 15):

```bash
brew services start postgresql@15
```

---

## Access the Postgres CLI

Once the PostgreSQL service is running, you can connect to the default `postgres` database using:

```bash
psql postgres
```

You should see something like:

```bash
psql (17.2, server 15.12 (Homebrew))
Type "help" for help.

postgres=#
```

This means you are now inside the **Postgres shell**, and you can start running SQL commands.

---

## Create a new database

You can create a database in one of two ways:

### ✅ Inside the Postgres shell:

```sql
CREATE DATABASE mydatabase;
```

### ✅ Or directly from the terminal:

```bash
createdb mydatabase
```

You can check the list of all databases with:

```sql
\l
```

---

## Connect to a specific database

### ✅ From the terminal:

```bash
psql mydatabase
```

This connects you directly to that database.

### ✅ From inside the Postgres shell:

```sql
\c mydatabase
```

If the connection is successful, your prompt will change:

```bash
You are now connected to database "mydatabase" as user "yourusername".
mydatabase=#
```

---

## Check tables in the current database

Once connected to a specific database, you can list all tables with:

```sql
\dt
```

If no tables exist, you’ll see:

```bash
Did not find any relations.
```

You can also list schemas:

```sql
\dn
```

And describe a specific table structure:

```sql
\d tablename
```

---

## Find your Postgres connection string (for apps)

If you're using this database in an app (like with FastAPI + SQLAlchemy), your local database URL will look like:

```
postgresql://<username>:<password>@localhost:5432/<database>
```

For example, if your username is `sanjayprasads`, your DB is `conferencePlanner`, and you have no password:

```
postgresql://sanjayprasads@localhost:5432/conferencePlanner
```

---

## Exit the Postgres shell

Just type:

```sql
\q
```

And you're out !

---

Gotcha! Now let’s level up your markdown doc with all the essentials for working with **tables, relationships, and altering schemas** — the bread and butter of database design. Here's a clean, complete continuation of your doc:

---

## Creating Tables

Once you're connected to your database using `psql`, you can create a table using the `CREATE TABLE` command.

### ✅ Example: Basic `users` table

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Defining Relationships (Foreign Keys)

You can create related tables by referencing another table’s primary key using `FOREIGN KEY`.

### ✅ Example: `events` table referencing `users`

```sql
CREATE TABLE events (
  id SERIAL PRIMARY KEY,
  title TEXT NOT NULL,
  host_id INTEGER REFERENCES users(id),
  event_date DATE NOT NULL
);
```

This means each event is “hosted by” a user in the `users` table.

---

## Listing Tables and Their Structures

- List all tables in the current database:

  ```sql
  \dt
  ```

- View the schema of a specific table:
  ```sql
  \d tablename
  ```

---

## Inserting Data

You can add data into your tables like this:

```sql
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
INSERT INTO events (title, host_id, event_date) VALUES ('Postgres 101', 1, '2025-04-10');
```

---

## Viewing Data

```sql
SELECT * FROM users;
SELECT * FROM events;
```

You can join them too:

```sql
SELECT events.title, users.name AS host
FROM events
JOIN users ON events.host_id = users.id;
```

---

## Altering Tables (Modify Schema Later)

### ✅ Add a new column

```sql
ALTER TABLE users ADD COLUMN bio TEXT;
```

### ✅ Rename a column

```sql
ALTER TABLE users RENAME COLUMN bio TO biography;
```

### ✅ Drop a column

```sql
ALTER TABLE users DROP COLUMN biography;
```

### ✅ Change column data type

```sql
ALTER TABLE users ALTER COLUMN name TYPE VARCHAR(100);
```

---

## Dropping Tables (Careful!)

```sql
DROP TABLE events;
```

---

## Reset Serial ID Sequence (Optional)

If you delete all rows but want the `id` to start from 1 again:

```sql
TRUNCATE TABLE users RESTART IDENTITY;
```

---

## Bonus: Useful `psql` Meta Commands

| Command        | Description               |
| -------------- | ------------------------- |
| `\l`           | List all databases        |
| `\c dbname`    | Connect to a database     |
| `\dt`          | List tables in current DB |
| `\d tablename` | Describe table structure  |
| `\q`           | Exit the Postgres shell   |

---

## Sample ER Diagram

| Table: users |
| ------------ |
| id (PK)      |
| name         |
| email        |
| created_at   |

| Table: events |
| ------------- |
| id (PK)       |
| title         |
| host_id (FK)  |
| event_date    |

---

Now you're ready to design relational databases like a pro 🧠💥

```

Let me know if you want this turned into a real Postgres schema SQL file or if you want help drawing an ER diagram too!
```
