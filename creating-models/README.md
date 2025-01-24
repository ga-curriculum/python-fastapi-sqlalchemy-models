<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Creating Models</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to define SQLAlchemy models for creating and managing database tables.

## Overview

Now that we’ve installed SQLAlchemy, it’s time to create a `model`. A model defines the structure of our data and handles interactions with the database.

In SQLAlchemy, a model is simply a **Python class** that represents a table in the database. The **class attributes** of the model map to the **columns** in the SQL table. This allows us to interact with the database using Python objects, rather than writing raw SQL queries.

### SQLAlchemy Model responsibilities

| Step                 | Description                                                                                                                                  |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Define DB Schema** | A model defines the structure of the database table, including column names, types, and constraints.                                         |
| **Map Data**         | A model converts/maps data in the database into Python objects. Each instance of the model class corresponds to a row in the database table. |
| **CRUD Operations**  | A model provides an interface for Create, Read, Update, and Delete (CRUD) operations on the database.                                        |

For this example, we will use **teas** as our resource.

### Defining Tea Model

To define a model, we will create a class in a file called `models/tea.py`:

```bash
touch models/tea.py
```

Add the following code which extends SQLAlchemy's `Base` class:

```py
# models/tea.py

from sqlalchemy import Column, Integer, String, Boolean
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

#  TeaModel extends SQLAlchemy's Base class.
#  Extending Base lets SQLAlchemy 'know' about our model, so it can use it.

class TeaModel(Base):

    # This will be used directly to make a
    # TABLE in Postgresql
    __tablename__ = "teas"

    id = Column(Integer, primary_key=True, index=True)

    # Specific columns for our Tea Table.
    name = Column(String, unique=True)
    in_stock = Column(Boolean)
    rating = Column(Integer)
```

> The _magic_ property `__tablename__` is used to name our table.

We define the table structure using the `Column` class, and various data types, which include:

- `Integer`
- `Float`
- `String`
- `Text`
- `Enums`
- `Boolean`
- `Date`
- `Time`
- `DateTime`
