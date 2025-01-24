<h1>
  <span class="headline">FastAPI SQLAlchemy Models</span>
  <span class="subhead">Database Troubleshooting</span>
</h1>

## Troubleshooting PSQL database issues

If you encounter the error:

```
Ident authentication failed for user "postgres"
```

This means that your machine is having trouble authenticating to the PostgreSQL database. **Don’t worry!** This issue can be fixed by modifying the PostgreSQL configuration file. If you see this error, please **contact a member of your instructional team** for assistance before proceeding.

### What’s happening?

PostgreSQL is configured to use a specific authentication method called **"ident"** by default. This method tries to authenticate users based on the operating system’s username, which can sometimes cause issues when running the database as a different user.

In order to resolve this issue, we’ll change the authentication method to **"md5"**, which uses password-based authentication instead of the system's username.

## Steps to fix the issue

Only follow these steps if you see the **ident authentication failed** error. These changes are specific to the way PostgreSQL handles authentication and should only be done in this situation.

### 1. Open the `pg_hba.conf` file for editing

You will need to modify a configuration file that tells PostgreSQL how to authenticate users. You will likely need **root** permissions to edit this file, so use `sudo` to make changes.

Run one of the following commands based on which editor you prefer:

- Using `vi` editor:

  ```bash
  sudo vi /var/lib/pgsql/data/pg_hba.conf
  ```

- Using `nano` editor:
  ```bash
  sudo nano /var/lib/pgsql/data/pg_hba.conf
  ```

### 2. Modify the authentication method

Once the file is open, look for a line similar to this:

```
host    all       all      127.0.0.1/32      ident
```

Change the `ident` to `md5`, so it looks like this:

```
host    all       all      127.0.0.1/32      md5
```

This change tells PostgreSQL to require password-based authentication (md5) instead of the default ident-based authentication.

### 3. Save and exit the editor

- If using `vi`, press `Esc` then type `:wq` and press `Enter` to save and exit.
- If using `nano`, press `Ctrl + X`, then `Y` to confirm, and `Enter` to save.

### 4. Restart PostgreSQL

Now that you’ve updated the authentication settings, restart PostgreSQL to apply the changes:

```bash
sudo systemctl restart postgresql
```

### 5. Run the seed script

With the updated authentication method, you should now be able to run the `seed.py` script and populate your database with initial data:

```bash
pipenv run python seed.py
```
