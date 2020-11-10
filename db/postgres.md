# postgres

### 如何使用

```bash
#1
su - postgres
psql

#2
sudo -i -u postgres
psql
```

#### 建立使用者

```bash
sudo -i -u postgres
createuser --interactive --pwprompt
```

1. At the Enter name of role to add: prompt, type the user's name.
2. At the Enter password for new role: prompt, type a password for the user.
3. At the Enter it again: prompt, retype the password.
4. At the Shall the new role be a superuser? prompt, type y if you want to grant superuser access. Otherwise, type n.
5. At the Shall the new role be allowed to create databases? prompt, type y if you want to allow the user to create new databases. Otherwise, type n.
6. At the Shall the new role be allowed to create more new roles? prompt, type y if you want to allow the user to create new users. Otherwise, type n.
7. PostgreSQL creates the user with the settings you specified.

#### 修改權限

**1. Grant CONNECT to the database:**

```text
GRANT CONNECT ON DATABASE database_name TO username;
```

**2. Grant USAGE on schema:**

```text
GRANT USAGE ON SCHEMA schema_name TO username;
```

**3. Grant on all tables for DML statements: SELECT, INSERT, UPDATE, DELETE:**

```text
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA schema_name TO username;
```

**4. Grant all privileges on all tables in the schema:**

```text
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;
```

**5. Grant all privileges on all sequences in the schema:**

```text
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA schema_name TO username;
```

**6. Grant all privileges on the database:**

```text
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
```

**7. Grant permission to create database**:

```text
ALTER USER username CREATEDB;
```

**8. Make a user superuser**:

```text
ALTER USER myuser WITH SUPERUSER;
```

**9. Remove superuser status**:

```text
ALTER USER username WITH NOSUPERUSER;
```

### 資料來源

* \*\*\*\*[**How to manage PostgreSQL databases and users from the command line**](https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line)\*\*\*\*
* \*\*\*\*[**PostgreSQL - How to grant access to users?**](https://tableplus.com/blog/2018/04/postgresql-how-to-grant-access-to-users.html)\*\*\*\*
* \*\*\*\*[**how to install PostgreSQL on ubuntu20.04**](https://linuxconfig.org/ubuntu-20-04-postgresql-installation)\*\*\*\*

