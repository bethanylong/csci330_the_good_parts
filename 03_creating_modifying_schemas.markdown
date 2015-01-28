Creating and Modifying Schemas
==============================

A *schema* refers to how a specific database and its tables (plus other features, like views and stored procedures) are defined. This is as opposed to describing what specific pieces of data are stored there: the schema just describes the bare-bones scaffold that can hold the data.

Popular RDBMSs can hold many actual databases (in the schema sense), with all of them available at the same time. Commands to create databases and tables are run like any other query, but since you're typically only creating each database or table once, it makes the most sense to do that from the RDBMS's command line interface.

All of these commands have a wide range of additional options, such as ownership and access privileges, which are available in your RDBMS's documentation.

CREATE DATABASE
---------------

Intuitively, create a new database with the `CREATE DATABASE` command:

```
postgres=# CREATE DATABASE csci330_tgp;
```

Once you've created the database and want to add tables, you'll need to connect to that database. In Postgres, that's `\c databasename`.

CREATE TABLE
------------

Create a table with a certain set of columns using `CREATE TABLE`:

```
csci330_tgp=# CREATE TABLE unices (distro text, major_version integer, minor_version integer, release_date timestamp);
```

Within the parentheses is a list of column names and types. (Do they look familiar?) Standard SQL supports a relatively small set of column types that fit most needs (if awkwardly at times), but each RDBMS supports its own set of column types. Notably, the above table has a column with type `text`, which is Postgres's super awesome arbitrary-length string type, as opposed to standard SQL `varchar`s or `char`s.

Please avoid putting all your data in `text`/`varchar` columns if they're not actually all text. Parsing floats from strings is ~nobody's idea of a good time.
