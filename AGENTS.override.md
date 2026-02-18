This is a template API built entirely with GO from Alex Edward´s Let´s Go Further book, intended to be easily spin up to other backend projects with a tweak on the endpoints, data objects (since not all apps deal with movies lol), and auth.

We write an AGENTS.md file per directory for use with LLMs.

## Information

It’s important to be aware that httprouter doesn’t allow conflicting routes which potentially
match the same request. So, for example, you cannot register a route like GET /foo/new and
another route with a parameter segment that conflicts with it — like GET /foo/:id .


## Postgres

To install postgres, you can use the following command:

```
brew install postgresql
```
or 
```
sudo apt-get install postgresql
```
or 
```
choco install postgresql
```

on windows.

During installation, an operating system user named postgres should also have been
created on your machine. On Unix-based systems you can check your /etc/passwd file to
confirm this, like so:

```
cat /etc/passwd | grep 'postgres'
```

Connect via psql:

```
sudo -u postgres psql
```

### Creating a Database

To create a database, you can use the following command:

```
CREATE DATABASE mydatabase;
```

### Connecting to a Database

To connect to a database, you can use the following command:

```
\c mydatabase
```

### Rest of DB Tasks
1. Create a new user, without superuser permissions, password-based auth
2. Create citext extension

```
mydatabase=# CREATE ROLE user WITH LOGIN PASSWORD 'password';
CREATE ROLE
mydatabase=# CREATE EXTENSION IF NOT EXISTS citext;
CREATE EXTENSION
```

3. Aim to connect to the database using the new user
```
psql --host=localhost --dbname=mydatabase --username=user
```

4. Donwload a database driver - choosing pq in this case

```
go get github.com/lib/pq@v1
```

To connect to the database we’ll also need a data source name (DSN), which is basically a
string that contains the necessary connection parameters. The exact format of the DSN will
depend on which database driver you’re using (and should be described in the driver
documentation).


```
postgres://mydatabase:password@localhost/mydatabase
```

We want our DSN to be configurable at runtime


Note: If you receive the error message pq: SSL is not enabled on the server you
should set your DSN to:

postgres://mydatabase:password@localhost/mydatabase?sslmode=disable.

You can include this as an environment variable or a configuration file.
