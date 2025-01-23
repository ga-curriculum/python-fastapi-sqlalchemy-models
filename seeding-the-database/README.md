<h1>
  <span class="headline">Python and SQLAlchemy</span>
  <span class="subhead">Seeding the Database</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to seed a PostgreSQL database using Python SQLAlchemy.

## Creating the Database

You will need to ensure that you have created a database before you attempt to seed it. Our seed program will create the _table_ but not the database itself. The database name should match the `db_URI` variable in `environment.py`, which is `teas_db`:

```sh
createdb teas_db -U postgres
```

When prompted for a password, enter `postgres`.

> Note: The `createdb` command is a utility command provided by PostgreSQL and may not be available if users are using different types of SQL databases.

To check that the database was created, we can check it using `psql`:

```sh
psql teas_db -U postgres
```

Type `\q` and hit enter to exit the `psql` shell.


<blockquote class="warning">
  🚨 Having issues with your password? See the troubleshooting section at the bottom of this page!
</blockquote>

## Seeding the Database

We should now be able to seed the database with the following commands:

```sh
pipenv run python seed.py
```

### Verifying the Data

Once seeding has completed, re-connect to the `psql` shell:

```sh
psql -d teas_db -U postgres
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

## Troubleshooting: Resetting PostgreSQL Password

This guide demonstrates how to reset the PostgreSQL `postgres` user password using the command line.


1. **Stop PostgreSQL Service**

```bash
 sudo systemctl stop postgresql
```

```bash
 sudo -u postgres postgres --single -D /var/lib/pgsql/data
```

2. **Change Password Inside PostgreSQL Prompt**

   Once inside the PostgreSQL single-user mode prompt, type the following command:

```bash
 alter user postgres with password 'postgres';
```

3. **Start PostgreSQL Service**

```bash
 sudo systemctl start postgresql
```

4. **Verify the Password Change**

```bash
 psql -U postgres
```

5. You can now log into **PostgreSQL** with the new password.
