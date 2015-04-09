Creating and Modifying Schemas
==============================

A **schema** refers to how a specific database and its tables (plus other
features, like views and stored procedures) are defined. This is as opposed to
describing what specific pieces of data are stored there: the schema just
describes the bare-bones scaffold that can hold the data.

Popular RDBMSs can hold many actual databases (in the schema sense), with all
of them available at the same time. Commands to create databases and tables are
run like any other query, but since you're typically only creating each
database or table once, it makes the most sense to do that from the RDBMS's
command line interface.

All of these commands have a wide range of additional options, such as
ownership and access privileges, which are available in your RDBMS's
documentation.

CREATE DATABASE
---------------

Intuitively, create a new database with the ``CREATE DATABASE`` command::

    postgres=# CREATE DATABASE csci330_tgp;

Once you've created the database and want to add tables, you'll need to connect
to that database. In Postgres, that's ``\c databasename``.

CREATE TABLE
------------

Create a table with a certain set of columns using ``CREATE TABLE``::

    csci330_tgp=# CREATE TABLE unices (distro text, major_version integer, minor_version integer, release_date timestamp);

Within the parentheses is a list of column names and types. (Do they look
familiar?) Standard SQL supports a relatively small set of column types that
fit most needs (if awkwardly at times), but each RDBMS supports its own set of
column types. Notably, the above table has a column with type ``text``, which
is Postgres's super awesome arbitrary-length string type, as opposed to
standard SQL ``varchar`` or ``char``.

Please avoid putting all your data in ``text``/``varchar`` columns if they're
not actually all text. Parsing floats from strings is ~nobody's idea of a good
time.

You can create your columns with certain constraints that further specify what
sort of data is stored there. To ensure that the special value ``NULL`` isn't
inserted in a column, use ``NOT NULL`` after the column type::

    csci330_tgp=# CREATE TABLE unices (distro text, major_version integer, minor_version integer, release_date timestamp NOT NULL);

To set a default value for a column so users or applications don't have to
explicitly insert data for it unless necessary, use ``DEFAULT`` after the column
type::

    csci330_tgp=# CREATE TABLE unices (distro text, major_version integer NOT NULL, minor_version integer DEFAULT 0, release_date timestamp DEFAULT NOW());

(``NOW()`` is a built-in function that returns the current date/time.)

DROP DATABASE and DROP TABLE
----------------------------

On the other hand, to destroy a database and all its contents, use ``DROP
DATABASE`` (with care)::

    postgres=# DROP DATABASE csci330_tgp;

Same goes for tables and ``DROP TABLE``::

    csci330_tgp=# DROP TABLE unices;

ALTER TABLE
-----------

Changing columns after table creation works a bit differently, since that
involves changing the definition of a table. Thankfully, the syntax is still
fairly intuitive.

Add a column::

    csci330_tgp=# ALTER TABLE unices ADD COLUMN free_as_in_beer boolean;

Destroy a column::

    csci330_tgp=# ALTER TABLE unices DROP COLUMN release_date;

Modify a column::

    csci330_tgp=# ALTER TABLE unices ALTER COLUMN major_version TYPE bigint;

    csci330_tgp=# ALTER TABLE unices ALTER COLUMN release_date SET NOT NULL;
    csci330_tgp=# ALTER TABLE unices ALTER COLUMN release_date DROP NOT NULL;

    csci330_tgp=# ALTER TABLE unices ALTER COLUMN major_version SET DEFAULT 0;
    csci330_tgp=# ALTER TABLE unices ALTER COLUMN major_version DROP DEFAULT;

Viewing your schemas
--------------------

Finally, in Postgres, use ``\d`` to examine databases and tables::

    csci330_tgp=# \d
             List of relations
     Schema |  Name  | Type  |  Owner  
    --------+--------+-------+---------
     public | unices | table | bethany

::

    csci330_tgp=# \d unices 
                        Table "public.unices"
        Column     |            Type             |   Modifiers   
    ---------------+-----------------------------+---------------
     distro        | text                        | 
     major_version | integer                     | 
     minor_version | integer                     | 
     release_date  | timestamp without time zone | default now()
