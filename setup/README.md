<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Setup</span>
</h1>

## Setup

In this lesson, we’ll start by working with a pre-existing application that demonstrates full CRUD (Create, Read, Update, Delete) functionality on a mock data model. This will provide a solid foundation for integrating **SQLAlchemy** into the project.

> If you have a complete, working application from the `Python FastAPI MVC CRUD Build` Lesson, you may choose to use that codebase as starter code instead of the repo provided below.

### 1. Clone the starter code

We’ve provided a starter repository with the base application code. Clone the repository to your local machine and rename the folder for this lesson:

```bash
git clone https://git.generalassemb.ly/modular-curriculum-all-courses/python-fastapi-mvc-crud-build-solution python-fastapi-sqlalchemy-models
cd python-fastapi-sqlalchemy-models
```

### 2. Install dependencies

This project uses `pipenv` for managing dependencies. To install everything the project needs, run:

```bash
pipenv install
```

## Installing SQLAlchemy

SQLAlchemy is a powerful and flexible library for working with databases in Python. While it is not part of FastAPI itself, it is commonly used in FastAPI applications for interacting with relational databases.

### 1. Install required database packages

For this lesson, we’ll be using **PostgreSQL** as our database engine. To work with PostgreSQL in Python, we need to install two new packages:

- **`SQLAlchemy`** – A popular Object Relational Mapper (ORM) that allows us to interact with databases using Python objects instead of raw SQL queries.
- **`psycopg2-binary`** – A PostgreSQL database adapter that enables SQLAlchemy to connect to and interact with PostgreSQL databases.

To install both dependencies in your virtual environment, run:

```bash
pipenv install sqlalchemy psycopg2-binary
```

### 2. Activate the virtual environment:

```sh
 pipenv shell
```

### 3. Start the development server:

```bash
pipenv run uvicorn main:app --reload
```

> You should now have the app running. Visit [`http://127.0.0.1:8000`](http://127.0.0.1:8000) in your browser to confirm it’s working.

Open the application in Visual Studio Code:

```bash
code .
```

### 4. Integrating SQLAlchemy

In this module we will be:

- Defining models using SQLAlchemy’s ORM (Object Relational Mapper).
- Configuring a PostgreSQL database connection.
- Migrating from mock data to a real database.
