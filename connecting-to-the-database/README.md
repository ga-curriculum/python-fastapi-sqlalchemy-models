<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Connecting to the Database</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to connect their FastAPI application to a PostgreSQL database using the SQLAlchemy ORM.

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

# ! Connect FastAPI with SQLAlchemy
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

Now let's update `main.py`:

**main.py**

```py
# main.py

from fastapi import FastAPI
# Let's import some of the SQLAlchemy libraries that we'll need
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, Session
# Let's also import the database uri, which will point to our teas_db
from config.environment import db_URI
from controllers.teas import router as TeasRouter
from database import get_db  # import get_db from database.py

app = FastAPI()

app.include_router(TeasRouter, prefix="/api")

@app.get('/')
def home():
    return 'Hello World!'
```

Here we're pulling in the necessary packages as well as the `get_db` function we just created.

We're also importing a `db_URI` from an environment file. This file will configure environment variables that can change depending on what environment we're running our FastAPI app in (the values might be different in a testing environment vs our local environment).

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
db_URI = "postgresql://postgres:postgres@localhost:5432/teas_db"
```

This connection string will connect to the local PostgreSQL `teas_db` database on your system.
