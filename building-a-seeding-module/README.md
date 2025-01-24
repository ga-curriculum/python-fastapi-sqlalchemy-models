<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Building a Seeding Module</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to create a modular Python script for seeding a database with an application's
initial data.

## Overview

Now we're going to write a small Python script, `seed.py`. A seed program is used to populate a database with initial data, also known as seed data, when building an application.

The sole responsibility of this script is to generate our tables and put some initial testing data in our database. This will allow to make sure everything is working in terms of our models, _before_ we make any changes to our API itself.

## Populating the Seeding Module

Create a file `seed.py` in the root of your project;

```bash
touch seed.py
```

Add the following code:

```py
# seed.py
from sqlalchemy.orm import sessionmaker, Session
from models.tea import TeaModel, Base
from data.tea_data import teas_list
from config.environment import db_URI
from sqlalchemy import create_engine

engine = create_engine(db_URI)
SessionLocal = sessionmaker(bind=engine)

# This seed file is a separate program that can be used to "seed" our database with some initial data.
try:
    print("Recreating database..")
    # Dropping (or deleting) the tables and creating them again is for convenience. Once we start to play around with
    # our data, changing our models, this seed program will allow us to rapidly throw out the old data and replace it.
    Base.metadata.drop_all(bind=engine)
    Base.metadata.create_all(bind=engine)

    print("seeding our database..")
    # Seed teas
    db = SessionLocal()
    db.add_all(teas_list)
    db.commit()
    db.close()

    print("bye 👋")
except Exception as e:
    print(e)

```

## Modularizing the applications data

The data we're seeing will come from a new file named `data/tea_data.py`. Create a new directory for it:

```sh
mkdir data
```

Now move the old existing `models/tea_data.py` to `data`:

```sh
mv models/tea_data.py data
```

Edit `data/tea_data.py`, delete the existing content, and add the following:

```py
# data/tea_data.py
from models.tea import TeaModel

# We create some instances of our tea model here, which will be used in seeding.
teas_list = [
    TeaModel(name="chai", rating=4, in_stock=True),
    TeaModel(name="earl grey", rating=3, in_stock=False),
    TeaModel(name="matcha", rating=3, in_stock=True),
    TeaModel(name="green tea", rating=5, in_stock=True),
    TeaModel(name="black tea", rating=4, in_stock=True),
    TeaModel(name="oolong", rating=4, in_stock=False),
    TeaModel(name="hibiscus", rating=4, in_stock=True),
    TeaModel(name="peppermint", rating=5, in_stock=True),
    TeaModel(name="jasmine", rating=3, in_stock=True)
]
```

The above is the code that will actually create instances of our SQLAlchemy models to be used by our seeding program. It makes those lists of models ready for us to commit to the database in `seed.py`.

We can see where this is used in our `seed.py` here:

```py
# Seed teas
db.add_all(teas_list)
db.commit()
```
