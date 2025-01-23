<h1>
  <span class="headline">Python and SQLAlchemy</span>
  <span class="subhead">Setup</span>
</h1>

## Setup


In this lesson, we’ll start by working with a pre-existing application that demonstrates full CRUD (Create, Read, Update, Delete) functionality on a mock data model. This will provide a solid foundation for integrating **SQLAlchemy** into the project.

### 1. Clone the Starter Code

We’ve provided a starter repository with the base application code. Clone the repository to your local machine and rename the folder for this lesson:

```bash
git clone https://git.generalassemb.ly/modular-curriculum-all-courses/python-fastapi-mvc-crud-app-build-solution
mv python-fastapi-mvc-crud-app-build-solution sql-alchemy-models
cd sql-alchemy-models
```

### 2. Install Dependencies

This project uses `pipenv` for managing dependencies. To install everything the project needs, run:

```bash
pipenv install
```

After installation is complete, activate the virtual environment and start the development server:

```bash
pipenv shell
uvicorn app.main:app --reload
```

You should now have the starter app running. Visit `http://127.0.0.1:8000` in your browser to confirm it’s working.


## Installing SQLAlchemy

SQLAlchemy is a powerful and flexible library for working with databases in Python. Although it’s not directly related to FastAPI, it integrates seamlessly and is widely used in FastAPI applications.

### 1. Install SQLAlchemy and psycopg2

For this lesson, we’ll be using **PostgreSQL** as our database engine. To connect Python to PostgreSQL, we’ll also need to install the `psycopg2-binary` adapter.

Install these dependencies in the virtual environment:

```bash
pipenv install sqlalchemy psycopg2-binary
```

### 2. Integrating SQLAlchemy

Now that SQLAlchemy is installed, we’ll start integrating it into our FastAPI app in the upcoming sections. 

In this module we will be:
- Defining models using SQLAlchemy’s ORM (Object Relational Mapper).
- Configuring a PostgreSQL database connection.
- Migrating from mock data to a real database.
