<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Seeding the Database</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to seed a PostgreSQL database using Python SQLAlchemy.

## Seeding the Database

We should now be able to seed the database with the following commands:

```sh
pipenv run python seed.py
```

### Verifying the Data

Once seeding has completed, re-connect to the `psql` shell:

```sh
psql -d teas_db -U <username>
```

In the psql shell, run the following query:

```sql
SELECT * FROM teas;
```

You should see something like the following:

```
| id |       name       | in_stock | rating |
|----|------------------|----------|--------|
|  1 | chai             | t        |      4 |
|  2 | earl grey        | f        |      3 |
|  3 | matcha           | t        |      3 |
|  4 | green tea        | t        |      5 |
|  5 | black tea        | t        |      4 |
|  6 | oolong           | f        |      4 |
|  7 | hibiscus         | t        |      4 |
|  8 | peppermint       | t        |      5 |
|  9 | jasmine          | t        |      3 |
```

Well done! Remember, our API still does not use our database. We have a database and have seeded it with data, but we still need to link this up to our API.
