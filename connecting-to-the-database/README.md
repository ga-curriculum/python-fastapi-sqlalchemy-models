<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Connecting to the Database</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to connect their FastAPI application to a PostgreSQL database using the SQLAlchemy ORM.

# Creating a database for Teas

### Open the `psql` shell as your `<username>`

If you are using **Mac or Linux**, open a terminal and run:

```bash
psql -U <username>
```

If you are on **Windows**, use:

```powershell
psql -U <username> -h localhost
```

This connects you as the username you created.

> **If you get a "role does not exist" error**, you need to create the `<username>` user first:
>
> ```sql
> CREATE ROLE "<username>" WITH LOGIN PASSWORD 'your_secure_password';
> ```
>
> Then, try connecting again.

### Create the `teas_db` database

Inside the `psql` shell, run:

```sql
CREATE DATABASE teas_db;
```

This creates a new PostgreSQL database named `teas_db`.

### Verify that the database was created

Run:

```sql
\l
```

This lists all databases. You should see `teas_db` in the list.

## Connecting our app to a database

First, we need to setup the database connection in a separate file called `database.py`.

```sh
touch database.py
```

Create this file in your editor and add the following:

```py
# database.py

from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, Session
from config.environment import db_URI

# Connect FastAPI with SQLAlchemy
engine = create_engine(
    db_URI
)

SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

Here we're doing a few things:

- We first import necessary libraries from SQLAlchemy (`create_engine` and `sessionmaker`).
- Then, we create an engine and a `SessionLocal` class with `create_engine` and `sessionmaker`. The `SessionLocal` class is our actual database session.
- The `get_db` function is a dependency that can be included in the path operation functions. This function creates a new session and closes it once the request is finished.

### Create a `config` file to hold our `db_URI`

Create the directory `config`:

```sh
mkdir config
```

Create `config/environment.py`:

```bash
touch config/environment.py
```

Add the following to your new `config` file:

```py
# config/environment.py
db_URI = "postgresql://<username>@localhost:5432/teas_db"
```

This connection string will connect to the local PostgreSQL `teas_db` database on your system.

- **_Modify your database connection string to use your username as the `<username>`._**
